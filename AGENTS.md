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
  Likewise `Inexistent sprite type "GFX_sxx_button_district_*"` from `zzzz_sxx_districts_ui.gui`
  (the `sxx_*` districts' mod is not installed; seen 2026-11-25).
- Slot counts are BPVR scripted variables (`@BPV_CITY_SLOT`, `@BPV_ZONE_SLOT`,
  `@BPV_CITY_ZONES`), first definition wins; the core's help files explain them
  (`steamapps/workshop/content/281990/3576125834/help/`).

## Game 4.6 (2026-11-25): rebased onto the 4.6 upstreams, not yet checked in game

**The BPVR core's update of 2026-11-25 crashed 4.6.0 while loading, at random (reported on its
Workshop page, 3576125834, 2026-11-26). Its workaround, core 1.2.0 (Workshop files 2026-11-26
15:43), is not yet tallied:** tally the core alone (native, 3+ launches to the main menu, no
"already exists" line for a building in `error.log`) before the in-game check.
- Core 1.2.0 (2026-11-26, read on mkDell): the two files are renamed to vanilla's,
  `00_capital_buildings.txt` and `11_primitive_buildings.txt`, so they replace vanilla's files
  instead of redefining keys. Each holds all of vanilla 4.6.0's keys (20 and 28) and differs only
  by `branch_office_target_max_buildings_add = @BPV_CORP_SLOT_ADD_*` and comments. A full-file
  override must follow every patch that touches those files: diff them against the game after
  each update.
- Engine cause (Paradox forum bug report of 2026-10-18, 4.5.2, Windows build reverse-engineered,
  quoted by Sakura on 2026-11-26 — "Paradox should take responsibility"): redefining a vanilla
  building destroys the old one's modifier records but leaves their entries in the `modifier:`
  parser's global registry; a post-load loop then writes modifier ids into the freed objects (use
  after free). Linux's allocator puts live objects there and crashes, native and Proton alike;
  native Windows usually survives. Our guess sent to the author (links by key, `convert_to`) was
  wrong.
- Cause found (2026-11-26, the author's guess, confirmed by tally): the core's `common/buildings/`
  files, `00_capital_buildings_game.txt` and `11_primitive_buildings_game.txt`, define 14 vanilla
  buildings again under another file name (`error.log`: "Object with key: building_capital
  already exists, using the one at … `_game.txt`"). A local copy of the core without those two
  files: 6 of 6 launches clean (4 confirmed in the logs; with UIOD). The Workshop core the same
  day, same machine: 2 of 4 crashed. Its other 78 duplicate keys (districts, zones, starbase
  levels, agreement terms) stay in the copy and do not crash. Sent with the result: a guess,
  unverifiable (stripped binary), that other buildings link to the capitals by key
  (`convert_to` in `13_fallen_empire_buildings.txt` and `21_wilderness_buildings.txt`,
  `upgrades` in `16_first_contact_buildings.txt`) and a parallel load sometimes leaves a link to
  the discarded vanilla copy. Not a rename fix: the core's files hold 13 of the vanilla file's 20
  buildings and 1 of 28. The patch notes since 4.5.0 say only that duplicate keys now always log
  an error (4.5.1); nothing about them crashing.
- Testing a change to a Workshop mod: Steam restores a deleted or moved file of a subscribed item
  at the next launch, unnoticed (the files keep their old dates). Copy the item to a local folder,
  drop `remote_file_id` and rename it in `descriptor.mod`, `slink` it, and enable it instead of
  the Workshop item; check each run in `dlc_load.json` and `error.log` before the next launch
  (`logs/` is rewritten at each launch).
- Tally (2026-11-26, mkMac2014; also seen on 2 more machines): no mods 0 of 5 crashed, UIOD
  alone 0 of 5+, **the core alone 3 of 3** (also after unsubscribe/resubscribe), core + UIOD
  (± Single Row Mode, ± the add-ons City 12 Slot / 3 City Zones / 6 Zone Slots) 3 of 6.
  2026-11-25 (another machine): 10 of 12 with the core, 0 of 3 without.
- Signature: SIGSEGV about 15-25 s after the last `error.log` line (~126-150 lines, end of
  database loading), stack `+0x123eda7`/`+0x123edaa` → `+0xfdfdf9` → `+0x170b1f3` → `+0x9f6b6f`.
  A SIGABRT in a worker thread via `libsteam_api.so`, after 34 lines (`_20261126_101231`, UIOD
  alone), is another crash. The Windows build (Proton, `PROTON_USE_WINED3D=1`) crashes too:
  `EXCEPTION_ACCESS_VIOLATION` at `0x1403DCD03`, same stage.
- Not the cause: our Layout, Single Row Mode, UIOD, the load order, the slot add-ons, a corrupt
  download, the game files, kernel or driver.
- The core's files against vanilla 4.6, object by object with its variables at their defaults:
  vanilla apart from the variables, except the district `zone_slots`, whose `BPV_district_slots`
  inline script gives rural districts their urban slot twice (`slot_energy`,
  `slot_energy_urban`, `slot_energy_urban`; vanilla has the first two). Asked the author whether
  that is intended and new; we have no older core files to tell.
- Crash folders: native `stellaris_20261125_162053` to `_170214` (other machine),
  `stellaris_20261126_081421` to `_104048`; Proton `stellaris_20261126_110018` in the prefix.

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
