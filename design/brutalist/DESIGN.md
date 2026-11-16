# DESIGN.md — Neubrutalism / 新粗野主义

> 版本 1.0 · 2026-11
> 适用：活动页、独立品牌、产品发布、有个性的作品集、移动端 H5
> 字体：Archivo Black（标题）/ Inter（正文）/ Instrument Serif（可选旁白）
> 使用方式：先读 §2「Hard rules」，按 §3–§9 实现，交付前逐条过 §13。
> 视觉基准：`../../style-probe.html#s3`

---

## 1. 定位

把界面的“构造”暴露出来：3px 黑边、硬阴影、大字、贴纸和跑马灯。信息直给，态度优先，但必须可读、可点、可维护。

- **它相信**：界面可以吵闹，只要层级清楚；装饰本身就是内容的一部分。
- **它拒绝**：软阴影、玻璃、圆角、渐变、克制的“性冷淡”模板。

| 适合 | 不适合 |
|---|---|
| 活动 / 发布 / 快闪页 | 银行、医疗、政务 |
| 独立品牌、创意工作室 | 高密度后台 |
| 有个性的作品集 | 需要安静阅读的长文 |
| 潮流 / 音乐 / 青年文化 | 面向老年人的产品 |
| H5 传播页 | 严肃的 B2B 采购流程 |

**一句话给 AI**：Neubrutalism — cream canvas, 3px black borders, hard offset shadows, oversized Archivo Black type, two loud accents, sticker rotation, marquee, zero radius.

---

## 2. Hard rules（不可协商）

1. 边框 `3px solid var(--ink)`；阴影只允许 `Npx Npx 0 var(--ink)`（**0 blur**），N 取 4 / 6 / 8。
2. 圆角 `0`。
3. 一页最多 **2** 个高饱和色（从蓝 / 黄 / 粉里选）+ 米色底 + 墨色。
4. 大标题用 Archivo Black（英文）；中文用 PingFang SC **900**，且只在 ≥40px 时允许（小字号用 600，避免合成加粗发糊）。
5. 正文用 Inter 400/500；标签用 Inter 700 全大写 `+0.12em`。
6. 旋转只用于贴纸 / 海报：`-6°` ~ `9°`，每屏 ≤ 3 个。
7. 禁止：渐变、玻璃、发光、软阴影（blur > 0）、emoji 图标。
8. hover：位移 `-2px, -2px` 且阴影 `+2px`；active：位移 `+2px, +2px`；不允许缩放。
9. 跑马灯 `aria-hidden="true"`；`prefers-reduced-motion` 下停止。
10. 对比度：米底黑字 ≥15:1；蓝底白字 5.8:1 可用；**粉底只能用黑字**（白字仅 2.9:1）。

冲突时优先级：**可访问性 > 品牌与内容 > 本文件 > 个人偏好**。

---

## 3. 色彩

### Light（默认）

| Token | 值 | 用途 |
|---|---|---|
| `--cream` | `#FFF6DF` | 页面底色，占 ~70% |
| `--ink` | `#0A0A0A` | 文字、边框、阴影 |
| `--card` | `#FFFFFF` | 卡片、输入框 |
| `--blue` | `#2B4BFF` | 海报、主 CTA（二选一） |
| `--yellow` | `#FFD84D` | 高亮块、跑马灯、CTA |
| `--pink` | `#FF5CA8` | 贴纸、标签（少量） |

### Dark

| Token | 值 |
|---|---|
| `--cream` | `#0B0B0B` |
| `--ink` | `#FFF6DF` |
| `--card` | `#161616` |
| `--blue` | `#5C78FF` |
| `--yellow` | `#FFE066` |
| `--pink` | `#FF7CBC` |

深色模式里硬阴影会变成“米色偏移块”，这是这套风格的特征，保留它。

### 用量

- 70% 米色
- 20% 墨色（文字 / 边框 / 阴影）
- 10% 强调色，一屏不超过两块

### 对比度（实测）

| 组合 | 比值 | 可用性 |
|---|---|---|
| `#0A0A0A` / `#FFF6DF` | 18.3:1 | 正文、标题 |
| `#FFFFFF` / `#2B4BFF` | 5.8:1 | 正文、按钮均可用 |
| `#0A0A0A` / `#FFD84D` | 14.4:1 | 正文、按钮 |
| `#0A0A0A` / `#FF5CA8` | 7.3:1 | 贴纸、标签 |
| `#FFFFFF` / `#FF5CA8` | 2.9:1 | **禁用** |

### 规则

