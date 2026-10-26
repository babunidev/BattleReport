# BattleReport — visual and interaction design

**Creative director:** Babuni.dev. **Implementation evidence:** current UI.lua, README, GUIDE and September Git revisions.

## A compact notebook, not a ranking interface

The current interface is a **720×652** movable dark window with soft gold heading, pale text, bounded cards and category accents: orange for damage, blue for defense, green for healing, purple for casts, teal for recovery. It is intentionally a **personal fight explorer**, not a raid leaderboard.

Seven tabs separate Overview, Damage, Defense, Healing, Casts, Effects and Recovery. The top navigation moves between the latest/live encounter, saved fights and a separate Average view. Lower arrows and wheel scroll through the seven visible detail rows. Hover details explain what the observations mean.

## Making context visible

The activity display uses dealt and taken bars for the fight's time bins, adapting the bin width when long fights exceed its bound. Cards can show a signed difference **versus prior average**; the initial baseline is frozen *before* a fight, so this is not self-comparison. An unavailable baseline is presented honestly as **No baseline**.

Color direction isn't a universal score. Higher damage or healing can be green; lower incoming damage can be green. Duration, healing received and resources spent have neutral signed differences because context determines value. The interface shouldn't imply a fight against a trivial mob proves better skill.

## The optional quick-report choreography

The prompt added September 7 shows **three randomly chosen facts** for about **twelve seconds** after its entrance. It animates the movable launcher out, into the temporary position and back, using a gentle pulse. Clicking opens the associated saved fight. Another combat start or disabling the option dismisses it.

A September 9 revision made the quick report itself draggable, with its **own saved location**, distinct from the normal launcher. Dragging pauses the display countdown and restarts it on release. The checkbox that disables the feature does not stop normal recording.

## Information ethics of combat numbers

A tick isn't a cast, an effect refresh isn't a unique proc, and a sampled resource gain doesn't identify a specific regeneration source. Good visual design includes those qualifications in tooltips and category descriptions rather than hiding uncertain assumptions behind attractive totals.

Open usability tests: keyboard/escape and focus, fixed-size window on small clients, tab contrast and dense rows, tooltip readability, prompt motion comfort, and usability when an older report has no resource/recovery field. Those checks were not performed in the current audit and no redesign has been approved.
