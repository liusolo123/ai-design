# DESIGN.md — Collage Art / 拼贴艺术

> 版本 1.0 · 2026-11
> 适用：独立品牌、杂志 / 文化项目、展览、音乐与潮流活动、作品集、H5
> 字体：Archivo Black（标题碎片）/ Instrument Serif（旁白）/ Inter（正文）/ JetBrains Mono（标签）
> 使用方式：先读 §2「Hard rules」，按 §3–§9 实现，交付前逐条过 §13。
> 视觉基准：`../../style-probe-2.html#n4`

---

## 1. 定位

像做一张纸上的拼贴：剪下来的标题、贴歪的照片、胶带、印章、手写旁白。乱是表面的，底下必须有一张严格的网格；每一块“随手贴上去”的东西都要能对到网格线。

- **它相信**：层叠和材质能传递“人做的”温度；不完美比精确更有说服力。
- **它拒绝**：没有底网格的纯堆砌、渐变背景、玻璃拟态、3D 图标。

| 适合 | 不适合 |
|---|---|
| 独立品牌、创意工作室 | 银行、医疗、政务 |
| 杂志 / 文化项目 / 展览 | 高密度后台 |
| 音乐、潮流、青年文化 | 需要安静阅读的长文 |
| 有个性的作品集 | 严肃的 B2B 采购 |
| H5 传播页 | 儿童教育（易显杂乱） |

**一句话给 AI**：Editorial collage — aged paper canvas, torn-paper headline scraps in 3 colors, taped halftone photos with white borders, rubber stamp, mono labels, underlying 12-column grid.

---

## 2. Hard rules（不可协商）

1. 底层必须是 **12 栏网格 + 48px 切割垫网格**；所有元素对齐到网格，再谈旋转。
2. 每屏拼贴元素 ≤ **5** 个（照片 / 贴纸 / 印章 / 胶带 / 旁白各算一个；标签行算一组）。
3. 旋转范围 `-8°` ~ `9°`；同一元素只转一次，不要动态摇晃。
4. 撕纸边只用于标题碎片和照片边；按钮、表单、导航保持直边。
5. 一屏只有一个视觉焦点（标题）；照片不得比标题更抢眼。
6. 禁止：渐变背景、玻璃、发光、3D、emoji 图标、卷草花纹。
7. 照片：`6px` 白边 + `8–16px` 软阴影；这是全站**唯一**允许的软阴影。
8. 撕纸上的文字必须对比达标：白字只放红 / 蓝，黑字放纸色 / 黄。
9. 中文标题 PingFang SC **900**，只在 ≥40px 使用；正文 Inter 400。
10. 动效 120–320ms；入场旋转一次；`prefers-reduced-motion` 下取消。

冲突时优先级：**可访问性 > 品牌与内容 > 本文件 > 个人偏好**。

---

## 3. 色彩

### Light（默认）

| Token | 值 | 用途 |
|---|---|---|
| `--paper` | `#EDE4D2` | 页面底色，占 ~70% |
| `--ink` | `#111111` | 文字、网格线、边框 |
| `--muted` | `#6B6154` | 标签、说明 |
| `--red` | `#D23B2E` | 标题碎片、印章、CTA hover |
| `--mustard` | `#E8B33A` | 高亮碎片、标签 |
| `--blue` | `#2B4BFF` | 照片色偏、可选第三色 |
| `--tape` | `#ECE2C6` | 胶带 |
| `--photo` | `#FBF7EC` | 照片白边 |

### Dark

| Token | 值 |
|---|---|
| `--paper` | `#141210` |
| `--ink` | `#F2EBDD` |
| `--muted` | `#B5A894` |
| `--red` | `#E8553F` |
| `--mustard` | `#F0C04E` |
| `--blue` | `#5C78FF` |
| `--tape` | `#3A3428` |
| `--photo` | `#2A241C` |

### 对比度（实测，浅色底）

