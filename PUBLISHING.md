# Publishing

Store copy and checklist for **BPVR - Compact Layout (with some more slots and one more zone)**.
Both stores are uploaded through the **Paradox Launcher** (Mod Tools → Upload Mod). Only
`bpvr_layout/` ships. `assets/` holds the thumbnail source (`thumbnail.svg`, our own art, rendered
with `rsvg-convert -w 512 -h 512 assets/thumbnail.svg -o bpvr_layout/thumbnail.png`) and the
store screenshot `planet-view.png`, cropped from the user's own F12 shot `2026_11_10_12.png` (the
0.2.2 check) to the planet window (`magick <shot> -crop 1220x1086+56+304 +repage <out>`).

Permission: Sakura (author of the GUI files' original, BPV Reborn - Zone Single Row Mode),
2026-11-11, on the core mod's Workshop page — `AGENTS.md`.

## Checklist (first release, 1.0.0)

- [x] Layout checked in game on 0.2.2 with only UIOD and the BPVR core next to it (`AGENTS.md`,
      Status), on a capital, an arkship, a habitat and a ring segment.
- [x] `picture="thumbnail.png"` (512×512, our own art), tags, public name.
- [ ] `version="1.0.0"` (own `chore:` commit).
- [ ] GitHub repo `mkoester/stellaris-mod-BPVR-Layout` created public, pushed.
- [x] Discord forum `bpvr-compact-layout` under MODS, invite `jw6YtHsSej` (2026-11-11), in the
      store texts below, `README.md` and `../docs/discord.md`.
- [ ] `scripts/clean-mods.sh` from the workspace root; `ls -A bpvr_layout` lists only
      `common/ descriptor.mod interface/ thumbnail.png`.
- [ ] Launcher closed → `scripts/link-mod.sh stellaris-mod-BPVR-Layout/bpvr_layout` → launcher
      open. On Linux the upload dialog may not see a **symlinked** mod: then copy the folder into
      `<user dir>/mod/` and upload the copy.
- [x] Upload to **Steam Workshop** (2026-11-11) (description: BBCode below, then the "More from me" block from
      `../docs/store-more-from-me.md` without this mod's line). On the item's page: add
      `assets/planet-view.png`, and **Required items** → UI Overhaul Dynamic (`1623423360`) and
      BPVR - More Building Slots (`3576125834`). A first upload starts **Hidden**: set it Public.
      The launcher writes `remote_file_id` into `descriptor.mod`: commit it.
- [ ] Upload to **Paradox Mods** (failed twice on 2026-11-11, "check mod files and credentials";
      launcher log: `Finalizing publication failed`, logged in, identical payloads. New against
      Empty Hulls: the 62-character name and `×` in the text, now `2x2`) (plain text below; format headings, lists and links with the
      website editor, then check the saved page). Add the screenshot there too.
- [ ] IDs into the table below, `../AGENTS.md` and `../docs/store-more-from-me.md`; then
      re-paste the "More from me" block into the other mods' descriptions, both stores.
- [ ] Unregister the dev copy (`slink --unlink stellaris-mod-BPVR-Layout/bpvr_layout`), subscribe
      to the Workshop item, and check the planet view once more in game.
- [ ] Optional: tell Sakura on the core mod's page, with the link.

## Published IDs

| Store | Item ID | URL |
|---|---|---|
| Steam Workshop | `3838089096` | https://steamcommunity.com/sharedfiles/filedetails/?id=3838089096 |
| Paradox Mods | | |

`descriptor.mod` carries only the Workshop ID (`remote_file_id`); the launcher keeps the Paradox
one in its own database.

---

## Store description — Steam Workshop (BBCode)

```bbcode
[h1]BPVR - Compact Layout[/h1]
[i](with some more slots and one more zone)[/i]

A tidier planet view for [url=https://steamcommunity.com/sharedfiles/filedetails/?id=3576125834]BPVR - More Building Slots[/url]: more building slots, laid out so you can see them all at a glance, without scrolling.

[h2]What you get[/h2]
[list]
[*][b]8 government slots[/b] in the city district, as 2 rows of 4 (vanilla: 6).
[*][b]A third specialization zone[/b] in every city district (vanilla: 2).
[*][b]4 slots in every other zone[/b] (vanilla: 3): one row of 4 in the city's zones, 2×2 in generator, mining and farming districts.
[*]The city district is shorter, so the rural districts below get the room, and [b]Colony Production[/b] sits beside it again, as in UI Overhaul Dynamic.
[/list]
Checked on a capital, an orbital habitat, a shattered ring segment and a Nomads arkship.

[h2]Setup[/h2]
[list]
[*][b]Required[/b], enabled and loaded before this mod: UI Overhaul Dynamic, BPVR - More Building Slots.
[*][b]Replaces[/b], so disable them: BPVR - City 9 Slot, BPVR - 3 City Zones, BPVR - 4 Zone Slots, and BPV Reborn - Zone Single Row Mode / Double Row Mode.
[*]Load it where Single Row Mode was: after UIOD and its add-ons.
[/list]

[h2]Compatibility[/h2]
[list]
[*]Built for Stellaris 4.5.x.
[*]Ancient Empires, Voyage to Eternity and VoidArk get the same slot numbers the replaced add-ons gave them (not tested with those mods).
[*]Changes the checksum: no achievements or Ironman while it is active.
[/list]

[h2]Credits[/h2]
This mod stands on [b]Sakura[/b]'s BPV Reborn: its interface files are modified copies of [url=https://steamcommunity.com/sharedfiles/filedetails/?id=3485762595]BPV Reborn - Zone Single Row Mode[/url], published with Sakura's kind permission. Thanks also to the original BPV author, and to UI Overhaul Dynamic, which the interface builds on.

[h2]Bugs & feedback[/h2]
Post them in the [url=https://discord.gg/jw6YtHsSej]bpvr-compact-layout forum on Discord[/url].

[i]Unofficial fan project, not affiliated with Paradox Interactive.[/i]
```

---

## Store description — Paradox Mods (plain text)

```text
BPVR - Compact Layout
(with some more slots and one more zone)

A tidier planet view for BPVR - More Building Slots: more building slots, laid out so you can see them all at a glance, without scrolling.

What you get
• 8 government slots in the city district, as 2 rows of 4 (vanilla: 6).
• A third specialization zone in every city district (vanilla: 2).
• 4 slots in every other zone (vanilla: 3): one row of 4 in the city's zones, 2x2 in generator, mining and farming districts.
• The city district is shorter, so the rural districts below get the room, and Colony Production sits beside it again, as in UI Overhaul Dynamic.
Checked on a capital, an orbital habitat, a shattered ring segment and a Nomads arkship.

Setup
• Required, enabled and loaded before this mod: UI Overhaul Dynamic, BPVR - More Building Slots.
• Replaces, so disable them: BPVR - City 9 Slot, BPVR - 3 City Zones, BPVR - 4 Zone Slots, and BPV Reborn - Zone Single Row Mode / Double Row Mode.
• Load it where Single Row Mode was: after UIOD and its add-ons.

Compatibility
• Built for Stellaris 4.5.x.
• Ancient Empires, Voyage to Eternity and VoidArk get the same slot numbers the replaced add-ons gave them (not tested with those mods).
• Changes the checksum: no achievements or Ironman while it is active.

Credits
This mod stands on Sakura's BPV Reborn: its interface files are modified copies of BPV Reborn - Zone Single Row Mode, published with Sakura's kind permission. Thanks also to the original BPV author, and to UI Overhaul Dynamic, which the interface builds on.

Bugs & feedback
Post them in the bpvr-compact-layout forum on Discord: https://discord.gg/jw6YtHsSej

Unofficial fan project, not affiliated with Paradox Interactive.
```
