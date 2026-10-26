# BattleReport — technical architecture and measurement limits

**Examined:** BattleReport.toc and Core.lua, Average.lua, Resources.lua, Parser.lua, UI.lua on October 26, 2026. **Source inspection**, not live-client or fixture execution.

## Manifest and module boundaries

```text
Interface 11200 / Version 1.6.5
SavedVariablesPerCharacter: BattleReportDB
  Core.lua       personal fight lifecycle, event aggregation, bounded timeline
  Average.lua    pre-fight baselines, per-fight average, reset and browsing
  Resources.lua  observed active power and health changes
  Parser.lua     old-client localized string parsing, events, optional Nampower
  UI.lua         seven tabs, comparison cards, launcher, prompt animations
```

One global **BattleReport** object coordinates the modules. There is no backend, remote API, network reporting or chat broadcast. The test harness uses Python lupa's Lua **5.1** runtime with a mocked WoW frame API, even though the addon targets Lua 5.0 conventions in a 1.12 client.

## Combat lifecycle and saved reports

Core creates **R.current** on player combat entry and can also start when an incoming parsed event arrives while **UnitAffectingCombat("player")** is true. On **PLAYER_REGEN_ENABLED** it finishes immediately; R.Tick also checks exit. Logout silently finishes a partial report.

Reports contain damage, incoming damage, healing, avoidances, ability/effect/cast/recovery maps, timeline, and prior-fight scalar baseline. R.Finish creates a saved report only when meaningful combat activity exists, assigns a serial number and unshifts it into **history**, dropping entries beyond 100. UI/window options and reports are stored in per-character BattleReportDB.

This strict window comes from the **v1.6.4** revision; opening casts/mana spent before combat is established are intentionally excluded. Don't resurrect an earlier two-second buffer in documentation as though still present.

The damage/incoming time chart has a **60-bin** upper bound: as a fight lengthens, pairs of bins are combined and their width doubles. This keeps the timeline bounded.

## Combat parser

Parser compiles the client's **GlobalStrings** printf-style patterns into Lua patterns. It handles percent-s/percent-d values and positional format placeholders, then evaluates more specific spell templates before broad melee templates. It parses personal hits, crits, spells, periodic damage/healing, avoidance, mitigated amounts, effects and certain environmental messages.

The parser normalizes a combat-text actor name matching the current player's UnitName to **player**, then ignores entries unrelated to that actor. This deliberately avoids broad party/pet metrics, but shared names, custom client messages and missing localized templates can undermine identification. Pet/totem contributions aren't automatically treated as the player's.

**Damage ticks, aura refreshes, cast completions and item trigger events describe different things**. Their counts must not be added as unique casts or procs.

### Cast confirmation

At login, the addon looks for **GetSpellRecField** and an *already enabled* Nampower **NP_EnableSpellGoEvents** setting. If both are available, it receives SPELL_CAST_EVENT requests and SPELL_GO_SELF, correlating accepted requests to server confirmations within **60 seconds**. It also distinguishes item-trigger events when an item ID appears.

Without these events, named SPELLCAST_START/STOP completions are recorded, with exclusions for interruption/failure. Instant casts and channels are incomplete in fallback. No code changes Nampower settings or hooks the player's casting functions.

## Resource and health sampling

Resources observes UnitPowerType, UnitMana and UnitManaMax for the active visible pool, and UnitHealth changes for player health. Positive delta is observed gain/recovery; negative delta is spend/loss. On power-type switch, capacity change, death or world entry, a baseline is reset rather than fabricating a massive cost.

These changes do **not** uniquely identify a potion, a hostile drain, MP5 or spirit: one update can contain multiple opposing causes. Named combat-log healing and resource restoration can overlap sampled positive deltas. At full health/mana, invisible excess regeneration isn't counted. Mana increases within five seconds of a recent decrease are a **timing proxy**, not a measured regeneration timer.

## Averaging and stored baseline

Average filters saved fights against **averageAfter** and excludeAverage flags. Scalar values and row counts are divided by fight count. Resource/recovery metrics use their own **coverage count** for older reports that didn't record those fields. Summed amount divided by summed fight durations produces an overall rate; **meanDPS** separately averages individual-fight DPS.

At **R.Start**, CaptureBaseline snapshots earlier scalar totals. Because the currently beginning fight isn't yet inserted, a completed report can compare against the past without including itself. ResetAverage advances a serial cutoff, keeping saved reports intact. Reset during combat flags that fight for exclusion from the new period.

## Window, interaction and performance

UI builds a **720×652** dark movable window, seven tabs (Overview, Damage, Defense, Healing, Casts, Effects, Recovery), rows with hover details, scrolling/paging and movable launcher. A **0.2-second** OnUpdate refresh checks visible UI. The optional quick-report flow shows three selected facts, fades/moves a launcher, holds around twelve seconds after fade-in, supports drag/pause and returns the button to its prior position.

The code uses implicit 1.12 callback globals (event, arg1, this), table.getn and math.mod. Direct modern WoW compatibility must not be assumed.

## Migration, release, tests

The Sep 18 **OctoBattleReportDB → BattleReportDB** rename required a PowerShell helper that reads TOCs, copies account/per-character SavedVariables, backs up originals and refuses overwrites without executing Lua source. Fixture: tests/test_upgrade.ps1.

The primary **tests/test_report.py** replays 1.12 strings through mocked game frames via Python lupa Lua 5.1. It requires the **gitignored** tests/GlobalStrings.lua file from an archived 1.12.1 game UI. The Sep 18 GitHub release notes say applicable tests passed; **none was run in this docs audit**. The published ZIP is not byte-verified against the code here.
