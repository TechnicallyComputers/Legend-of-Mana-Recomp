# Legend of Mana  Recompiled

Static recompilation of **Legend of Mana** built on
[psxrecomp](https://github.com/mstan/psxrecomp) and
[recomp-ui](https://github.com/mstan/recomp-ui).

While incorporating action role-playing game elements from the three games which preceded it, Legend of Mana has its own distinct style of gameplay. Most notably, it gives the player the ability to shape the game's world of Fa'Diel according to his or her desires, a system which was incorporated through the use of "artifacts," which are gained as the player progresses through the game. The player uses the artifacts to create different towns, dungeons, etc., called "Lands", to venture to and explore. This creates a non-linear gameplay, since the game is driven by a series of what would be considered side-quests in other games. Legend of Mana features three different plots which can occur simultaneously, and which do not necessarily need to be completed for the player to finish the game. Legend of Mana was a financial success in Japan. While the game garnered considerable praise for its graphics and presentation, many critics and fans were turned off by the game's lack of a main storyline.

| | |
|---|---|
| Players | 2 |
| Region | USA |
| Publisher | Square Enix |
| Year | 1999 |

Scaffolded with the New Project Layout. See
`psxrecomp/docs/GAME_PROJECT_SETUP.md` for the full flow.

## Legal

You must own the original game. Disc images under `disc/` are gitignored and
must never be committed. Retail BIOS dumps are not redistributed; OpenBIOS is
used for Generate unless you supply your own SCPH locally.

Optional box art under `launcher_assets/img/` may come from
[libretro-thumbnails](https://github.com/libretro-thumbnails/libretro-thumbnails)
(`Named_Boxarts`); see `BOXART_SOURCE.txt` when present.

## Quick start (dev)

```bash
git submodule update --init --recursive
./psxrecomp/tools/ci/build_emitters.sh
python3 psxrecomp/psxrecomp_cli.py generate \
  --config game.toml --project-root . --disc disc/<your>.cue
cmake -S . -B build-release -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build-release --target psx-runtime
```

Zip prefix for CI artifacts: `legendofmana`.

## Symbols

Progressive map: `symbols.toml` → `python3 tools/sync_symbols.py` →
`psx_symbols.h` (`PSX_FN_*`). See `psxrecomp/docs/SYMBOLS.md`.

## Framework pins

Submodule gitlinks (`psxrecomp`, optional `recomp-ui`, nested `recomp-net`)
are authoritative. `framework_pins.txt` is an optional scaffold snapshot;
release CI logs SHAs with `record_pins.sh` but builds whatever the gitlinks
resolve to. Bump submodules deliberately — do not float on `main`/`master`
in release CI.
