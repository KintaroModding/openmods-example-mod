# AGENTS.md: make a repository ready for openmods

You are an AI agent. Follow this guide to prepare a game mod repository for **openmods**, a website that lists open-source game mods. openmods hosts nothing: it reads two files from the repository and links to GitHub for the source code and the downloads.

Website: https://openmods.nexus

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
| `$schema` | no | Always `"https://openmods.nexus/openmods.schema.json"`. Editors then check the file. |
| `openmods` | yes | Always `1` (the version of the format). |
| `name` | yes | The name of the mod, at most 80 characters. |
| `summary` | yes | One sentence about the mod, at most 200 characters. Shown in mod lists and search engines. openmods cuts a longer one with "…". |
| `games` | yes | A list of game slugs: the last part of the game page address on openmods, for example `"stardew-valley"` from `/games/stardew-valley`. No limit: a tool or framework can name every game it supports. The mod shows on a game page after the user adds it there once ("Add mod" on that game page). |
| `tags` | yes | 1 to 5 tags from the fixed list in "Choose the tags" below. Tags work as categories: players filter the game's mod list by them. At least one tag must not be `adult`. Other tags are skipped. |
| `cover` | no | The path of an image in the repository, for example `"docs/cover.webp"`. WebP is best, JPG is fine; PNG and GIF work too. 16:9, for example 1280 x 720, under about 500 KB. It is the mod's thumbnail in game lists, the header of the mod page and the image of share previews. Without a cover, openmods shows the game's art. |
| `requires` | no | What players need first, for example `"SMAPI 4.0 or newer"`. Up to 20 entries. |
| `gameVersions` | no | Game versions the mod works with. One list for all games, for example `["1.6"]`, or one list per game slug from `games`, for example `{ "stardew-valley": ["1.6"] }`. Up to 20 entries per list. |
| `links` | no | An object with `discord`, `website` and/or `support`. Each one is an `https://` address. |

The game slug is the last part of the game page's address on openmods: for `https://openmods.nexus/games/baldurs-gate-3` it is `baldurs-gate-3`. Find the game with the search on https://openmods.nexus/games. If the game is missing, the user can ask for it on the openmods Discord server: https://discord.gg/8vtph8SCFe

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

The description for **players**, shown on the mod page. Deeper developer details, such as the code structure, stay in the README.

- Use GitHub Markdown. Keep it under 100 KB.
- Suggested sections, in this order: What it does, Screenshots, How to install, How to use, Compatibility, Known issues, How to build, Credits. See `openmods.md` in this repository. Leave out a section that does not fit the mod, for example How to use when the mod has no settings, keys or commands.
- Write for players first: what the mod changes, and how to install, update and remove it.
- **How to build** shows how anyone can build the release files from the source code, so players can check that the download matches the code, and anyone can continue the mod later. Write it from the repository's real build files, for example a `*.csproj`, `package.json`, `Makefile` or build script: name the tools and their versions, the build command, and where the built files end up. Never invent a command. If the mod has no code, write: "Nothing to build: the release contains the files of this repository." If you cannot tell how the mod is built, ask the user.
- Put the screenshots here, not into `openmods.json`. Use images from the repository with relative paths, for example `![Screenshot](docs/screen1.webp)`, or pictures on another site, for example Imgur, with their full `https://` address. Use the direct address of the picture file (it usually ends in `.webp`, `.jpg`, `.png` or `.gif`), not the address of the page that shows it.
- Keep every picture small: WebP or JPG, at most 1920 x 1080, under about 500 KB. Mod managers download each picture in full, even for a small preview, and a 3 MB PNG screenshot is often under 400 KB as WebP. Convert PNG screenshots before you add them.
- openmods removes scripts, styles and embedded frames. Plain Markdown works best.

## 4. Publish the downloads as GitHub releases

Players download from the **GitHub release page**; openmods links to the latest release. Create a release with a version tag (for example `v1.0.0`) and attach the mod files. A repository without a release can still be listed: openmods then shows "No release yet" and links to the source code.

### Write the release notes

The text of each GitHub release is the mod's **changelog**. Mod managers show it to players, for example before an update.

- Write it for players: what changed in this version. Do not repeat how to install; that is in `openmods.md`.
- Use the same form in every release. Leave out a heading that has nothing under it:

  ```markdown
  ## Added
  - A new option to hide the outlines in combat.

  ## Changed
  - The outlines are thinner.

  ## Fixed
  - The map no longer flickers after loading a save.
  ```

- One change per line, in short sentences.
- The first release can say "First release." and list what the mod does.
- The tag is the version, for example `v1.2.0`. Use a new tag for every release.

## 5. Check before you finish

- [ ] The repository is public.
- [ ] A `LICENSE` file with an accepted license is at the root.
- [ ] `openmods.json` is at the root, is valid JSON, and has `openmods`, `name`, `summary` and `games`.
- [ ] `summary` has at most 200 characters.
- [ ] Every value in `games` is a game slug from openmods.
- [ ] `tags` has 1 to 5 tags from the fixed list, and at least one of them is not `adult`.
- [ ] A mod with adult content uses the `adult` tag.
- [ ] The `cover` file and the images in `openmods.md` exist at the given paths.
- [ ] `openmods.md` is at the root and is under 100 KB.
- [ ] (Recommended) `openmods.md` has a How to build section that matches the repository's build files, or says "Nothing to build".
- [ ] (Recommended) The cover and the screenshots are WebP or JPG, at most 1920 x 1080 and under about 500 KB each.
- [ ] (Recommended) A GitHub release with the mod files exists.
- [ ] (Recommended) Its release notes say what changed, under `## Added`, `## Changed` and `## Fixed`.

## 6. List the mod

A person signs in on openmods with GitHub, opens the game page, clicks "Add mod" and pastes the repository link. openmods checks everything above and shows a preview first.

To change the listing later, change `openmods.json` or `openmods.md`. openmods refreshes its copy regularly, usually within half an hour. To remove the mod from openmods, delete both files.