- 黄底黑字是默认组合；蓝底用白字；粉底永远配黑字。
- 不要三个强调色同时大面积出现；选两个，第三个只做 1–2 个小元素。
- 深色模式下保留 3px 边框和硬阴影，不要换成发光。

---

## 4. 字体

### 角色

| 角色 | 字体 | 字重 | 说明 |
|---|---|---|---|
| Display | Archivo Black | 400（唯一字重） | 英文标题、数字；中文回退 PingFang SC 900 |
| Body | Inter | 400 / 500 | 正文、说明 |
| Label | Inter | 700 | 10–11px 全大写 `+0.12em` |
| Accent | Instrument Serif | 400 italic | 可选，每页 ≤1 处，做一句“旁白” |
| Mono | 不用 | — | 标签用 Inter 700 + 等宽数字即可 |

`Archivo Black` 只有 400 一个字重，不要写 `font-weight: 700` 去“加粗”它。

### 字阶

| Token | size / line-height / tracking | 用途 |
|---|---|---|
| `display` | `clamp(48px, 7.6vw, 104px)` / 1.02 / `-0.03em` | 首屏 H1，最多 2 行 |
| `h2` | `clamp(32px, 5vw, 56px)` / 1.05 / `-0.02em` | 区块标题 |
| `h3` | `20px` / 1.2 / `0` | 卡片标题 |
| `body` | `16px` / 1.6 / `0` | 正文 |
| `small` | `13px` / 1.5 / `0` | 说明 |
| `label` | `10px` / 1 / `+0.12em`，大写 | 编号、标签、跑马灯 |
| `sticker` | `10px` / 1 / `+0.1em`，大写 | 贴纸 |

中文正文行长 **26–32 字**；英文 55–70 字符。

### 中文规则

- 中文 **不能** 用 Archivo Black；用 `PingFang SC` 900（或思源黑体 Heavy）。
- 合成加粗只在 ≥40px 使用；正文和标签用 600。
- 中文不做 `text-transform: uppercase`（无效且会让字距错乱）。
- 中文标题字距 `-0.02em`；正文 0。
- 混排时英文用 Archivo，中文用 PingFang，行高按较大字号对齐。

---

## 5. 布局

### 网格

- 12 栏，gutter `16px`，max-width `1440px`
- 页边距：≥1080px 用 `56px`；760–1080 用 `24px`；<760 用 `18px`
- 允许破格：海报 / 跑马灯可超出内容区，但不得造成横向滚动

### 间距

`4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 80 / 120`

- 区块上下：64–96
- 标题 → 正文：16–20
- 卡片内：20–24
- 元素之间优先用 16，不要到处 12

### 形状

- radius 0
- border `3px var(--ink)`
- 阴影 `6px 6px 0 var(--ink)`；小元素 `4px`，海报 `8px`
- 允许：旋转贴纸、粗线分隔、跑马灯、halftone 点阵

### 响应式

| 断点 | 行为 |
|---|---|
| ≥1080 | 12 栏；H1 与海报并排 |
| 760–1079 | H1 占满；海报下移或隐藏 |
| <760 | 单栏；导航只留 logo + CTA；卡片堆叠；跑马灯保留 |
| <460 | 边框仍 3px；阴影降到 4px；H1 最小 40px |

移动端：不要为了塞内容把正文降到 12px；按钮不小于 44px。

---

## 6. 组件

### 导航

- 高 72px，底部 3px 墨线
- 左 logo：墨色块 + 黄字，padding `6px 10px`
- 链接：11px / 700 / 全大写，hover 加 2px 下划线
- CTA：黄底、3px 边、5px 硬阴影

```html
<header class="flex h-[72px] items-center justify-between border-b-[3px] border-ink">
  <a href="/" class="bg-ink px-2.5 py-1.5 font-display text-[15px] text-yellow">NULL*</a>
  <nav class="hidden gap-5 text-[11px] font-bold uppercase tracking-[0.08em] md:flex">
    <a href="#work" class="border-b-2 border-transparent hover:border-ink">Work</a>
    <a href="#about" class="border-b-2 border-transparent hover:border-ink">About</a>
    <a href="#contact" class="border-b-2 border-transparent hover:border-ink">Contact</a>
  </nav>
  <a href="#contact"
     class="inline-flex h-11 items-center border-[3px] border-ink bg-yellow px-5 text-[13px] font-bold
            shadow-hard-sm transition-transform duration-150
            hover:-translate-x-0.5 hover:-translate-y-0.5 hover:shadow-hard
            active:translate-x-0.5 active:translate-y-0.5 active:shadow-none">
    开始项目
  </a>
</header>
```

