# DESIGN 文档库

五份可直接喂给 AI 的前端设计规范。前两份来自 `style-probe.html`，后三份来自 `style-probe-2.html`。

> 第一次用？先读 **[HOW-TO-USE.md](HOW-TO-USE.md)**：工具接法、分阶段 prompt、纠正话术、验收步骤。

| 文档 | 风格 | 一句话 | 适合 |
|---|---|---|---|
| [`swiss/DESIGN.md`](swiss/DESIGN.md) | 极简瑞士 | 网格、留白、一个字重体系，只留一个暖红当事件 | 作品集、品牌官网、编辑型落地页、H5 |
| [`brutalist/DESIGN.md`](brutalist/DESIGN.md) | 新粗野主义 | 3px 黑边、硬阴影、大字、贴纸与跑马灯 | 活动页、独立品牌、产品发布 |
| [`neoclassic/DESIGN.md`](neoclassic/DESIGN.md) | 新古典主义 | 对称、双线框、Cormorant 高对比衬线、印章 | 作品集、文化机构、展览 / 邀请页 |
| [`glitch/DESIGN.md`](glitch/DESIGN.md) | 故障艺术 | RGB 分离、坏帧色带、时间码、ticker | 音乐 / 游戏 / 开发者活动、实验影像 |
| [`collage/DESIGN.md`](collage/DESIGN.md) | 拼贴艺术 | 碎纸标题、胶带、halftone 照片、印章 | 独立品牌、杂志、文化项目 |

## 选哪个

| 你想要 | 选 |
|---|---|
| 专业、克制、贵 | Swiss |
| 有态度、记得住、像海报 | Brutalist |
| 庄重、有文化感、像展览邀请 | Neoclassic |
| 技术、失真、夜间活动 | Glitch |
| 手作、有人味、像独立杂志 | Collage |

## 怎么用

1. 把对应目录里的 `DESIGN.md` 放进项目根目录（或作为附件贴给 AI）。
2. 用这个模板提需求：

```
先读 DESIGN.md，把它当作硬约束，不要自由发挥。
任务：做一个 [页面类型]，面向 [人群]，需要 [模块 1/2/3]。
技术栈：Next.js + Tailwind v4，移动端优先。
交付：语义化 HTML + Tailwind 类名，包含 hover / focus / disabled 状态。
最后按 DESIGN.md 的「验收清单」逐条自查，并列出未通过项。
```

3. 让 AI 先输出 token（颜色 / 字号 / 间距），确认后再写组件，能显著减少跑偏。
4. 交付前用清单过一遍；AI 最容易违反的是圆角、阴影、强调色数量和移动端字号。

**只选一份。** 如果确实要混，选一套做基底，另一套只借一个元素，且全站只出现一次（例如 Swiss 版面 + 一枚 Collage 印章）。

## 共同底座

- **正文都用 Inter**：切换风格时正文层不变，只换标题、形状与材质。
- **中文都回退 PingFang SC**；需要编辑感时回退 Songti SC。
- **都不用渐变与玻璃**：分别用留白、边框、纸感、信号色建立层次。
- **都要求** 44px 触控目标、可见焦点环、`prefers-reduced-motion` 降级、暗色模式单独测对比度。

## 字体

六款字体都来自 Google Fonts（SIL OFL），本地 latin 子集在 `../assets/fonts/`：

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link
  href="https://fonts.googleapis.com/css2?family=Archivo+Black&family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400&family=Inter:wght@400;500;600;700&family=Instrument+Serif:ital@0;1&family=JetBrains+Mono:wght@400;700&family=Space+Grotesk:wght@500;700&display=swap"
  rel="stylesheet">
```

| 字体 | Swiss | Brutalist | Neoclassic | Glitch | Collage |
|---|---|---|---|---|---|
| Inter | 全部 | 正文 / 标签 | 正文 | 正文 | 正文 |
| Instrument Serif | 一处点缀 | 可选旁白 | — | — | 旁白 |
| Archivo Black | — | 标题 / 数字 | — | — | 标题碎片 |
| Cormorant Garamond | — | — | 标题 / 小标 | — | — |
| Space Grotesk | — | — | — | 标题 | — |
| JetBrains Mono | 仅代码 | — | 标签 | 数据 / 标签 | 标签 |

## 不要混用

五套系统的“形状语言”互斥：Swiss 是 1px 线 + 无阴影，Brutalist 是 3px 边 + 硬阴影，Neoclassic 是双线框 + 对称，Glitch 是浅底 + 坏帧，Collage 是纸 + 撕边。同一页面里混用会立刻变成“没想清楚”。

## 维护

- 改风格只改文档里的 token 表，不要改组件规则。
- 新增组件时，先检查它是否违反「Hard rules」，再写样式。
- 每份文档版本号独立；改动较大时在文末记一行 changelog。
