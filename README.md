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

`BPV Reborn - All-in-One` (3824868657) merges the same mods with other numbers and claims fixes
for 4.5 (pop job info window, a parameter bug in the district slot inline scripts) — not
inspected yet.

## Test plan

1. Throwaway game: capital's city district shows 8 government slots in two rows of 4, three
   specialization zones of one row of 4 each; generator / mining / farming districts 4 slots.
2. A campaign save: the same, no building lost.
3. `logs/error.log`: no line naming `zzzz_planet_view.gui` or these scripted variables.
