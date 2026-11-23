# BPVR - Compact Layout (with some more slots and one more zone)

A Stellaris mod (game **4.5.x**): BPV Reborn's building slots laid out as 8 government
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
- Keep the GUI files byte-identical to Single Row Mode except lines marked `# BPVR-Layout` (one of them heads the pop job info block, taken whole from UIOD 4.5), so an
  upstream update is a copy plus re-applying them (`README.md`, "Updating from upstream").
  Expected error.log noise without Gigastructures: `Inexistent sprite type "GFX_*giga_birch*"`
  and `Gui type … is missing a name` from `zzzz_bpvr_giga_gui_birch_districts_uiod.gui`
  (Sakura's file, kept byte-identical; seen 2026-11-18). Cosmetic, not a finding.
- Slot counts are BPVR scripted variables (`@BPV_CITY_SLOT`, `@BPV_ZONE_SLOT`,
  `@BPV_CITY_ZONES`), first definition wins; the core's help files explain them
  (`steamapps/workshop/content/281990/3576125834/help/`).

## Game 4.6.0 (2026-11-23): waiting for upstream

Not usable on 4.6 until upstream updates; the user waits for that rather than patching here.
- **The BPVR core (3576125834, files of 2026-11-13) breaks zones.** 4.6 renamed a district
  specialization's `include` / `exclude` to `included_buildings` / `excluded_buildings` (release
  notes, Modding). The core's full copies of the zone files still say `include = { all }`
  (`00_zones_game.txt` lines 30 and 96, `02_special_zones_game.txt` 29,
  `03_wilderness_zones_game.txt` 33): `error.log` "Unexpected token: include", then
  `Zone type 'zone_default' / 'zone_urban' / 'zone_urban_wilderness' does not include any
  buildings`, and at the month change 147 "Failed to add building <colony capital> … This District
  Specialization cannot support this Building" (the user's campaign, one month; no building was
  lost in that month). The copies also freeze 4.5's zones: 4.6 rewrote 5 zone files.
- **This mod's GUI needs UIOD**, which breaks 4.6's main menu (UIOD still `v4.5.*`). Without it 15
  of the planet view's 118 sprites and 6 fonts (`font_text_14`, `font_header_20`, …) are UIOD's.
  4.6's vanilla `planet_view.gui` also adds `ideology_window` / `ideology_flags` (~1410–1430),
  which our copy lacks: add it at the rebase onto UIOD's 4.6 version.
- Turning this mod off in a running campaign drops its slot settings (8 government slots, third
  city zone, 4 per zone); untested what happens to buildings in them.

## Status (2026-11-10): 0.2.2 checked in game with only the BPVR core next to it (screenshot `2026_11_10_12`): 8 government slots, 3 zones of 4, rural zones 2×2 — the folded add-ons work — and Colony Production on 3 lines beside the city district. 0.2.1 checked in game: no city district scrollbar, nothing cut off (screenshot `2026_11_10_11`).
The layout (0.1.3 or 0.2.0) checked on an arkship, a volcanic capital, an orbital habitat and a shattered ring segment
(screenshots `2026_11_10_7`–`_10`): same layout on each, one main district, up to 27 cubes fit. 0.1.3 checked in game: Colony Production beside the city district, Build Queue moved up (screenshot `2026_11_10_6`). 0.1.2 checked in game — 8 government slots as 2×4, district cubes under them, specialization zones 1×4, rural zones 2×2, nothing overlapping (screenshot `2026_11_10_5`; 0.1.0: `_1`, UIOD and the BPVR modes for comparison: `_2`–`_4`)
