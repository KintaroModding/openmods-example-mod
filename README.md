# openmods Example Mod

The reference repository for [openmods](https://openmods.nexus), a website that lists open-source game mods. It is not a real mod. It shows the two files that every mod on openmods needs:

- [`openmods.json`](openmods.json): data for the website (name, summary, games, tags, cover, and more).
- [`openmods.md`](openmods.md): the description that players read on the mod page.

## Use it with an AI agent

Give your agent this prompt in your mod repository:

> Make this repository ready for openmods. Follow https://github.com/KintaroModding/openmods-example-mod/blob/main/AGENTS.md

[`AGENTS.md`](AGENTS.md) has every rule an agent needs.

## Use it by hand

1. Copy `openmods.json` and `openmods.md` into the root of your mod repository.
2. Change the values to fit your mod. The rules are in [`AGENTS.md`](AGENTS.md).
3. Make sure your repository is public and has an open-source license.
4. Sign in on openmods, open your game's page, click "Add mod" and paste your repository link.

## License

MIT. See [`LICENSE`](LICENSE).
