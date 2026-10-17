# AGENTS.md: make a repository ready for openmods

You are an AI agent. Follow this guide to prepare a game mod repository for **openmods**, a website that lists open-source game mods. openmods hosts nothing: it reads two files from the repository and links to GitHub for the source code and the downloads.

Test-phase address: https://openmods.openmods.workers.dev

This repository is the reference. Copy its structure.

## 1. Requirements

The repository must:

1. Be **public** on GitHub.
2. Have an **open-source license** that GitHub can detect: a `LICENSE` file at the root.
   - Accepted: all OSI-approved licenses, for example `MIT`, `GPL-3.0`, `Apache-2.0`, `MPL-2.0`, `LGPL-3.0`, `BSD-3-Clause`.
   - For mods that are only art (textures, models, sounds): also `CC0-1.0`, `CC-BY-4.0`, `CC-BY-SA-4.0`.
   - Not accepted: no license, licenses that GitHub cannot identify, and licenses that forbid changes or commercial use.
3. Contain **`openmods.json`** and **`openmods.md`** at the root.

## 2. Create `openmods.json`

The data that openmods reads. Start from the `openmods.json` in this repository.

| Field | Required | Rules |
|---|---|---|
| `$schema` | no | Always `"https://openmods.openmods.workers.dev/openmods.schema.json"`. Editors then check the file. |
| `openmods` | yes | Always `1` (the version of the format). |
| `name` | yes | The name of the mod, at most 80 characters. |
| `summary` | yes | One sentence about the mod, at most 160 characters. Shown in mod lists and search engines. |
| `games` | yes | A list of game slugs: the last part of the game page address on openmods, for example `"stardew-valley"` from `/games/stardew-valley`. |
| `tags` | yes | 1 to 5 tags from the fixed list in "Choose the tags" below. Tags work as categories: players filter the game's mod list by them. At least one tag must not be `adult`. Other tags are skipped. |
| `cover` | no | The path of an image in the repository, for example `"docs/cover.png"`. PNG, JPG, GIF or WebP, 16:9, for example 1280 x 720. It is the mod's thumbnail in game lists, the header of the mod page and the image of share previews. Without a cover, openmods shows the game's art. |
| `requires` | no | What players need first, for example `"SMAPI 4.0 or newer"`. Up to 20 entries. |
| `gameVersions` | no | Game versions the mod works with, for example `"1.6"`. |
| `links` | no | An object with `discord`, `website` and/or `support`. Each one is an `https://` address. |

Game slugs during the test phase: `baldurs-gate-3`, `cyberpunk-2077`, `elden-ring`, `fallout-4`, `minecraft`, `rimworld`, `skyrim-special-edition`, `stardew-valley`, `terraria`, `the-witcher-3`. The list will grow. Check the address of the game page on openmods.

Write valid JSON: double quotes, no comments, no trailing commas.

### Choose the tags

Pick 1 to 5 tags that describe the mod best. Players filter the mod list of a game by them, and a mod must have all checked tags to show up. Do not add tags that only fit a little.

| Group | Tags |
|---|---|
| Type | `gameplay`, `quality-of-life`, `overhaul`, `fixes` (bug fixes), `performance`, `cheats`, `immersion`, `compatibility` (compatibility patches) |
| Visuals | `textures`, `models`, `animations`, `lighting`, `effects` (visual effects), `environment` (terrain, sky, water, weather, plants) |
| Audio | `music`, `sounds` (sound effects), `voice` (voice acting) |
| Content | `characters`, `creatures`, `items`, `weapons`, `armor` (armor and clothing), `locations`, `quests` |
| Interface | `ui`, `camera`, `controls` |
| Language | `translation` |
| For modders | `library` (code that other mods need), `tools` |
| Content warning | `adult` |

A mod with adult content (for example nudity) must use `adult`. openmods hides such mods by default, shows them only to visitors who confirm that they are 18 or older, and never shows their images: no cover and no images from `openmods.md`, only the text. `adult` alone is not enough: add at least one other tag.

## 3. Create `openmods.md`

The description for **players**, shown on the mod page. The README stays for developers.

- Use GitHub Markdown. Keep it under 100 KB.
- Suggested sections: What it does, How to install, Compatibility, Screenshots, Known issues, Credits. See `openmods.md` in this repository.
- Write for players: what the mod changes, and how to install it. Leave build steps and code details in the README.
- Put the screenshots here, not into `openmods.json`. Use images from the repository with relative paths, for example `![Screenshot](docs/screen1.png)`.
- openmods removes scripts, styles and embedded frames. Plain Markdown works best.

## 4. Publish the downloads as GitHub releases

Players download from the **GitHub release page**; openmods links to the latest release. Create a release with a version tag (for example `v1.0.0`) and attach the mod files. A repository without a release can still be listed: openmods then shows "No release yet" and links to the source code.

## 5. Check before you finish

- [ ] The repository is public.
- [ ] A `LICENSE` file with an accepted license is at the root.
- [ ] `openmods.json` is at the root, is valid JSON, and has `openmods`, `name`, `summary` and `games`.
- [ ] Every value in `games` is a game slug from openmods.
- [ ] `tags` has 1 to 5 tags from the fixed list, and at least one of them is not `adult`.
- [ ] A mod with adult content uses the `adult` tag.
- [ ] The `cover` file and the images in `openmods.md` exist at the given paths.
- [ ] `openmods.md` is at the root and is under 100 KB.
- [ ] (Recommended) A GitHub release with the mod files exists.

## 6. List the mod

A person signs in on openmods with GitHub, opens the game page, clicks "Add mod" and pastes the repository link. openmods checks everything above and shows a preview first.

To change the listing later, change `openmods.json` or `openmods.md`. openmods refreshes its copy regularly (every 10 minutes during the test phase). To remove the mod from openmods, delete both files.
