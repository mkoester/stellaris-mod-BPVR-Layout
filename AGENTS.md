# BPVR Layout

A local Stellaris mod (game **4.5.x**): BPV Reborn's building slots laid out as 8 government
slots in 2 rows of 4 and one row of 4 in every other zone. Needs the core, `BPVR - More Building
Slots`, kept as a subscription (its district and zone overrides follow game patches); replaces
`BPVR - City 9 Slot`, `- 3 City Zones`, `- 4 Zone Slots` (folded in 2026-11-10, all numbers in
`common/scripted_variables/!!!bpvr_layout_settings.txt`) and `BPV Reborn - Zone Single Row Mode`; what, why and the playset: `README.md`. **Never published**
— the GUI files are modified copies of another author's mod. Workspace context: `../AGENTS.md`.

- Only `bpvr_layout/` gets linked into the game: `scripts/link-mod.sh
  stellaris-mod-BPVR-Layout/bpvr_layout` from the workspace root, launcher closed.
- Keep the GUI files byte-identical to Single Row Mode except lines marked `# BPVR-Layout` (one of them heads the pop job info block, taken whole from UIOD 4.5), so an
  upstream update is a copy plus re-applying them (`README.md`, "Updating from upstream").
- Slot counts are BPVR scripted variables (`@BPV_CITY_SLOT`, `@BPV_ZONE_SLOT`,
  `@BPV_CITY_ZONES`), first definition wins; the core's help files explain them
  (`steamapps/workshop/content/281990/3576125834/help/`).

## Status (2026-11-10): 0.2.2 checked in game with only the BPVR core next to it (screenshot `2026_11_10_12`): 8 government slots, 3 zones of 4, rural zones 2×2 — the folded add-ons work — and Colony Production on 3 lines beside the city district. 0.2.1 checked in game: no city district scrollbar, nothing cut off (screenshot `2026_11_10_11`).
The layout (0.1.3 or 0.2.0) checked on an arkship, a volcanic capital, an orbital habitat and a shattered ring segment
(screenshots `2026_11_10_7`–`_10`): same layout on each, one main district, up to 27 cubes fit. 0.1.3 checked in game: Colony Production beside the city district, Build Queue moved up (screenshot `2026_11_10_6`). 0.1.2 checked in game — 8 government slots as 2×4, district cubes under them, specialization zones 1×4, rural zones 2×2, nothing overlapping (screenshot `2026_11_10_5`; 0.1.0: `_1`, UIOD and the BPVR modes for comparison: `_2`–`_4`)