### 按钮

- 高 44–52；padding `0 20px`；3px 边；radius 0
- Primary：黄底黑字；Secondary：蓝底白字
- hover：`translate(-2px,-2px)` + 阴影 `5→7`
- active：`translate(2px,2px)` + 阴影归零
- 禁止：圆角、渐变、软阴影、缩放

### 跑马灯

- 黑底黄字，上下 3px 墨线，整体 `rotate(-1.1deg)`，宽度 102% 防露边
- 内容重复两份，`translateX(-50%)`，26s linear infinite
- `aria-hidden="true"`；reduced-motion 下静止

```html
<div class="relative -mx-6 rotate-[-1.1deg] overflow-hidden border-y-[3px] border-ink bg-ink text-yellow">
  <div class="flex w-max animate-marquee motion-reduce:animate-none">
    <span class="whitespace-nowrap py-3 pr-8 text-[13px] font-bold uppercase tracking-[0.16em]">
      品牌设计 ✱ 界面设计 ✱ 动效 ✱ 不做无聊的页面 ✱
    </span>
    <span aria-hidden="true" class="whitespace-nowrap py-3 pr-8 text-[13px] font-bold uppercase tracking-[0.16em]">
      品牌设计 ✱ 界面设计 ✱ 动效 ✱ 不做无聊的页面 ✱
    </span>
  </div>
</div>
```

### 卡片

- 白底、3px 边、6px 阴影、padding 20–24
- hover：位移 -2px / 阴影 8px；不要放大

```html
<article class="border-[3px] border-ink bg-card p-5 shadow-hard
                transition-transform duration-150
                hover:-translate-x-0.5 hover:-translate-y-0.5">
  <b class="text-[10px] font-bold uppercase tracking-[0.12em] text-ink/60">01 / Brand</b>
  <h3 class="mt-3 text-lg font-bold">品牌</h3>
  <p class="mt-1.5 text-[13px] leading-relaxed">命名、标识、视觉系统</p>
</article>
```

### 贴纸

- 粉底黑字、3px 边、4px 阴影、`rotate(9deg)`
- 10px / 700 / 大写；每屏 ≤3 个；不要每个卡片都转

### 海报块

- 蓝底白字、3px 边、8px 阴影、`rotate(4deg)`
- 大数字用 Archivo Black 64–96px；底部两行 10px 标签
- 移动端隐藏，不要缩到看不清

### 表单

- 输入 48px 高，3px 边，白底；focus 2px 墨色 outline + offset 2
- 错误：红条 + 文字；不能只靠颜色
- 标签 10px 700 大写

### 标签 / Tag

- 2px 边框，10px 700 大写，padding `3px 8px`，无圆角

---

## 7. 动效

| Token | 值 |
|---|---|
| `--dur-fast` | `120ms` |
| `--dur` | `180ms` |
| `--dur-slow` | `320ms` |
| `--ease` | `cubic-bezier(.2,.9,.25,1)` |
| `--marquee` | `26s` linear infinite |

### 戏剧化在哪

1. **跑马灯**：持续横移，是页面的“节拍器”。
2. **贴纸入场**：从 `rotate(0)` 到目标角度，一次，不循环。
3. **硬位移 hover**：按钮和卡片像被按下去。
4. **一处横向滚动画廊**：滚动锁定 + 横移（只允许一次，必须提供键盘/按钮替代）。
5. **标题高亮块**：进入视口时从左向右展开（scaleX）。

### 禁止

- 视差、鼠标跟随、循环缩放、超过一次的弹跳、软缓动。
- 跑马灯上放链接或重要信息。

### 降级

`prefers-reduced-motion: reduce` → 跑马灯静止、贴纸不旋转、位移取消、高亮块直接显示。

---

## 8. 图像与图标

- 图标：2.5–3px 描边、粗黑、方形端点；只用一种风格
- 图片：高对比；可做蓝 / 粉 duotone；加 3px 边框 + 6px 阴影
- 允许 halftone 点阵、粗网点、黑白扫描质感
- 禁止：3D 渲染、玻璃、发光、emoji、细线极简图标

---

## 9. 文案

- 直白、短、有态度；允许说“不”。
- 标题 4–10 字；可以用口语，但不要脏话。
- 英文标签全大写，2–3 个词。

