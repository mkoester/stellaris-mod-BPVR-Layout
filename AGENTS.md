# BPVR Layout

A local Stellaris mod (game **4.5.x**): BPV Reborn's building slots laid out as 8 government
slots in 2 rows of 4 and one row of 4 in every other zone. Replaces `BPVR - City 9 Slot` and
`BPV Reborn - Zone Single Row Mode`; what, why and the playset: `README.md`. **Never published**
— the GUI files are modified copies of another author's mod. Workspace context: `../AGENTS.md`.

- Only `bpvr_layout/` gets linked into the game: `scripts/link-mod.sh
  stellaris-mod-BPVR-Layout/bpvr_layout` from the workspace root, launcher closed.
- Keep the GUI files byte-identical to Single Row Mode except lines marked `# BPVR-Layout` (one of them heads the pop job info block, taken whole from UIOD 4.5), so an
  upstream update is a copy plus re-applying them (`README.md`, "Updating from upstream").
- Slot counts are BPVR scripted variables (`@BPV_CITY_SLOT`, `@BPV_ZONE_SLOT`,
  `@BPV_CITY_ZONES`), first definition wins; the core's help files explain them
  (`steamapps/workshop/content/281990/3576125834/help/`).

## Status (2026-11-10): 0.1.1, untested in game — 0.1.1 adds the 4.5 pop job info block
