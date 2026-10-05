# stellaris-live2d demo mod

[English](README.md) | [简体中文](README.zh-CN.md)

A demo **portrait-group mod** for [stellaris-live2d](https://github.com/Yidhar/stellaris-live2d), the plugin that draws Live2D models
into Stellaris 4.5.1's portraits. It gives the humans ten Live2D portraits and shows, in two small text files, how a mod

- registers portraits the usual way (copies of vanilla entries, so a game **without** the plugin shows ordinary humans),
- chooses which of them leaders, rulers, pops and species get, with the game's own `portrait_groups` syntax,
- says which of them are Live2D, with which model, framing, events, voice lines and expression,
- and covers the vanilla portrait keys too, for leaders a script or the empire designer gave a portrait by name.

**This repository contains no models and no sound.** The models the mod was made with are other people's art, so they cannot be
published here: bring your own (below). Without them the plugin logs that a model is missing and the game draws the ordinary portraits.

## What is in it

| File | Read by | What it does |
|---|---|---|
| `gfx/portraits/portraits/zz_live2d_humans.txt` | the game | ten portraits `l2d_human_female_01..05`, `l2d_human_male_01..05` (copies of the vanilla `human_*` ones), and the `human` portrait group: leaders, rulers and `game_setup` pick `01..03`, pops pick `04..05`, species any of the five |
| `gfx/portraits/live2d/00_live2d_humans.txt` | the plugin | which portraits are Live2D and how: model, framing (`live2d_view`), `live2d_scale`, `live2d_unmirror`, `live2d_ignore_parameters`, and `live2d_actions` (mouse follow, click, click on the head, hover, appear, idle, greeting) with expressions and voice lines |
| `descriptor.mod` | the game | the mod's name and version |

Things worth reading in them:

- **`set`, then `add`.** A portrait group defined in several files is *merged*, so a mod that only `add`s leaves vanilla's portraits in
  the pool. The first entry of each scope here is a `set`, which drops what vanilla listed.
- **The vanilla keys are bound too** (`human_female_05` has the same model as `l2d_human_female_05`): a leader whose portrait was named
  outright, such as the ruler an empire was designed with, is not drawn from a group.
- **`appear = { motion_group = "login" }`** plays each model's own entrance as its author made it. For many of these models that
  includes a black curtain that fades away and a camera move, which show in the portrait for the first seconds. A mod that does not want
  them lists the parameters in `live2d_ignore_parameters` (`tools/motion_diff.py` of the plugin repository finds them for a model; the
  plugin repository's `make_human_mod.py --ignore-stage` shows the result).
- `l2d_human_female_01` binds a voice line to each of three touch motions (`voices`); the others say any of the lines in turn (`sounds`).
  `l2d_human_female_04` is magnified by 30 percent (`live2d_scale`); `model_05` has a hand-made framing (`live2d_view = { x y height }`).

## Using it

1. Install the plugin ([stellaris-live2d](https://github.com/Yidhar/stellaris-live2d): build it, `python scripts\deploy.py`, point
   `stellaris_live2d.ini` at a Cubism Core library).
2. Put this folder in `Documents\Paradox Interactive\Stellaris\mod\` and enable it in the launcher or the playset
   (or copy `descriptor.mod` to `live2d_humans.mod` next to the folder with a `path="..."` line, the way the game's mod format wants).
3. Add models. Each portrait looks for its model in the mod folder; the nine folders are listed here with the portraits that use them:

   | Folder under `gfx/live2d/` | Portraits (`l2d_` ones and the vanilla keys alike) |
   |---|---|
   | `model_01` | `human_female_04` |
   | `model_02` | `human_female_02`, `human_male_05` |
   | `model_03` | `human_male_02` |
   | `model_04` | `human_female_03` |
   | `model_05` | `human_male_01` (framing set by hand) |
   | `model_06` | `human_male_04` |
   | `model_07` | `human_male_03` |
   | `model_08` | `human_female_05` |
   | `model_09` | `human_female_01` |

   A folder holds `model.model3.json`, the `moc3`, textures (PNG, or DXT5 DDS made with the plugin's `l2d_pack`), the physics and motion
   files; the motion groups the file asks for are `login`, `touch_*`, `wait_*` (a model without them just plays what it has), and an
   expression named `smile` is used by the hover and click actions (`gfx/live2d/<model>/expressions/smile.exp3.json`, listed in the
   `Expressions` of `model3.json`; without it those actions skip the expression). Any Cubism 4 model works: edit `live2d_model`
   in `00_live2d_humans.txt` to point a portrait at another folder, and `live2d_view` to frame it.
4. Optional voice lines: three WAV, MP3, FLAC or OGG files `sound/demo/line1.wav`, `line2.wav`, `line3.wav` in the mod folder.
5. Start a game with the humans (or load a save: leaders and pops pick their portraits from the group when they are created or shown),
   open a screen with portraits, and look at `stellaris_live2d.log` next to `stellaris.exe` if nothing shows. The log names, for each
   portrait key it meets, the model it got and the scope it was picked for (`leader #117 of human`).

## License

MIT for what is written here (see [LICENSE](LICENSE)). The ten portrait entries in `zz_live2d_humans.txt` are copies of Stellaris's own
`human_*` entries under new names (they point at the game's assets) and remain Paradox Interactive's. Models, if you add any, carry their
authors' licenses.