| 组合 | 比值 | 可用性 |
|---|---|---|
| ink / paper | 15.0:1 | 正文、标题 |
| muted / paper | 4.8:1 | 标签、说明 |
| ink / mustard | 9.8:1 | 黄底黑字 |
| `#FBF7EC` / red | 4.5:1 | 红底白字（大字更稳） |
| ink / blue | 4.6:1 | 蓝底黑字可用 |
| `#FBF7EC` / blue | 5.4:1 | 蓝底白字可用 |

### 规则

- 红底只配白字，粉 / 黄底只配黑字；不要反过来。
- 一屏最多 3 个碎片颜色（纸白 / 红 / 黄），蓝只做照片色偏或一个小标签。
- 深色模式保留纸感：不要用纯黑 `#000`，用 `#141210`。

---

## 4. 字体

### 角色

| 角色 | 字体 | 字重 | 说明 |
|---|---|---|---|
| Display | Archivo Black | 400 | 中文回退 PingFang SC 900 |
| Aside | Instrument Serif italic | 400 | 中文回退 Songti SC italic |
| Body | Inter | 400 | 正文、说明 |
| Label | JetBrains Mono | 500 | 编号、照片说明、印章 |
| Logo | Archivo Black | 400 | 字标 |

Archivo Black 只有 400；不要写 700 去“加粗”。中文 900 只在 ≥40px 使用。

### 字阶

| Token | size / line-height / tracking | 用途 |
|---|---|---|
| `scrap-lg` | `clamp(44px, 6.8vw, 94px)` / 0.96 / `-0.02em` | 标题最大碎片 |
| `scrap-md` | `clamp(42px, 6.4vw, 88px)` / 0.96 / `-0.02em` | 标题碎片 |
| `scrap-sm` | `clamp(38px, 5.8vw, 78px)` / 0.96 / `-0.02em` | 标题短碎片 |
| `h2` | `clamp(28px, 4vw, 44px)` / 1.05 / `-0.02em` | 区块标题 |
| `body` | `14px` / 1.7 / `0` | 正文 |
| `label` | `9.5px` / 1 / `0.14em`，大写 | 标签、图注 |
| `aside` | `clamp(17px, 1.8vw, 23px)` / 1.35，斜体 | 手写旁白 |

---

## 5. 布局

### 网格

- max-width `1400px`；页边距 ≥1080 用 `48px`，760–1080 用 `32px`，<760 用 `20px`
- 底层 12 栏，gutter `16px`；切割垫网格 `48px`，线 `rgba(17,17,17,.05)`
- 首屏高度 `100svh - 46px`；内容区至少 `520px`

### 间距

`4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 80 / 120`

- 首屏上下：32–64
- 标题 → 正文：26
- 正文 → 按钮：24
- 照片之间至少留 `32px`，不要互相压住文字

### 形状

- radius 0（照片白边也直角）
- 撕纸边：`clip-path` 多边形，最多 12 个顶点
- 胶带：`96×24px`，半透明，旋转 ±20°
- 照片：6px 白边，`box-shadow: 0 16px 40px rgba(40,30,20,.22)`（唯一阴影）

### 响应式

| 断点 | 行为 |
|---|---|
| ≥1081 | 标题 3 碎片横排；3–4 张照片环绕 |
| 760–1080 | 标题 2 行；保留 2 张照片；印章与标签下移 |
| 620–759 | 隐藏照片与胶带，只留碎片、印章、标签 |
| <620 | 标签改静态排列；印章缩小；标题碎片允许换行 3 行 |

移动端：照片隐藏是为了保证可读性；不要把它们缩到看不清还硬塞。

---

## 6. 组件

### 标题碎片

- 3 个碎片：纸白黑字、红底白字、黄底黑字
- 每片独立旋转（`-2° / 3° / -1.5°`），用 `clip-path` 做撕边
- 文字必须单行；窄屏允许每片单独一行

```html
<h1 class="flex flex-wrap items-center gap-x-3.5 gap-y-2">
  <span class="bg-[#FBF7EC] px-[.12em] font-display text-scrap-md [clip-path:polygon(...)] -rotate-2">让想法，</span>
  <span class="bg-[#D23B2E] px-[.12em] text-[#FBF7EC] [clip-path:polygon(...)] rotate-3">落到</span>
  <span class="bg-[#E8B33A] px-[.12em] [clip-path:polygon(...)] -rotate-[1.5deg]">屏幕上。</span>
</h1>
```

