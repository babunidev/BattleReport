# BattleReport — implementation decisions and open alternatives

**Decision authority:** Babuni.dev. History is reconstructed from commits and source, not invented meetings.

| Evidence | Implemented design direction | Qualification |
| --- | --- | --- |
| Sep 7 initial v1.3.1 | Standalone, personal fight data, up to 100 completed per-character reports | Prior prototypes not visible |
| Sep 7 quick-report commit | Optional animated three-fact post-fight prompt | Player can opt out |
| Sep 8 baseline commit | Snapshot earlier fights at combat entry for signed comparisons | Excludes current fight |
| Sep 9 v1.6.3 | Independently draggable quick prompt, parser/cleanup refinements | No client tests repeated here |
| Sep 11 v1.6.4 | Strict combat-only capture, immediate finish on exit | Sacrifices pre-combat opener capture |
| Sep 18 v1.6.5 | Provider-neutral BattleReport rename and saved-data migration | Real previous files need safe test |

## Why the tradeoffs matter

**A personal journal instead of a group meter** favors attributable events and avoids turning another player's performance into the subject. It also means pet/totem damage may be absent.

**Combat-only events vs completeness:** the code once buffered events just before combat. Version 1.6.4 removed that behavior to avoid out-of-combat contamination. Opening ability costs occurring before the game combat flag can be missed. This is a real visible revision, not an assumed bug fix discussion.

**Averages vs context:** rates calculated across total combat time are appropriate aggregate measures; arithmetic mean individual-fight DPS is a different statistic. The pre-fight baseline avoids self-inclusion but doesn't standardize opponent difficulty or scenario.

**Optional enhancement vs dependency:** Nampower can improve cast reporting, but the addon does not require it or enable its CVar. Without it, named cast-time completions are incomplete for instant spells/channels.

**Observation vs causation:** health/resource deltas can combine sources, and aura/item events can overlap; user labels shouldn't be confused with authenticated item triggers.

**Personal layout:** quick summaries can be disabled, and separately saved positions limit annoyance while preserving the option for playful feedback.

## Pending creator decisions

Should pets be included via an explicit choice? Should there be a separately marked optional precombat buffer? Should history extend beyond 100? Should effect source confidence be visual? Should animation duration be customizable? Which client locales are actually supported? What license should apply to the original code?

These are **proposals only**. The documentation audit approved/implemented no runtime change. Preserve user alternatives and actual later decisions when they exist.
