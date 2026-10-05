# stellaris-live2d demo mod

[English](README.md) | [简体中文](README.zh-CN.md)

A demo **portrait-group mod** for [stellaris-live2d](https://github.com/Yidhar/stellaris-live2d), the plugin that draws Live2D models
into Stellaris 4.5.1's portraits. It gives the humans ten Live2D portraits, **carries the nine models and their motion groups** the plugin
was developed and tested with, and shows, in two small text files, how a mod

- registers portraits the usual way (copies of vanilla entries, so a game **without** the plugin shows ordinary humans),
- chooses which of them leaders, rulers, pops and species get, with the game's own `portrait_groups` syntax,
- says which of them are Live2D, with which model, framing, events, voice lines and expression,
- and covers the vanilla portrait keys too, for leaders a script or the empire designer gave a portrait by name.

## What is in it

| File | Read by | What it does |
|---|---|---|
| `gfx/portraits/portraits/zz_live2d_humans.txt` | the game | ten portraits `l2d_human_female_01..05`, `l2d_human_male_01..05` (copies of the vanilla `human_*` ones), and the `human` portrait group: leaders, rulers and `game_setup` pick `01..03`, pops pick `04..05`, species any of the five |
| `gfx/portraits/live2d/00_live2d_humans.txt` | the plugin | which portraits are Live2D and how: model, framing (`live2d_view`), `live2d_scale`, `live2d_unmirror`, and `live2d_actions` (mouse follow, click, click on the head, hover, appear, idle, greeting) with expressions and voice lines |
| `gfx/live2d/model_01..09/` | the plugin | the nine models: `model.model3.json`, the `moc3`, DXT5 textures (`.dds`), physics, the motion groups of the model (`login`, `touch_*`, `wait_*`, `Idle`, ...) and an expression `smile` added for the hover and click actions |
| `sound/demo/line1..3.wav` | the plugin | three short voice lines (Chinese, made with the Windows speech synthesizer) |
| `descriptor.mod` | the game | the mod's name and version |

Things worth reading in the text files:

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

The models and the portraits that use them:

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

## Using it

1. Install the plugin: unpack a zip from the [stellaris-live2d releases](https://github.com/Yidhar/stellaris-live2d/releases) and run
   `python scripts\deploy.py` in it (it also installs a Cubism Core and writes the plugin's ini, so nothing else is needed).
2. Put this folder in `Documents\Paradox Interactive\Stellaris\mod\` and enable it in the launcher or the playset
   (or copy `descriptor.mod` to `live2d_humans.mod` next to the folder with a `path="..."` line, the way the game's mod format wants).
3. Start a game with the humans (or load a save: leaders and pops pick their portraits from the group when they are created or shown),
   open a screen with portraits (the council, the leaders list, a planet's population), and look at `stellaris_live2d.log` next to
   `stellaris.exe` if nothing shows. The log names, for each portrait key it meets, the model it got and the scope it was picked for
   (`leader #117 of human`).

To use your own models, put them in other folders under `gfx/live2d/` and point `live2d_model` of a portrait in `00_live2d_humans.txt`
at them (`live2d_view` frames them; `l2d_pack` of the plugin converts PNG textures to DXT5). Any Cubism 4 model works; a model without the
motion groups or the `smile` expression just plays what it has.

## Credits and license

The text files (everything but `gfx/live2d/` and `sound/`) are MIT, see [LICENSE](LICENSE). The ten portrait entries in
`zz_live2d_humans.txt` are copies of Stellaris's own `human_*` entries under new names (they point at the game's assets) and remain
Paradox Interactive's.

**The nine models are not MIT and not ours.** They are character art from the game *Girls' Frontline* (少女前线), taken from the community
collection [gfl-archive](https://github.com/steve1316/gfl-archive), and are included only as test material for this demo, for non-commercial
use. All rights belong to their owners. **[ASSETS.md](ASSETS.md) (中英文) gives the original work, the source, whose they are, what was changed
and how to contact us to have them removed**; if you are a rights holder and want them gone, open an issue and they will be removed promptly.
The voice lines were made with the Windows speech synthesizer for this demo.
