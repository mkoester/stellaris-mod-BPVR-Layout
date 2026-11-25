# BPVR - Compact Layout (with some more slots and one more zone)

A Stellaris mod (game **4.6.x**): BPV Reborn's building slots laid out as 8 government
slots in 2 rows of 4 and one row of 4 in every other zone. Needs the core, `BPVR - More Building
Slots`, kept as a subscription (its district and zone overrides follow game patches); replaces
`BPVR - City 9 Slot`, `- 3 City Zones`, `- 4 Zone Slots` (folded in 2026-11-10, all numbers in
`common/scripted_variables/!!!bpvr_layout_settings.txt`) and `BPV Reborn - Zone Single Row Mode`; what, why and the playset: `README.md`. Workspace context: `../AGENTS.md`.

- **Public with the GUI author's permission**: the GUI files are modified copies of Sakura's
  Single Row Mode, and Sakura answered our request on the core mod's Workshop page (3576125834,
  2026-11-11 10:36 PST, to `MirkoMachine`): "please feel free to share your mod with us". Keep
  the credits in `README.md` and the store texts (`PUBLISHING.md`: store texts, IDs, checklist).
- Repo name and folder stay `stellaris-mod-BPVR-Layout` / `bpvr_layout/`; the public name lives
  in `descriptor.mod` only.
- Only `bpvr_layout/` gets linked into the game: `scripts/link-mod.sh
  stellaris-mod-BPVR-Layout/bpvr_layout` from the workspace root, launcher closed.
- Keep the GUI files byte-identical to Single Row Mode except lines marked `# BPVR-Layout`, so an
  upstream update is a three-way merge (`README.md`, "Updating from upstream").
  Expected error.log noise without Gigastructures: `Inexistent sprite type "GFX_*giga_birch*"`
  and `Gui type … is missing a name` from `zzzz_bpvr_giga_gui_birch_districts_uiod.gui`
  (Sakura's file, kept byte-identical; seen 2026-11-18). Cosmetic, not a finding.
- Slot counts are BPVR scripted variables (`@BPV_CITY_SLOT`, `@BPV_ZONE_SLOT`,
  `@BPV_CITY_ZONES`), first definition wins; the core's help files explain them
  (`steamapps/workshop/content/281990/3576125834/help/`).

## Game 4.6 (2026-11-25): rebased onto the 4.6 upstreams, not yet checked in game

Upstream updated on 2026-11-25 (Workshop files of that date): the BPVR core now writes 4.6's
`included_buildings` in its zone copies (the 4.6.0 break: `error.log` "Unexpected token:
include", zones without buildings), and Single Row Mode 1.1.0 and UIOD are `v4.6.*`.
- `zzzz_planet_view.gui` is Single Row Mode 1.1.0 plus our `# BPVR-Layout` lines (three-way
  merge, `README.md`). That brings 4.6's `ideology_window` and the pop job info block of UIOD 4.6
  (14 lines, `pop_factions` / `wanted_factions`), so our UIOD 4.5 copy of that block is gone.
- Single Row Mode now also ships `zzzz_sxx_districts_ui.gui`, the district windows of a
  third-party mod's `sxx_*` districts. Copied byte-identical, without our layout changes: not
  installed here, so untested.
- Turning this mod off in a running campaign drops its slot settings (8 government slots, third
  city zone, 4 per zone); untested what happens to buildings in them.

## Status (2026-11-10): 0.2.2 checked in game with only the BPVR core next to it (screenshot `2026_11_10_12`): 8 government slots, 3 zones of 4, rural zones 2×2 — the folded add-ons work — and Colony Production on 3 lines beside the city district. 0.2.1 checked in game: no city district scrollbar, nothing cut off (screenshot `2026_11_10_11`).
The layout (0.1.3 or 0.2.0) checked on an arkship, a volcanic capital, an orbital habitat and a shattered ring segment
(screenshots `2026_11_10_7`–`_10`): same layout on each, one main district, up to 27 cubes fit. 0.1.3 checked in game: Colony Production beside the city district, Build Queue moved up (screenshot `2026_11_10_6`). 0.1.2 checked in game — 8 government slots as 2×4, district cubes under them, specialization zones 1×4, rural zones 2×2, nothing overlapping (screenshot `2026_11_10_5`; 0.1.0: `_1`, UIOD and the BPVR modes for comparison: `_2`–`_4`)