撕边多边形（可直接用）：

```
polygon(0 5%, 3% 0, 48% 2%, 97% 0, 100% 9%, 98% 46%, 100% 88%, 96% 100%, 52% 98%, 4% 100%, 0 92%, 2% 50%)
```

### 照片

- 6px 白边；内部做 halftone（重复径向渐变）+ 单一色偏
- 右下或左下角 mono 图注 `Fig. 01 — 2026`
- 每张照片最多一条胶带，胶带压在边上，不压人脸 / 主体

```html
<figure class="absolute right-[2%] top-0 w-[240px] rotate-6 border-[6px] border-[#FBF7EC] bg-[linear-gradient(135deg,#56697A,#C0A98A)] shadow-[0_16px_40px_rgba(40,30,20,.22)]">
  <figcaption class="absolute -bottom-5 left-1 font-mono text-[8px] uppercase tracking-[0.14em] text-muted">Fig. 01 — 2026</figcaption>
</figure>
```

### 胶带

- `96×24px`，`rgba(236,226,198,.72)`，加细条纹
- 旋转 ±20°，`z-index` 高于照片
- 每张照片最多 1 条；不要贴成“井”字

### 印章

- 双线方框 + 两行 mono 大写 + 城市 / 年份
- 红色，旋转 `-12°`，透明度 `.82`
- 每屏 1 个，位置在边缘，不要压标题

### 标签行

- 3–4 个纸片标签，mono 9.5px，`01 · 品牌` 格式
- 轻微旋转（±2°），其中一个用黄色
- 桌面绝对定位在左下；移动端改为静态 flex

### 旁白

- Instrument Serif italic，17–23px，`-4°`
- 以 `↳` 开头，最多一句；中文回退宋体斜体
- 一屏最多 1 条

---

## 7. 动效

| Token | 值 |
|---|---|
| `--dur-fast` | `120ms` |
| `--dur` | `180ms` |
| `--dur-slow` | `320ms` |
| `--ease` | `cubic-bezier(.2,.8,.2,1)` |

### 编排

- 入场：碎片从 `rotate(0)` 到目标角度 + 上移 24px，stagger 60ms（只一次）
- 照片：上移 20px + 淡入；胶带不单独动
- hover：按钮 `rotate(-1° → 1°)` + 上移 2px；不要放大
- 没有持续运动；不要漂浮、抖动、视差

### 降级

`prefers-reduced-motion: reduce` → 取消旋转入场与位移，元素直接显示为最终角度。

---

## 8. 图像与图标

- 照片：高对比、暖色 duotone 或 halftone；不要用彩色渐变占位图
- 没有照片时：用色块 + 图注占位，不要用 emoji
- 图标：如必须，2px 描边、粗黑、方形端点；不混线性与填充
- 允许：点阵、网点、纸张纹理、复印颗粒
- 禁止：玻璃、发光、3D、渐变网格、emoji

---

## 9. 文案

- 像手写便签和杂志标题：短、直接、有一点态度
- 允许口语和“不”；不要网络烂梗
- 示例：
  - 好：“别做无聊的东西。”
  - 好：“先贴上去，再对齐。”
  - 差：“以匠心致初心，焕新品牌价值。”

---

## 10. Do / Don't

| Do | Don't |
|---|---|
| 底网格 + 5 个以内的拼贴元素 | 满屏随机旋转 |
| 3 个碎片颜色 | 每个字一种颜色 |
| 6px 白边 + 一条胶带 | 照片无边框 + 多条胶带 |
| 一个印章 | 每屏都有印章 |
| 撕边只用于标题/照片 | 按钮也做撕边 |
| 软阴影只给照片 | 卡片也加软阴影 |
| 静态拼贴 | 元素持续摇晃 |

### 如果要收敛

