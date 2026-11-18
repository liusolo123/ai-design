# 字体与许可

本目录的 woff2 是 Google Fonts 的 latin 子集，全部采用 **SIL Open Font License 1.1（OFL-1.1）**。

| 字体 | 文件 | 版权行 |
|---|---|---|
| Inter | `inter-400 / 500 / 600` | Copyright 2020 The Inter Project Authors |
| Space Grotesk | `space-grotesk-500 / 700` | Copyright 2020 The Space Grotesk Project Authors |
| JetBrains Mono | `jetbrains-mono-400 / 700` | Copyright 2020 The JetBrains Mono Project Authors |
| Instrument Serif | `instrument-serif-400` | Copyright 2022 The Instrument Serif Project Authors |
| Archivo Black | `archivo-black-400` | Copyright 2017 The Archivo Black Project Authors |
| Cormorant Garamond | `cormorant-garamond-400`（含 italic） | Copyright 2015 the Cormorant Project Authors |

完整许可证文本在同目录的 [`LICENSES/`](LICENSES/) 下，每个家族一份。

## 可以做什么

- 个人与商业项目免费使用，无需付费或申请；
- 网页、App、印刷品、视频、UI 中嵌入；
- 修改字形、子集化、重新打包；
- 随项目再分发。

## 条件

- **不能单独售卖字体文件本身**（作为产品的一部分售卖没问题）；
- 再分发字体文件时，必须随附 OFL 文本与版权行（本目录的 `LICENSES/` 就是为此准备）；
- 如果修改后使用了原字体声明过的 Reserved Font Name，需要改名。**这六个家族均未声明 RFN**，所以子集化后可以保留原名。

## 两个说明

1. **这些文件是 latin 子集**（只含拉丁字符），属于对原字体的修改；没有 RFN 限制，可以继续用原名。中文本来就不在这些文件里。
2. **中文不使用这些字体**：`PingFang SC`、`Songti SC`、`Hiragino Sans GB` 是 Apple 的系统字体，随操作系统授权，**不随本仓库分发，也不能自行打包再分发**。CSS 里写字体名做回退没有问题；如果要做跨平台一致的商业站点，改用 **Noto Sans SC / Noto Serif SC**（OFL，Google Fonts）或思源黑体 / 思源宋体（OFL），并注意中文字体文件较大、需要子集化。

## 页面上的署名

OFL 不要求在网页上显示署名，但要求随字体软件保留版权与许可证。建议在页脚或 `credits` 页面放一行：

> Typefaces: Inter, Space Grotesk, JetBrains Mono, Instrument Serif, Archivo Black, Cormorant Garamond — SIL OFL 1.1.

不是强制，但是好 practice；再分发文件时则是必须。
