# BattleReport — human and AI development rules

**Creative owner / final decision-maker:** Babuni.dev. **Current:** Battle Report v1.6.5; originally Octo Battle Report.

Read README, GUIDE, TOC, all five Lua modules, existing tests, ROADMAP, docs/ARCHITECTURE, docs/DEVLOG and docs/DECISIONS before implementation. Preserve the **lightweight personal-report** premise, not a party leaderboard or automatic combat optimizer.

## Technical invariants

- The TOC targets **WoW 1.12 / interface 11200**, with **per-character** BattleReportDB.
- **Combat-only** recording was an explicit September 11 revision. Begin on player combat, finish immediately on exit; do not silently reintroduce pre-combat buffering.
- Retain at most **100 completed fights**, bounded timeline bins and cached average computation. A reset changes the average cutoff rather than deleting history.
- The baseline snapshot at combat **entry** must exclude the current fight, and a reset during combat must exclude the ongoing encounter from the new period.
- Resource gain/spend is observed delta, not exact expense or regeneration cause. Logged heals, power gains and sampled recovery may overlap.
- Build log parser rules from **actual client GlobalStrings**, including positional placeholders; avoid pretending all custom/localized formats are covered.
- Counts for periodic ticks, effects and accepted spells are distinct. Nampower cast confirmation is optional and should not change companion settings.
- Preserve optional Quick report with separate launcher/prompt positions, twelve-second hold, drag pause, opt-out and cleanup.
- Source labels supplied by the user are descriptions, **not proofs** that an item caused an effect.
- Do not merge pet/totem damage into player totals without explicit creative approval.
- The Sep 18 rename from OctoBattleReportDB to BattleReportDB needs safe migration and backups.
- There is **no LICENSE** in this repository. Never invent one or silently redistribute external fixture files.

## Testing and provenance

Run **python tests/test_report.py** only with the independently supplied 1.12.1 GlobalStrings fixture and lupa Lua 5.1; the fixture is gitignored. Run **tests/test_upgrade.ps1** on safe temporary folders. Record command, environment, actual output and gaps. Synthetic tests do **not** prove an actual WoW game session worked. Do not claim pass without executing the test.

For each substantial change update README, GUIDE when user facing, CHANGELOG, CONCEPT, ROADMAP, AGENTS, docs/DEVLOG, docs/DECISIONS, docs/DESIGN, docs/CONTENT, docs/ARCHITECTURE and docs/AI_COLLABORATION as relevant. Preserve *user direction*, assistant proposals, creative iteration, explicit user decisions, changed files/commits, and independently observed tests. Do not attribute Babuni.dev's original creative vision to AI.

Avoid publishing real combat histories, private characters/accounts, original private chats or credentials. This 2026-10-26 task is documentation-only.