- 旋转收敛到 ±3°
- 去掉胶带和第三张照片，保留碎片 + 图注
- 印章改为文字标签
- 背景网格从 48px 放大到 64px，降低存在感

---

## 11. Tailwind v4

```css
@import "tailwindcss";

:root {
  --paper: #EDE4D2;
  --ink: #111111;
  --muted: #6B6154;
  --red: #D23B2E;
  --mustard: #E8B33A;
  --blue: #2B4BFF;
  --tape: #ECE2C6;
  --photo: #FBF7EC;
}

[data-theme="dark"] {
  --paper: #141210;
  --ink: #F2EBDD;
  --muted: #B5A894;
  --red: #E8553F;
  --mustard: #F0C04E;
  --blue: #5C78FF;
  --tape: #3A3428;
  --photo: #2A241C;
}

@theme inline {
  --color-paper: var(--paper);
  --color-ink: var(--ink);
  --color-muted: var(--muted);
  --color-red: var(--red);
  --color-mustard: var(--mustard);
  --color-blue: var(--blue);
  --color-tape: var(--tape);
  --color-photo: var(--photo);

  --font-display: "Archivo Black", "PingFang SC", sans-serif;
  --font-serif: "Instrument Serif", "Songti SC", serif;
  --font-sans: "Inter", "PingFang SC", sans-serif;
  --font-mono: "JetBrains Mono", ui-monospace, monospace;

  --text-scrap-lg: clamp(2.75rem, 6.8vw, 5.875rem);
  --text-scrap-lg--line-height: 0.96;
  --text-scrap-lg--letter-spacing: -0.02em;

  --text-scrap-md: clamp(2.625rem, 6.4vw, 5.5rem);
  --text-scrap-md--line-height: 0.96;
  --text-scrap-md--letter-spacing: -0.02em;

  --text-scrap-sm: clamp(2.375rem, 5.8vw, 4.875rem);
  --text-scrap-sm--line-height: 0.96;
  --text-scrap-sm--letter-spacing: -0.02em;
}
```

---

## 12. 给 AI 的 prompt（可直接粘贴）

```
Build an editorial collage [page type] for [audience].
Read DESIGN.md and treat it as a hard constraint.

Non-negotiables:
- Aged paper #EDE4D2, ink #111, 0 radius; underlying 12-column grid plus a 48px
  cutting-mat grid at 5% opacity.
- Headline: 3 torn-paper scraps (paper / red / mustard) with labels, rotated
  -2°, 3° and -1.5°; one visual focus only.
- Type: Archivo Black for scraps (Chinese PingFang 900 only ≥40px),
  Inter for body, JetBrains Mono 9–10px uppercase for labels,
  Instrument Serif italic for one aside at most.
- Photos: 6px white border, halftone texture, 8–16px soft shadow (the only shadow),
  one tape strip each, mono caption.
- Max 5 collage elements per viewport; no gradients, glass, glow, 3D or emoji.
- Motion: 120–320ms rotate/translate, staggered 60ms, once only; no floating.
- Mobile ≤620px: hide photos and tape, keep scraps, stamp and tag row.

Output semantic HTML + Tailwind v4, mobile-first, with visible focus states.
```

---

## 13. 验收清单

- [ ] 底网格可见，所有元素对得上网格
- [ ] 拼贴元素 ≤5 个/屏
- [ ] 旋转在 -8°~9°，没有持续摇晃
- [ ] 标题 3 个碎片，颜色 / 文字对比达标
- [ ] 照片 6px 白边 + 单条胶带 + 图注
- [ ] 软阴影只出现在照片上
- [ ] 印章 ≤1 个，旁白 ≤1 条
- [ ] 移动端隐藏照片后仍成立，不空洞
- [ ] 触控目标 ≥44px，焦点环可见
- [ ] reduced-motion 下无旋转入场
- [ ] 没有渐变 / 玻璃 / emoji / 3D
- [ ] 中文 900 只出现在 ≥40px 标题

---

变更记录：v1.0 — 初版，基于 style-probe-2 N4。
