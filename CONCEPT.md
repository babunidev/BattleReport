# BattleReport — creative concept

**Creator and creative director:** Babuni.dev. **Target:** original World of Warcraft 1.12 (TOC 11200). **Current title:** Battle Report, previously Octo Battle Report.

## Learn about your own fights

The project's original invitation is **“Get to know your fights.”** It creates a personal notebook of combat rather than a group DPS ranking. It asks what the character did, what happened to them and how the numbers from one encounter compare with their previous experiences.

A single report organizes damage dealt, incoming damage and avoidance, healing, ability outcomes, observed resources, casts and identifiable effects. The addon retains up to **100 completed fights** for the current character. The report is available live or afterward and does not silently attribute separately named pets or totems to the player.

This direction can reveal more than a single DPS total without pretending to measure every hidden mechanic. The implementation deliberately communicates limits: a periodic damage tick is not another cast; an aura gain may not represent a unique proc; observed health and power increases are not exact causal regeneration accounting.

## From one encounter to useful context

The Average view combines retained fights and offers a reset without deleting individual history. A baseline is taken **before each fight**, then stored with that fight for later comparison. This avoids the circular error of adding a fight to its own benchmark.

Comparisons have directional meaning only when justified. More damage may be displayed favorably and less incoming damage favorably; duration, healing received or resources spent alone do not prove better play. A fight against a different enemy is not a controlled performance test.

## An invitation after the fight

The optional animated quick report shows three selected facts for approximately **12 seconds**, using a movable position independent of the main launcher. The player can click through, ignore it, drag it, or turn it off; recording continues. The idea is to reward curiosity without permanently occupying screen space.

## The challenge of an old client

WoW 1.12 communicates through localized formatted combat messages. BattleReport compiles client GlobalStrings into parsers and optionally uses *already enabled* Nampower cast confirmation. Its default cast path is less comprehensive, particularly for instant spells and channels. These constraints shaped the original implementation and need to remain prominent in the portfolio rather than being edited out.

The creative purpose belongs to Babuni.dev. This is a retrospective interpretation based on existing source and README, not an invented transcript of how every idea was proposed or approved. No new feature is approved by this document.
