# stellaris-live2d 演示 mod

[English](README.md) | [简体中文](README.zh-CN.md)

[stellaris-live2d](https://github.com/Yidhar/stellaris-live2d)（把 Live2D 模型画进 Stellaris 4.5.1 肖像的插件）的演示用**肖像组 mod**。它给人类十个 Live2D 肖像，**自带插件开发和测试时用的九个模型和它们的动作组**，并用两个小文本文件演示一个 mod 怎样：

- 照常注册肖像（原版条目的副本，所以**没有**插件的游戏显示的是普通人类），
- 用游戏自己的 `portrait_groups` 语法决定领袖、统治者、人口和物种各用其中哪些，
- 声明哪些是 Live2D、用哪个模型、什么取景、什么事件、语音和表情，
- 并且也覆盖原版肖像键，用于脚本或帝国设计器直接按名字指定了肖像的领袖。

## 里面有什么

| 文件 | 谁读 | 作用 |
|---|---|---|
| `gfx/portraits/portraits/zz_live2d_humans.txt` | 游戏 | 十个肖像 `l2d_human_female_01..05`、`l2d_human_male_01..05`（原版 `human_*` 的副本），以及 `human` 肖像组：领袖、统治者和 `game_setup` 选 `01..03`，人口选 `04..05`，物种选五个中的任意一个 |
| `gfx/portraits/live2d/00_live2d_humans.txt` | 插件 | 哪些肖像是 Live2D 以及怎么画：模型、取景（`live2d_view`）、`live2d_scale`、`live2d_unmirror`，以及 `live2d_actions`（鼠标跟随、点击、点击头部、悬停、出现、待机、问候），含表情和语音 |
| `gfx/live2d/model_01..09/` | 插件 | 九个模型：`model.model3.json`、`moc3`、DXT5 贴图（`.dds`）、物理、模型自己的动作组（`login`、`touch_*`、`wait_*`、`Idle` 等），以及为悬停和点击动作加的表情 `smile` |
| `sound/demo/line1..3.wav` | 插件 | 三句简短的语音（中文，用 Windows 语音合成器生成） |
| `descriptor.mod` | 游戏 | mod 的名字和版本 |
| `ASSETS.md` | 人 | 资源说明：原作品、来源、归属、改动和下架联系方式 |

文本文件里值得看的地方：

- **先 `set`，再 `add`。** 在多个文件里定义的肖像组会被*合并*，只写 `add` 的 mod 会让原版肖像留在池子里。这里每个作用域的第一条是 `set`，它丢掉原版列出的肖像。
- **原版键也绑定了**（`human_female_05` 和 `l2d_human_female_05` 用同一个模型）：按名字直接指定肖像的领袖（比如开局设计帝国时选的统治者）不是从组里抽的。
- **`appear = { motion_group = "login" }`** 按作者做的样子播每个模型自己的入场动画。这批模型里很多带有逐渐散去的黑幕和镜头运动，开头几秒会在肖像里显示出来。不想要的话，把对应参数列进 `live2d_ignore_parameters`（插件仓库的 `tools/motion_diff.py` 能为某个模型找出它们；插件仓库的 `make_human_mod.py --ignore-stage` 可以看到效果）。
- `l2d_human_female_01` 给三个点击动作各绑了一句语音（`voices`）；其它肖像轮流说其中任意一句（`sounds`）。`l2d_human_female_04` 放大 30%（`live2d_scale`）；`model_05` 的取景是手工指定的（`live2d_view = { x y height }`）。

模型和用它们的肖像：

| `gfx/live2d/` 下的文件夹 | 肖像（`l2d_` 的和原版键都一样） |
|---|---|
| `model_01` | `human_female_04` |
| `model_02` | `human_female_02`、`human_male_05` |
| `model_03` | `human_male_02` |
| `model_04` | `human_female_03` |
| `model_05` | `human_male_01`（取景手工指定） |
| `model_06` | `human_male_04` |
| `model_07` | `human_male_03` |
| `model_08` | `human_female_05` |
| `model_09` | `human_female_01` |

## 使用

1. 安装插件：解压 [stellaris-live2d 的 releases](https://github.com/Yidhar/stellaris-live2d/releases) 里的 zip，在里面运行 `python scripts\deploy.py`（它也会装上 Cubism Core 并写好插件的 ini，不需要再做别的）。
2. 把这个文件夹放进 `Documents\Paradox Interactive\Stellaris\mod\`，在启动器或播放集里启用（或者按游戏的 mod 格式，在文件夹旁边写一个 `live2d_humans.mod`，内容是 `descriptor.mod` 加一行 `path="..."`）。
3. 开一局有人类的新游戏（或读档：领袖和人口在创建或显示时从组里挑肖像），打开有肖像的界面（议政厅、领袖列表、星球的人口）；没有显示的话看 `stellaris.exe` 旁边的 `stellaris_live2d.log`。日志会写出它遇到的每个肖像键拿到了哪个模型、是为什么作用域挑的（`leader #117 of human`）。

想用自己的模型：把它们放进 `gfx/live2d/` 下别的文件夹，让 `00_live2d_humans.txt` 里某个肖像的 `live2d_model` 指向它们（`live2d_view` 取景；插件的 `l2d_pack` 把 PNG 贴图转成 DXT5）。任何 Cubism 4 模型都行；缺少这些动作组或 `smile` 表情的模型就播它有的。

## 署名和许可证

文本文件（`gfx/live2d/` 和 `sound/` 之外的所有内容）是 MIT，见 [LICENSE](LICENSE)。`zz_live2d_humans.txt` 里的十个肖像条目是 Stellaris 自己的 `human_*` 条目换了名字的副本（它们指向游戏的资源），仍属 Paradox Interactive。

**九个模型不是 MIT，也不是我们的。** 它们是游戏《少女前线》的角色美术资源，取自社区合集 [gfl-archive](https://github.com/steve1316/gfl-archive)，只作为这个演示的测试素材放在这里，仅限非商业用途。所有权利属于它们的所有者。**[ASSETS.md](ASSETS.md)（中英文）写明了原作品、来源、归属、改动和下架联系方式**；如果你是权利方并希望移除，请开一个 issue，会立即移除。语音是为这个演示用 Windows 语音合成器生成的。
