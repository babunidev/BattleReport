# BattleReport — roadmap and verification

**Decision authority:** Babuni.dev. These are source-backed test priorities and proposed options, not a claim of completed tests or approved new functionality.

## Implemented in current v1.6.5 source

Five Lua modules implement personal event capture, old-client log parsing, sampled resource/health deltas, per-fight baselines, rolling 100-fight averages and a seven-tab UI. Reports start with player combat and end on combat exit. Nampower enhancement is optional. An animated, movable post-fight summary is optional and remembers settings per character. The repo has Python/Lua and PowerShell fixture tests.

The [published September 18 v1.6.5 release](https://github.com/babunidev/BattleReport/releases/tag/v1.6.5) includes ZIP and checksum assets and says applicable source, regression and migration checks passed. **This October 26 documentation session did not rerun any tests** or download the archive.

## P0 — game-client truth

1. Install on the intended WoW 1.12 client, verify TOC load, UI and Lua errors, and record build/version.
2. Test one fight with outgoing direct/periodic damage, incoming hits, avoidance and healing; compare numbers to the actual combat log.
3. Confirm only the player's own character is counted. Separately named pets/totems are excluded, and players sharing a name may be ambiguous.
4. Verify **strict combat-only capture**: out-of-combat falling damage, resource usage and casting should not enter history; an opening spell before combat begins may be omitted.
5. Check fight closure on combat exit, partial-report behavior on logout, and the 100-report eviction boundary.
6. Compare **without Nampower** (named cast-time completions) and **with pre-enabled Nampower events** (accepted requests correlated with server go signals). Do not adjust companion CVars behind the player's back.
7. Test active-power spending/regeneration, health changes, caps, form/power-type changes, death, drains and simultaneous resource changes. Preserve the warning that observed deltas aren't proof of individual costs or MP5 sources.
8. Test average reset during combat, first fight after reset, baseline snapshot, uneven fight durations, missing older recovery data and per-character isolation.

## P1 — repeatable fixture and release checks

9. Run **python tests/test_report.py** with Python lupa Lua 5.1 and the original 1.12.1 **tests/GlobalStrings.lua** fixture from the archived Blizzard FrameXML. That fixture is *gitignored*, so a normal clone cannot run this test unchanged.
10. Run **tests/test_upgrade.ps1** in PowerShell on its synthetic temporary saved-data directories. Then test a backup copy of real old data with the game closed.
11. Verify the downloaded v1.6.5 ZIP digest against the published SHA256SUMS and inspect its exact file contents/TOC. No such byte-level check happened in this review.
12. Test localized/positional combat strings and custom-server messages; the parser can ignore unsupported formats.
13. Test optional coexistence with MeleeStartAttack or other game addons; BattleReport should not hook a player's casting functions.

## P2 — experience and publishing

14. Test all seven tabs, scrolling and hover explanations, 60-bin timeline scaling and usability at different game UI scales.
15. Exercise the twelve-second quick report through combat restart, mouse drag, hidden launcher, opt-out and logout; verify independent saved positions.
16. Verify slash aliases **/breport** and **/battlereport**, last/button/position/source commands.
17. Create safe portfolio screenshots from non-sensitive test character data. Early commit screenshots aren't present in today's main tree.
18. Decide a code license and confirm permissions around third-party test fixtures; there is no LICENSE in the current repository.

## Pending creative decisions (not approved)

Keep reports strictly self-only or optionally attribute pets? Keep strict combat boundaries or offer a user-opt-in opener buffer? Should the 100-report cap change? Should effect labels show confidence? Should quick-report animation be further adjustable? Which clients and locales should be *officially verified*? No answer to these questions is assumed.
