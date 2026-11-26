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

**Blocked (2026-11-25): the BPVR core's update of that day crashes 4.6.0 at random.** With
`BPVR - More Building Slots` (3576125834, Workshop files 16:17) enabled, 10 of 12 sessions crashed
with SIGSEGV, 9 while loading (about 15-20 s after the last `error.log` line) and one at exit;
already with only the core, UIOD and Single Row Mode. 0 of 3 without it (UIOD on). Not the
cause: our Layout (crashed without it), the load order (both orders crashed and loaded), the
game files (Steam's check replaced nothing), kernel or driver (unchanged since 2026-11-21, when
yesterday's clean sessions ran). Still open: two clean sessions (launch + exit) with the core
off, a fresh download of the core (unsubscribe/resubscribe), then a report on its Workshop page
with a crash folder. The user upgraded the system and rebooted afterwards: count from scratch
after a kernel or driver change. Crash folders `stellaris_20261125_162053` to `_170214`.
2026-11-26, mkMac2014: reproduced (core + UIOD + Single Row Mode, `stellaris_20261126_081421`,
same stack region `+0x123edaa`); the user saw it on 3 machines. Clean launches (09:31, 09:36, 09:41) with
`BPVR - City 12 Slot`, `- 3 City Zones`, `- 6 Zone Slots` added (pure overrides of
`@BPV_CITY_SLOT`/`@BPV_ZONE_SLOT`/`@BPV_CITY_ZONES`, `BPV_district_slots.txt` and
`DEFAULT_MAX_PLANET_BUILDINGS_PER_ZONE`, which our Layout overrides too), then the 4th crashed
(`stellaris_20261126_094350`, `+0x123eda7`, the same chain): the add-ons do not fix it. No mods: 5 of 5 clean.
UIOD alone: a crash at run 4 or 5 (`stellaris_20261126_101231`), but not this one: SIGABRT, not
SIGSEGV, an uncaught C++ exception in a worker thread unwinding through `libsteam_api.so`
(`+0x12fbcc7`), 20 s after `error.log` line 34 (the mod list scan; the BPVR crashes reach ~150
lines, the end of database loading). Not counted against UIOD; the further UIOD-only runs (last
10:25) were clean. Core + UIOD, no Single Row Mode: the first run crashed
(`stellaris_20261126_103106`, SIGSEGV, `+0x123edaa`, the same chain): Single Row Mode is not needed.
**The core alone crashes** (`stellaris_20261126_103327`, `+0x123eda7`, the same chain). Its files,
object by object against vanilla 4.6 with its variables at their defaults, are vanilla apart from
the variables, except the district `zone_slots`: its `BPV_district_slots` inline script, which
gives rural districts their urban slot twice (`slot_energy`, `slot_energy_urban`,
`slot_energy_urban`; vanilla 4.6 has the first two). Whether that is new in 4.6 is unknown (no
old core files, the extraction does not record zone slots).
Resubscribed (all 86 files rewritten 10:39): the core alone crashed again (`_104048`; `_103843`
too, a minute before the files' timestamp). Not a corrupt download. Next: the report on its
Workshop page (`meta.yml`'s `LaunchArguments` hold the Paradox account ID and a session token:
drop that line before sharing a crash folder).

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