| 好 | 差 |
|---|---|
| 不做无聊的页面。 | 我们致力于打造卓越的用户体验。 |
| 想法要落地，不要落灰。 | 以创新为引擎，驱动品牌价值升级。 |
| 先做对，再做响。 | 全方位赋能，构建增长闭环。 |

---

## 10. Do / Don't

| Do | Don't |
|---|---|
| 3px 边 + 6px 硬阴影 | 12px 圆角 + 软阴影 |
| 米色底 + 两色 | 四个高饱和色同时出现 |
| Archivo 大字 | 正文也用 Archivo |
| 贴纸 1–3 个 | 每个卡片都旋转 |
| hover 硬位移 | hover 放大 1.05 |
| 跑马灯一条 | 三条跑马灯抢注意力 |
| 中文 900 只用于大字 | 14px 中文也合成加粗 |
| 白字只放蓝底 | 白字放粉底 |

---

## 11. Tailwind v4

```css
@import "tailwindcss";

:root {
  --cream: #FFF6DF;
  --ink: #0A0A0A;
  --card: #FFFFFF;
  --blue: #2B4BFF;
  --yellow: #FFD84D;
  --pink: #FF5CA8;
}

[data-theme="dark"] {
  --cream: #0B0B0B;
  --ink: #FFF6DF;
  --card: #161616;
  --blue: #5C78FF;
  --yellow: #FFE066;
  --pink: #FF7CBC;
}

@theme inline {
  --color-cream: var(--cream);
  --color-ink: var(--ink);
  --color-card: var(--card);
  --color-blue: var(--blue);
  --color-yellow: var(--yellow);
  --color-pink: var(--pink);

  --font-display: "Archivo Black", "PingFang SC", "Hiragino Sans GB", sans-serif;
  --font-sans: "Inter", "PingFang SC", "Hiragino Sans GB", sans-serif;
  --font-serif: "Instrument Serif", "Songti SC", serif;

  --text-display: clamp(3rem, 7.6vw, 6.5rem);
  --text-display--line-height: 1.02;
  --text-display--letter-spacing: -0.03em;

  --shadow-hard-sm: 4px 4px 0 var(--ink);
  --shadow-hard: 6px 6px 0 var(--ink);
  --shadow-hard-lg: 8px 8px 0 var(--ink);

  --animate-marquee: marquee 26s linear infinite;
}

@keyframes marquee {
  to { transform: translateX(-50%); }
}
```

`shadow-hard` / `shadow-hard-lg` 会直接生成同名工具类；`animate-marquee` 对应 `animate-marquee`。

Tailwind v3：把颜色、字体、阴影放进 `theme.extend`，`keyframes` + `animation` 放进 `extend`。

---

## 12. 给 AI 的 prompt（可直接粘贴）

```
Build a neubrutalist [page type] for [audience].
Read DESIGN.md and treat it as a hard constraint.

Non-negotiables:
- Cream #FFF6DF canvas, ink #0A0A0A, 3px solid borders, 0 radius,
  hard shadows only (6px 6px 0 ink, 0 blur).
- At most two loud accents from blue #2B4BFF / yellow #FFD84D / pink #FF5CA8.
- Type: Archivo Black for display, Inter for body, Inter 700 uppercase for labels.
  Chinese display uses PingFang SC 900 only at ≥40px.
- Rotation only on stickers/posters (-6° to 9°), max 3 per screen.
- One marquee band, aria-hidden, stopped under prefers-reduced-motion.
- Hover: translate(-2px,-2px) + shadow grows; active: translate(2px,2px). No scaling.
- No gradients, glass, glow, soft shadows, emoji, or rounded corners.
- Mobile: single column ≤760px, 44px targets, no horizontal scroll.

Output semantic HTML + Tailwind v4, mobile-first, with visible focus states.
```

---

## 13. 验收清单

- [ ] 所有边框 3px，所有阴影 0 blur
- [ ] 圆角全部 0
- [ ] 强调色 ≤2 种，且没有白字放粉底
- [ ] 中文 900 只出现在 ≥40px 的标题
- [ ] 贴纸 ≤3 个，旋转角度在 -6°~9°
- [ ] 跑马灯 aria-hidden，reduced-motion 下停止
- [ ] hover / active 位移与阴影联动，无缩放
- [ ] 焦点环可见，键盘可完成主流程
- [ ] 触控目标 ≥44px
- [ ] 760px 下无横向滚动，跑马灯不撑破页面
- [ ] 正文对比度 ≥4.5:1（暗色模式单独测）
- [ ] 没有渐变 / 玻璃 / emoji / 软阴影

---

变更记录：v1.0 — 初版，基于 style-probe S3。
