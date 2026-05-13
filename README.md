# Vagabond — Chazut Addon

![Vagabond Chazut](vagabond_chazut.png)

An unofficial addon that extends the **Vagabond** mod for SPT (Single Player Tarkov) with additional trader exfils and transit points across the maps.

> ⚠️ The image above shows transits with a **100 000 roubles** entry cost. Those requirements **are not functional yet in Vagabond 0.6.1** — the author is actively working on a fix. Big thanks to **MrEliasen** for that! Until the upstream fix lands, you can roleplay the cost by **manually discarding 100 000 ₽ from your stash before taking the transit**. The cost lines are commented out in the config and will be re-enabled here as soon as Vagabond supports them properly.

## About

This is **not a standalone mod**. It is an addon that overlays files on top of an existing Vagabond install and the vanilla SPT data. All credit for the underlying transit/exfil framework goes to the original author of Vagabond:

- Forge page: https://forge.sp-tarkov.com/mod/2642/vagabond
- GitHub: https://github.com/MrEliasen/SPT-Vagabond

## Design intent

This addon was designed and balanced around a **Customs start with the hideout placed in Customs** (mine sits in **ZB-1011**). Every transit and trader exfil was tuned with that anchor point in mind, so distances, risks and rewards radiate outward from Customs.

The goal is to **add variety to how you move between maps without making the mod easier** — quite the opposite. Where vanilla Vagabond would let you flit anywhere for free, this addon adds a layer of soft progression to the most valuable destinations.

Different transits cost different things:

- **Roubles** — direct cash gate (e.g. reaching Streets or Ground Zero). *Currently simulate by discarding the amount manually until Vagabond 0.6.x ships the fix.*
- **Fuel** — some transits require expedition fuel, turning long-range travel into a logistics decision rather than a free teleport.
- **World events** — certain routes are gated behind in-raid actions, e.g. opening **D-2 on Reserve**, powering up **Interchange** *and* owning the matching keycard, etc.
- **Backpack sacrifice** — a few shortcuts exist for players willing to leave their loot behind to move fast.

That's the **goal** — a travel network where shortcuts exist but every shortcut has a cost. I won't pretend the current balance is perfect, so if you have suggestions or tweaks that push things further in that direction, I'll happily take them. Open an issue or a PR.

## What this addon adds

### Support for modded traders
Vagabond focuses on the vanilla trader roster, which is a perfectly reasonable scope for the base mod. This addon extends that roster by giving many popular modded traders their own dedicated extract on the relevant maps, so if you run a heavily modded trader setup each one becomes an actual destination you can travel to.

### More ways to travel between maps
Adds a varied set of extra transits across the map roster, opening up new routes between maps.

### Cleaner blend with vanilla SPT transits
A few vanilla SPT transits that overlapped with Vagabond's custom ones are turned off so the two systems don't fight each other.

> The originals are preserved in the `backup/` folder — restoring vanilla behavior is just a copy-paste away (see [Uninstall](#uninstall)).

## Installation

1. Make sure the base **Vagabond** mod is installed and working.
2. Copy the `SPT/` folder of this repo into your SPT installation root, overwriting:
   - `SPT_Data/database/locations/*/base.json`
   - `user/mods/Vagabond/*`
3. Launch the SPT server — Vagabond will pick up the extended config on startup.

> Back up your own files before overwriting if you have made local changes.

### Optional — match my starting setup

If you want to mirror the balance assumptions of this addon (Customs hideout, Croupier as your first vendor), edit `user/mods/Vagabond/config/vagabond.json` and change the following keys:

```json
"StartRaid": "Customs",
"StartExfilIdentifier": "VGB_EXT_CROUPIER_AMONYA"
```

This config don't have access to Fence at the very start, so your first raid has to land at a real vendor. Croupier is the closest viable option from Customs and his starter kits is at 150k — so you can buy one on raid #1 instead of being stuck naked.

This is **only needed if you have the Croupier trader installed** and want to copy my exact early-game pacing. Any other map and/or trader works too — just point `StartExfilIdentifier` at their `VGB_EXT_*` ID from `trader_locations.json`.

## Uninstall

Removing this addon is a two-step process — uninstalling Vagabond alone is **not enough**, because this addon also edits vanilla SPT location files (to disable a few transits that overlapped with Vagabond's). Those edits live outside the Vagabond mod folder and won't be reverted by deleting it.

1. **Restore the vanilla SPT files** — copy the contents of this repo's `backup/` folder into your SPT installation root, overwriting:
   - `SPT_Data/database/locations/bigmap/base.json`
   - `SPT_Data/database/locations/interchange/base.json`
   - `SPT_Data/database/locations/lighthouse/base.json`
   - `SPT_Data/database/locations/rezervbase/base.json`
   - `SPT_Data/database/locations/sandbox/base.json`
   - `SPT_Data/database/locations/sandbox_high/base.json`
   - `SPT_Data/database/locations/tarkovstreets/base.json`
   - `SPT_Data/database/locations/woods/base.json`
2. **Remove or restore Vagabond** — either delete `user/mods/Vagabond/` entirely, or restore your own clean Vagabond config files.

After step 1, all vanilla transit are back, regardless of whether you keep Vagabond afterward.

## Compatibility

- Built against **SPT 4.0.13** and **Vagabond 0.6.1**.
- Trader IDs in `trader_locations.json` reference specific third-party trader mods. Entries pointing to a trader you don't have installed are simply ignored by Vagabond.
- The transit-requirement lines (e.g. `Requires 100k roubles`) are currently commented out — they are bugged in Vagabond 0.6.1. They will be re-enabled here as soon as the upstream fix lands.
- Balance assumes a **Customs start + Customs hideout** (ZB-1011 in my own playthrough). Other starts will still work, but the difficulty curve was tuned around that anchor.

## Disclaimer

This addon is provided as-is, with no affiliation to or endorsement from the Vagabond author. Issues with this addon should be reported here, **not** on the upstream Vagabond repository.
