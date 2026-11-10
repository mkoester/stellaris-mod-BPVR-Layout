# BPVR Layout (local)

A local Stellaris mod (game **4.5.x**) on top of the BPV Reborn building-slot mods: the
government zone of a city district gets **8 slots shown as 2 rows of 4**, and every other zone
shows **one row of 4**. **Never published**: its interface files are modified copies of
*BPV Reborn - Zone Single Row Mode* (Workshop 3485762595), whose author has not been asked.

Unofficial fan project, not affiliated with Paradox Interactive.

## What it replaces

| Replaced | By |
|---|---|
| `BPVR - City 9 Slot` (3575491852) | `common/scripted_variables/`: `@BPV_CITY_SLOT = 8` (same file names) |
| `BPV Reborn - Zone Single Row Mode` (3485762595) | `interface/`: its two files, changes marked `# BPVR-Layout` |

Changes in `interface/zzzz_planet_view.gui` (top of file, nothing else touched):

- `@primary_zone_slot_h` 6 → 4 — the government zone's grid wraps after 4 slots.
- `@secondary_zone_slot_h` 6 → 4 — every other zone's row holds 4.
- `@primary_zone_size_x` 320 → 216, `@secondary_zone_x` 420 → 316, `@secondary_zone_size_x`
  450 → 346 — the width the 5th and 6th slot used to take, removed.

## Playset

Still needed, enabled: `BPVR - More Building Slots` (core), `BPVR - 3 City Zones`,
`BPVR - 4 Zone Slots`, and `UI Overhaul Dynamic` (the GUI copy is UIOD-based).
Disabled: `BPVR - City 9 Slot`, `BPV Reborn - Zone Single Row Mode`/`Double Row Mode`.
This mod goes where Single Row Mode was: after UIOD and its add-ons.

Register (workspace root, launcher closed):

```
scripts/link-mod.sh stellaris-mod-BPVR-Layout/bpvr_layout
```

## Updating from upstream

When Single Row Mode updates, copy its two `interface/` files over these and re-apply the five
variables above (`diff` against the Workshop copy shows only those lines today).

Also taken over, from UI Overhaul Dynamic 4.5 (found comparing with `BPV Reborn - All-in-One`,
3824868657, v1.5.0, on 2026-11-10): the pop job info block. Single Row Mode's copy predates 4.5
and names its faction line `pop_faction`; 4.5 (vanilla and UIOD) has `pop_factions` plus a new
`wanted_factions` line, so the rows below move down 20 px and the box grows to 280. Re-apply this
too after an upstream copy (`diff` that block against UIOD's `interface/planet_view.gui`).

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
