# BPVR - Compact Layout (with some more slots and one more zone)

A Stellaris mod (game **4.6.x**) on top of Sakura's BPV Reborn building-slot mods: the
government zone of a city district gets **8 slots shown as 2 rows of 4**, a city district gets a
**third specialization zone**, and every other zone gets **4 slots in one row** (2×2 in
generator, mining and farming districts). The city district is shorter, so the rural districts
below it get the room, and Colony Production sits beside it again, as in UIOD.

![The planet view with this mod](assets/planet-view.png)

**Requires**, enabled and loaded before this mod:
[UI Overhaul Dynamic](https://steamcommunity.com/sharedfiles/filedetails/?id=1623423360) and
[BPVR - More Building Slots](https://steamcommunity.com/sharedfiles/filedetails/?id=3576125834).
Bugs and feedback: the [bpvr-compact-layout forum on Discord](https://discord.gg/jw6YtHsSej).
Store pages, IDs and the release checklist: `PUBLISHING.md`.

Unofficial fan project, not affiliated with Paradox Interactive.

## Credits

- **Sakura**, author of BPV Reborn: the `interface/` files are copies of
  [BPV Reborn - Zone Single Row Mode](https://steamcommunity.com/sharedfiles/filedetails/?id=3485762595)
  (changes marked `# BPVR-Layout`), and the slot numbers are the scripted variables of
  [BPVR - More Building Slots](https://steamcommunity.com/sharedfiles/filedetails/?id=3576125834)
  and its add-ons. Published with Sakura's permission: "please feel free to share your mod with
  us" (comment on the core mod's Workshop page, 2026-11-11).
- **The original BPV (Better Planet View) author**, whose work BPV Reborn builds on.
- **UI Overhaul Dynamic**: the GUI is UIOD-based.

Only the changes marked `# BPVR-Layout`, the settings file and the store texts are ours.

## What it replaces

| Replaced | By |
|---|---|
| `BPVR - City 9 Slot` (3575491852) | `@BPV_CITY_SLOT = 8` |
| `BPVR - 3 City Zones` (3575502878) | `@BPV_CITY_ZONES = 3`, and its `common/inline_scripts/districts/BPV_district_slots.txt` (government + 3 zone lines; overrides the core's, so this mod loads after the core) |
| `BPVR - 4 Zone Slots` (3575511840) | `@BPV_ZONE_SLOT = 4`, and its `common/defines/zz_bpv_zone_slots_override.txt` (`DEFAULT_MAX_PLANET_BUILDINGS_PER_ZONE = 4`) |
| `BPV Reborn - Zone Single Row Mode` (3485762595) | `interface/`: its three files, changes marked `# BPVR-Layout` (only in `zzzz_planet_view.gui`) |

All slot numbers, and the third-party-mod values the add-ons set, are in
`common/scripted_variables/!!!bpvr_layout_settings.txt`. Changing one there also needs the file
its comment names.

Changes in `interface/zzzz_planet_view.gui` (top of file, nothing else touched):

- `@primary_zone_slot_h` 6 → 4 — the government zone's grid wraps after 4 slots.
- `@secondary_zone_slot_h` 6 → 4 — every other zone's row holds 4.
- `@primary_zone_size_x` 320 → 216, `@secondary_zone_x` 420 → 316, `@secondary_zone_size_x`
  450 → 346 — the width the 5th and 6th slot used to take, removed.
- City district cubes moved from a 3-wide column under the icon to an 8-wide band under the
  government zone (`district_box` in `planet_district_entry_width_2` and `_3`), so
  `@main_district_size_dy` 70 → 30: the city district is 40 px shorter and the rural districts
  below get the room.
- `@secondary_district_slot_h` 3 → 2 — a generator / mining / farming district's zone shows its
  4 slots as 2×2; a row of 4 would not fit the 285 px district box.
- Colony Production back beside the city district, as in UIOD: `@main_district_size_dx` 310 → 96
  (city district 666 wide, its zones end at 662), `@resource_offset_x/_y` 0, the box
  `@resource_box_width = 206` wide (UIOD: 300; its texts wrap instead) and as tall as the city
  district, at `y = 107` for every resolution. `@build_queue_offset_y` 185 → 0: the side column's
  Build Queue gets that room back. The `planet_district_entry_width_3` entry's fixed 865 follows
  the district width now.
- No scrollbar in the city district: `@main_district_scroll_x` 1200 → 208 (its window's height)
  and `@primary_zone_size_y` 1048 → 112 (2 rows). BPVR sized both for 10 zones and 20 rows; ours
  are fixed at 3 and 2. Since Single Row Mode 1.1.0 the scrollbar sits on the government zone,
  which at 2 rows holds all 8 slots, so it does not show.
  The rural districts' scrollbar stays as in UIOD.

## Playset

Still needed, enabled: `BPVR - More Building Slots` (core) and `UI Overhaul Dynamic` (the GUI
copy is UIOD-based); this mod after both. Disabled: `BPVR - City 9 Slot`, `BPVR - 3 City Zones`,
`BPVR - 4 Zone Slots`, `BPV Reborn - Zone Single Row Mode`/`Double Row Mode`.
This mod goes where Single Row Mode was: after UIOD and its add-ons.

Register (workspace root, launcher closed):

```
scripts/link-mod.sh stellaris-mod-BPVR-Layout/bpvr_layout
```

## Updating from upstream

When Single Row Mode updates, merge its new files onto ours three-way. The base is its previous
version: the commit that last took it over (2026-11-25, Single Row Mode 1.1.0) with our
`# BPVR-Layout` lines put back to its values. Then
`git merge-file -p <ours> <base> <new upstream>`: conflicts come only where upstream touched a
line we changed. Afterwards `diff` against the Workshop copy must show nothing but
`# BPVR-Layout` lines. The other two files carry none of our changes: copy them over.

Until 1.1.0 we carried UIOD 4.5's pop job info block (`pop_factions` plus `wanted_factions`) because
Single Row Mode's predated 4.5. 1.1.0 has UIOD 4.6's, identical line for line, so it is upstream's
again.

What else All-in-One changes, and why we skip it:
- Merges the core and the add-ons into one mod (12 / 6 / 4 zones) — we keep them separate.
- Own `bpvr_*` fonts and vanilla sprites/scrollbars instead of UIOD's — only needed without UIOD.
- `BPV_district_slots2`–`8` pass `GOVERNMENT` — those helpers are called by nothing, here or in
  vanilla.
- Building overrides as partial `*_game.txt` files instead of full copies — the core's full copies
  of `00_capital_buildings.txt` and `11_primitive_buildings.txt` match 4.5 vanilla apart from the
  slot variables, so nothing is stale.
- An Extra Districts zone patch — not installed here.

Its settings file confirms the load-order rule we rely on: for `@variables` the first definition
wins ("already taken" in `error.log`), so `bpv_city_slots_override.txt` beats the core's
`zz_bpv_defines.txt`.

## Test plan

1. Throwaway game: capital's city district shows 8 government slots in two rows of 4, three
   specialization zones of one row of 4 each; generator / mining / farming districts 4 slots.
2. A campaign save: the same, no building lost.
3. `logs/error.log`: no line naming `zzzz_planet_view.gui` or these scripted variables.
