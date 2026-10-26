# Battle Report

**Author:** Babuni.dev

**Get to know your fights.** A lightweight personal combat report for World of Warcraft 1.12. Watch your numbers live, review your last encounter, or see your average performance across up to 100 fights.

**[Download the latest addon ZIP](https://github.com/Morkahja/BattleReport/releases/latest/download/BattleReport.zip)** · [All releases](https://github.com/Morkahja/BattleReport/releases)

## What does it show?

- **Damage:** how much you dealt, which abilities contributed, hits, criticals and periodic ticks.
- **Defense:** damage taken, who hit you, dodges, parries and blocks.
- **Healing and recovery:** healing done and received, observed health recovery, mana restored, rage generated and energy regenerated.
- **Resources:** mana, rage and energy used alongside the amounts recovered.
- **Casts and effects:** recorded spell casts, effect gains and identifiable item triggers.
- **Long-term averages:** per-fight amounts, counts and duration, with damage and healing rates.

This is a report for **your character**, not a group ranking. Pets and separately named totems are not attributed to you.

## Installation

1. [Download **BattleReport.zip**](https://github.com/Morkahja/BattleReport/releases/latest/download/BattleReport.zip) and extract it.
2. Copy the **BattleReport** folder into your game's **Interface\AddOns** folder.
3. Check that the folder structure looks like this—avoid an extra folder inside another folder:

   ```text
   World of Warcraft/
   └── Interface/
       └── AddOns/
           └── BattleReport/
               ├── BattleReport.toc
               ├── Core.lua
               ├── Average.lua
               ├── Resources.lua
               ├── Parser.lua
               └── UI.lua
   ```

4. Restart the game. At character selection, open **AddOns** and enable **Battle Report**.
5. Log in and click **Battle Report**, or type **`/battlereport`**.

For updates, replace the files in the existing addon folder, then type `/reload`. Your saved reports and window position are stored separately by the game.

**Compatibility:** made for the original 1.12 client. This package does not target modern WoW Retail or Blizzard Classic. No other addon is required; optional Nampower support improves cast tracking and item-source identification.

## Upgrade from a previous add-on name

If you used this add-on under a previous folder name, migrate your saved data
before playing with the new installation. A normal file replacement is not
enough when the folder and saved-variable names change.

1. Fully close the game. Keep the previous add-on installed for this step.
2. Install the new `BattleReport` folder beside the previous folder.
3. Open PowerShell in `BattleReport` and run the following, replacing both example values:

   ```powershell
   .\Upgrade-SavedData.ps1 -ClientPath "C:\Games\World of Warcraft" -PreviousAddonName "PreviousAddonFolder"
   ```

The helper reads the previous TOC, copies account-wide and per-character saved
data to the new names, and saves backups under `AddonUpgradeBackups` in the
game folder. It keeps the original files intact and refuses to overwrite
existing saved data for the new add-on. It does not execute saved Lua code.

4. Disable the previous add-on and enable **BattleReport** before entering the world.
5. Check your settings and saved data. Keep the backups until you have verified them.

Further updates using the same add-on name keep your saved data normally.
On other operating systems, back up the files, then copy the previous add-on's
`.lua` file in each `WTF/Account/**/SavedVariables` directory to `BattleReport.lua`.
Change only the top-level variable name declared in the old TOC to the matching
name in the new TOC; leave its table contents unchanged. Do this with the game closed.

## Your first report

Fight a mob, then open `/battlereport`. Recording is automatic, even while the window is closed. You can also leave it open during combat to watch the counters update.

### Optional quick report

Use the **Quick report** checkbox at the **top right of the main window** to turn the post-fight prompt on or off. It is enabled by default and remembers your choice per character. Turning it off dismisses any active prompt; normal fight recording and the main report continue to work.

**Move the quick report:** drag its **Battle Report** button while the facts are visible. Future quick reports appear at that saved position, remembered per character across reloads. The normal launcher has its own separate position. The timeout pauses while dragging and restarts for twelve seconds when you release the button.

After each recorded fight, the **Battle Report** button appears at your saved quick-report position (by default, centered horizontally one fifth of the way down the screen) for twelve seconds with a gentle pulse and three random facts from that fight on a translucent dark backdrop. The button fades out before changing position, then fades in; each fade takes a quarter-second. Its twelve-second display time starts once fully visible. Click it to open that report immediately while the button fades back, or let it return automatically to your saved position. Starting another fight dismisses the prompt. A hidden launcher appears temporarily for the prompt, then hides again.

Use the tabs to explore **Overview, Damage, Defense, Healing, Casts, Effects** and **Recovery**. Hover over a row for details. Scroll with the mouse wheel or use the lower arrows to browse more rows.

- **Live / Latest** follows the current fight, or displays the newest completed one.
- **Top arrows:** left decreases the saved-fight number; right increases it. Fight **1** is the newest.
- **Average** shows your per-fight averages from up to **100 completed fights**, saved separately for each character.
- **Reset average** starts a new average period while keeping individual reports. If you reset during combat, the next fight starts the new sample.

Drag the window by its header to move it. The small launcher button is movable too. Press **Escape** to close the report.

## Look beyond a single fight

Completed reports compare **Damage Dealt**, **Damage Taken**, and **Healing Done** with your average from before that fight. A small signed amount, such as `+120 vs avg`, shows the difference. More damage/healing dealt is green; less damage taken is green. The reverse is red, and equal values are neutral. Hover a card to see how many earlier fights formed the baseline.

Quick-report facts include the same signed comparison below their values. Higher DPS, critical hits, avoidance and resource recovery are green; lower values are red. Duration, resources spent and healing received use neutral differences because their direction alone does not establish better performance. Comparisons are observations across different encounters, not a rating of how well you played.

The baseline uses up to 100 completed fights in the current average period, excludes the fight being evaluated, and stays attached to that report. Resetting the average starts a fresh baseline for future fights. The first fight of a new period and older reports without a stored baseline show **No baseline**. Live and Average views do not color the three cards against themselves.

Average helps you compare your usual damage, incoming attacks, resource use and recovery over several encounters. Counts such as `0.8 dodges` mean an average per fight. Rates use the total amount divided by total combat time; Overview also includes the mean of individual fight DPS.

## See your effects

The Effects tab lists observed gains and item-triggered spells. When the client identifies the item, its name appears beside the effect and in the tooltip.

## A few things to know

Resource and health recovery are **observed changes**, not exact accounting of every cost or regeneration source. Simultaneous spending, damage and recovery can mask one another. The addon cannot always distinguish MP5, willpower or vampirism unless the combat log names the effect.

Effect gains are not always separate procs, and hits or periodic ticks are not separate casts. Without optional Nampower events, cast counts cover named cast-time completions and can miss instant spells and channels. Hover text explains what each measurement represents. Older reports may lack data added in later versions.

## Handy commands

| Command | Action |
| --- | --- |
| `/battlereport` or `/battlereport` | Open or close the report |
| `/battlereport last` | Show the last completed fight |
| `/battlereport button` | Hide or show the launcher |
| `/battlereport position` | Restore window and launcher positions |
| `/battlereport source` | Explain how to label an effect's source |

For capture details, fight boundaries and testing notes, see the [detailed guide](GUIDE.md).

### Combat-only recording

Recording starts when you enter combat and stops immediately when you leave it. Falling damage, healing, casts and resource changes outside combat do not create or enter reports. Opening actions reported before combat begins are excluded.
