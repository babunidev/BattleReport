# BattleReport — recorded data and interface vocabulary

**Project creator:** Babuni.dev. **Scope:** source-defined data contract and safe portfolio descriptions, not the user's real SavedVariables.

## What is stored

The TOC persists **BattleReportDB per character**. A completed fight can contain:
- Relative start/last/duration and timestamp, inferred encounter/enemy title.
- Damage dealt/taken, healing done/received, attempts, hits, periodic ticks, crits, incoming hits, avoidance and certain mitigation values.
- Named maps for abilities, defense, heals, effects, casts and recovery observations.
- Observed active resource changes (especially Mana, Rage and Energy); positive health updates.
- Damage/taken timeline with adjustable bin width and a stored **prior-fight baseline**.
- Report serial ID, optional exclusion from new average period, and cast-capture mode.

History retains **at most 100 saved completed reports**. The file also stores window, main launcher and prompt coordinates; **quickReport** preference; source-label mappings; and the **averageAfter** serial cutoff.

## Seven information groups

| Tab | Main question | Do not infer |
| --- | --- | --- |
| Overview | What happened in this fight? | Universal performance ranking |
| Damage | What abilities and outcomes dealt damage? | Every tick corresponds to a cast |
| Defense | Who hit me and which attacks were avoided? | Unreported armor reduction amounts |
| Healing | What healing was named in the combat log? | Exact effective heal after overhealing |
| Casts | What spell executions could the client count? | Instant/channel coverage without optional enhancement |
| Effects | Which auras, gains, triggers appeared? | Unique item/enchantment activation count |
| Recovery | How much health/resource visibly rose? | Exact MP5/spirit/potion source |

Source labels entered with **/battlereport source Effect = Item or enchantment** help future reports, but represent **user attribution**, not proof.

## Published and third-party artifacts

The repository contains **GUIDE.md**, five Lua modules, **tests/test_report.py**, **tests/test_upgrade.ps1**, and a SavedVariables migration utility. Historical Blizzard **GlobalStrings.lua** (needed for test playback) is gitignored, not an authored repository asset.

GitHub's [v1.6.5 release](https://github.com/babunidev/BattleReport/releases/tag/v1.6.5) includes **BattleReport.zip** and **SHA256SUMS.txt**. Earlier September Git history included three screenshots, but the **current tree has no screenshots folder**. Don't use broken links or present deleted images as current assets.

The repository has **no LICENSE** in the inspected current tree. No player's actual report data or other player information should be copied into a public portfolio without explicit review. Prefer synthetic examples.
