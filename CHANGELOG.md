# BattleReport — dated Git and release history

**Creator:** Babuni.dev. Dates below distinguish source commits from release metadata and unverified usage.

## October 26, 2026 — full documentation audit

Expanded eleven Markdown files: README, concept, roadmap, changelog, agent rules, architecture, design, content, decisions, narrative journal and AI collaboration. The detailed preexisting GUIDE.md remains unchanged. Verified a published v1.6.5 release containing ZIP and checksum assets and corrected README download links to the current babunidev owner, plus the **/breport** alias. **Docs only:** no runtime scripts, tests, migration logic or media changed. No test was run.

## September 7, 2026 — Octo Battle Report appears

**b7cced7: Release Octo Battle Report 1.3.1.** First visible source included five modules (Core, Average, Resources, Parser, UI), a substantial GUIDE, README, test harness, per-character reporting and 100-fight rolling summaries. This was an initial **committed state**, not proof no earlier local prototypes existed.

**b5e0c54: Add optional animated post-fight quick reports.** Introduced three-fact prompt, a saved on/off option and lifecycle cleanup for dismissals and combat restart.

## September 8–9 — comparison and movement

**9c62c60 (Sep 8):** Captured prior-fight summary baseline at combat entry and used it for signed comparisons; improved quick-report cleanup.

**483c089 (Sep 9): Release 1.6.3.** Made quick reports independently draggable with persistent location and extra timed cleanup/parser regression handling.

## September 11 — revised definition of combat

**486ddc7: Release 1.6.4, record only during combat.** Removed earlier short buffering of opening/out-of-combat events and mana costs. Reports now close immediately on combat exit. This protects fight boundaries at the cost of missing events before combat status begins. Parser, resource handling, GUIDE and regression cases were updated.

## September 18 — new identity and preserved history

**4cea3d4: provider-neutral names and compatibility.** Renamed Octo Battle Report to **Battle Report**, changed Lua global and SavedVariables to **BattleReportDB**, changed TOC/slash aliases, and added saved-data migration utility plus PowerShell tests. Version advanced to **1.6.5**.

The [v1.6.5 release](https://github.com/babunidev/BattleReport/releases/tag/v1.6.5) was **published September 18** with **BattleReport.zip** and **SHA256SUMS.txt**. Its notes **report** successful packaging/syntax and regression/migration tests; an independent run was **not** part of this October documentation task.

## October 26 — attribution and doc foundations

Commits **ab15e79**, **2725e14**, **d5888bd** and **b57a8b4** standardized the Babuni.dev author credit and created the initial short docs/README links. This expanded narrative replaces that scaffold without retroactively inventing development conversations.
