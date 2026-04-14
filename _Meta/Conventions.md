# Vault Conventions

This file defines how we use this vault. Read it before creating or editing notes.

---

## Naming

- Use the canonical in-world terms from the consolidated lore. When in doubt, check the Glossary.
- File names use title case with hyphens for multi-word names: `Verdant-Expanse.md`, `High-Priest.md`.
- Enemy files follow the format: `Name (Common Name).md` — e.g. `Fiafhreine (Moss Deer).md`.
- NPC files use the character's in-world name: `Aine.md`, `Tuathal.md`.

## Canonical Terms

Use these. Do not invent synonyms in design notes.

| Term | Refers to | Do not use |
|------|-----------|------------|
| Athnemeton | The remembered civilisation on the Elder's planet | Athnemari, "the aliens" |
| Cethrai | Those connected to the energy cycle | Anointed |
| Dechrai | Those severed from the cycle | Profane |
| Nemethari | The original elf species | "the elves" (too generic) |
| The Beholder | The primal entity in the void | Demiurge (use only in meta/design commentary) |
| Overseers | The six enslaved representatives | Elders (collides with Nemethari Elder), Archons (use only in meta) |
| Aeonic Drive | The energy project | Perpetuum Mobile |
| Caer Bile | The world tree / hub city on the elf planet | — |

## Tags

Use tags sparingly. The following are the only tags in use:

- `#unresolved` — open design question, needs team input
- `#placeholder` — temporary content, to be replaced
- `#wip` — work in progress, do not treat as final
- `#canon` — reviewed and accepted as canonical lore

## Links

Use `[[wikilinks]]` to connect notes. If a note does not exist yet, link to it anyway — Obsidian will show it as an unresolved link, which tells us what notes still need to be written.

## Templates

Templates live in `_Meta/Templates/`. Use them when creating new enemies, NPCs, biomes, or quests. Copy the template into the appropriate folder and fill it in.

## Who writes where

Everyone writes in their areas. Use `Drafts/[your-name]/` for rough work. Move finished content into the proper folder.

| Person | Primary areas |
|--------|--------------|
| Toni | Sound design, atmosphere, lore coherence, dialogue editing, naming |
| Adrian (Banshi) | Lore, dialogue, atmosphere, art style, Godot |
| Kate | Lore, dialogue, voice over, sounds, art |
| Jurato | Animations, art, mechanics, coding/Godot |
| Borko | Coding, art for implementation needs |

## Git sync

The vault syncs automatically via obsidian-git every minute. See the setup guide if you haven't configured it yet. If you see merge conflict markers (`<<<<<<< HEAD`), resolve them and commit.
