# Publishing

Store copy and checklist for **BPVR - Compact Layout (with some more slots and one more zone)**.
**Steam Workshop only**: the Paradox Mods upload failed (below) and was given up on 2026-11-11;
its text stays here for a later try. Both stores are uploaded through the **Paradox Launcher** (Mod Tools → Upload Mod). Only
`bpvr_layout/` ships. `assets/` holds the thumbnail source (`thumbnail.svg`, our own art, rendered
with `rsvg-convert -w 512 -h 512 assets/thumbnail.svg -o bpvr_layout/thumbnail.png`) and the
store screenshot `planet-view.png`, cropped from the user's own F12 shot `2026_11_10_12.png` (the
0.2.2 check) to the planet window (`magick <shot> -crop 1220x1086+56+304 +repage <out>`).

Permission: Sakura (author of the GUI files' original, BPV Reborn - Zone Single Row Mode),
2026-11-11, on the core mod's Workshop page — `AGENTS.md`.

## Update for game 4.6 (2026-11-25)

Rebased onto Single Row Mode 1.1.0, the BPVR core's 4.6 update and UIOD 4.6 (`AGENTS.md`,
"Game 4.6"). Needs UIOD 4.6, so 4.6 only.
- [x] `supported_version="v4.6.*"`; store text says 4.6.x.
- [ ] `version="1.1.0"` (own `chore:` commit).
- [ ] In game, with UIOD and the BPVR core (both updated): README test plan 1–3, the planet
      view's ideology flags, the pop job info box (factions lines) and no scrollbar in the city
      district.
- [ ] `scripts/store_texts.py --all` (launcher closed), `scripts/clean-mods.sh`, upload to the
      Workshop. Change note: "Supports Stellaris 4.6 (Willpower): rebased onto BPV Reborn - Zone
      Single Row Mode 1.1.0 and UI Overhaul Dynamic 4.6."

## Checklist (first release, 1.0.0)

- [x] Layout checked in game on 0.2.2 with only UIOD and the BPVR core next to it (`AGENTS.md`,
      Status), on a capital, an arkship, a habitat and a ring segment.
- [x] `picture="thumbnail.png"` (512×512, our own art), tags, public name.
- [x] `version="1.0.0"` (own `chore:` commit).
- [x] GitHub repo `mkoester/stellaris-mod-BPVR-Layout` created public, pushed.
- [x] Discord forum `bpvr-compact-layout` under MODS, invite `jw6YtHsSej` (2026-11-11), in the
      store texts below, `README.md` and `../docs/discord.md`.
- [x] `scripts/clean-mods.sh` from the workspace root; `ls -A bpvr_layout` lists only
      `common/ descriptor.mod interface/ thumbnail.png`.
- [x] Launcher closed → `scripts/link-mod.sh stellaris-mod-BPVR-Layout/bpvr_layout` → launcher
      open. On Linux the upload dialog may not see a **symlinked** mod: then copy the folder into
      `<user dir>/mod/` and upload the copy.
- [x] Upload to **Steam Workshop** (2026-11-11) (description: BBCode below, then the "More from me" block from
      `../docs/store-more-from-me.md` without this mod's line). On the item's page: add
      `assets/planet-view.png`, and **Required items** → UI Overhaul Dynamic (`1623423360`) and
      BPVR - More Building Slots (`3576125834`). A first upload starts **Hidden**: set it Public.
      The launcher writes `remote_file_id` into `descriptor.mod`: commit it.
- [ ] ~~Upload to **Paradox Mods**~~ — given up (failed three times on 2026-11-11, the third with `2x2`, "check mod files and credentials";
      launcher log: `Finalizing publication failed`, logged in, identical payloads. New against
      Empty Hulls: the 62-character name, untried; whether UIOD and the BPVR core are on Paradox Mods
      at all is unchecked) (the launcher's form is filled by `slink`; check the saved page). Add
      the screenshot there too.
- [x] IDs into the table below, `../AGENTS.md` and `../docs/store-more-from-me.md`; then
      re-paste the "More from me" block into the other mods' descriptions, both stores
      (still to do: the Workshop blocks gained this mod's line).
- [ ] Unregister the dev copy (`slink --unlink stellaris-mod-BPVR-Layout/bpvr_layout`), subscribe
      to the Workshop item, and check the planet view once more in game.
- [ ] Optional: tell Sakura on the core mod's page, with the link.

## Published IDs

| Store | Item ID | URL |
|---|---|---|
| Steam Workshop | `3838089096` | https://steamcommunity.com/sharedfiles/filedetails/?id=3838089096 |
| Paradox Mods | — | not published |

`descriptor.mod` carries only the Workshop ID (`remote_file_id`); the launcher keeps the Paradox
one in its own database.

---

## Store description

`store/bpvr_layout.bbcode` is the Steam Workshop text (BBCode). `scripts/store_texts.py` in the workspace (run by `slink`, or on its own with the launcher closed) writes it into the launcher's upload form, with the "More from me" block appended, and makes the Paradox Mods HTML and short description from it. Edit the file, never the form.
