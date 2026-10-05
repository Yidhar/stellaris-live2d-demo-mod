# Asset notice / 资源说明

This demo mod includes third-party art. This file says where it comes from, whose it is, what was changed, and how to get it removed.
本演示 mod 附带了第三方美术资源。本文件说明它们的来源、归属、做过的改动，以及如何联系下架。

## Original work / 原作品

**Girls' Frontline (少女前线)**, a mobile game. The characters, their art and their Live2D models are the work of the game's developer and
publishers (for the Chinese version MICA Team / 云母组 and Sunborn / 散爆网络, and the publishers of the other regional versions).
This project is a fan-made technical demo. It is **not affiliated with, endorsed by or connected to** the rights holders.

**《少女前线》**（手游）。角色、立绘和 Live2D 模型的著作权归游戏的开发商和发行商所有（国服为云母组 MICA Team、散爆网络 Sunborn，其他地区版本为各自的发行商）。
本项目是爱好者制作的技术演示，**与权利方没有任何隶属、授权或合作关系**。

## What is included / 包含的资源

Nine Live2D models of T-Dolls (the game's characters), under `gfx/live2d/`. The ids are those of the community collection named below.
`gfx/live2d/` 下的九个战术人形 Live2D 模型。编号取自下面所说的社区合集。

| Folder / 文件夹 | Character / 角色 | Archive id / 合集编号 |
|---|---|---|
| `model_01` | OTs-14 | `d119_s3001` |
| `model_02` | 64 Shiki (64式) | `d243_s2901` |
| `model_03` | Lewis | `d253_s6901` |
| `model_04` | QBU-88 | `d261_s3801` |
| `model_05` | ZB-26 | `d307_s4703` |
| `model_06` | General Liu | `d316_s11603` |
| `model_07` | M26-MASS | `d351_s9001` |
| `model_08` | Type 88 (88式) | `d95_s50001` |
| `model_09` | PA-15 | `pa15_5802` |

(`d<number>` is the character's number in the archive, `s<number>` the skin.)

## Source / 来源

Taken from the community collection **gfl-archive**, <https://github.com/steve1316/gfl-archive>, which in turn holds resources extracted from the
game. This project did not create, draw or rig any of them.
取自社区合集 **gfl-archive**（<https://github.com/steve1316/gfl-archive>），其内容来自游戏客户端资源。本项目没有创作、绘制或绑定其中任何一个。

## What was changed / 做过的改动

- The textures were re-encoded from PNG to DXT5 (`.dds`, with `l2d_pack` of stellaris-live2d), the format of the game's own textures.
- One expression file, `expressions/smile.exp3.json`, was added to each model (and listed in its `model3.json`).
- The folders were renamed (`model_01` ...).

Nothing else was changed: the `moc3` files, the motions, the physics files and the model files are as published.
贴图从 PNG 重新编码为 DXT5；每个模型加了一个表情文件 `smile.exp3.json`；文件夹改了名。除此之外没有改动：`moc3`、动作、物理和模型文件与公开的一致。

## License and use / 许可和使用

These models are **not** covered by this repository's MIT license; all rights remain with their owners. They are included only as test and
demonstration material for the [stellaris-live2d](https://github.com/Yidhar/stellaris-live2d) plugin, for non-commercial use. Do not use them
commercially, do not claim them as your own, and respect the owners' policies on fan works. If you want to use the models for anything else, get
them from, and ask, the rights holders.
这些模型**不**适用本仓库的 MIT 许可证，权利仍归所有者。它们只作为 [stellaris-live2d](https://github.com/Yidhar/stellaris-live2d) 插件的测试和演示素材，仅限非商业用途。请勿商用，请勿冒称自己的作品，并遵守权利方对二次创作的相关规定。要把这些模型用于别的用途，请向权利方获取并征得同意。

## Takedown / 下架联系

If you are a rights holder (or act for one) and want any of this removed, or want the credit changed, open an issue at
<https://github.com/Yidhar/stellaris-live2d-demo-mod/issues> (or contact the owner through <https://github.com/Yidhar>). The files will be
removed promptly, no questions asked.
如果你是权利方（或其代理人），希望移除其中任何内容或更改署名，请在 <https://github.com/Yidhar/stellaris-live2d-demo-mod/issues> 提 issue（或通过 <https://github.com/Yidhar> 联系所有者）。相关文件会立即移除，无需任何理由。

## Voice lines / 语音

`sound/demo/line1..3.wav` are three short Chinese lines made for this demo with the Windows speech synthesizer; they are not taken from the game.
`sound/demo/line1..3.wav` 是为本演示用 Windows 语音合成器生成的三句简短中文，不是游戏里的语音。
