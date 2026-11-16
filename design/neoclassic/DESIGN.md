# DESIGN.md — Neoclassicism / 新古典主义

> 版本 1.0 · 2026-11
> 适用：设计师 / 工作室作品集、品牌官网、展览与出版物邀请页、文化机构、移动端 H5
> 字体：Cormorant Garamond（标题）/ Inter（正文与标签）
> 使用方式：先读 §2「Hard rules」，按 §3–§9 实现，交付前逐条过 §13。
> 视觉基准：`../../style-probe-2.html#n1`

---

## 1. 定位

用对称、留白和高对比衬线建立“庄重感”。整页只有象牙纸色、墨色和一点旧金，所有装饰都必须有结构上的理由（框、线、印章、罗马数字），不是贴上去的花纹。

- **它相信**：秩序让人安静；比例比装饰重要。
- **它拒绝**：亮金渐变、浮雕阴影、卷草花纹、婚礼请柬式的堆砌。

| 适合 | 不适合 |
|---|---|
| 设计师 / 工作室作品集 | 游戏、儿童、潮流快消 |
| 品牌官网、机构介绍 | 高密度后台 |
| 展览 / 出版物 / 邀请页 | 促销、直播、强转化落地页 |
| 建筑、法律、咨询 | 需要强角色感的营销页 |
| 文化项目 H5 | 大量插画 / 3D 的页面 |

**一句话给 AI**：Neoclassical editorial — symmetrical ivory canvas, double hairline frame, high-contrast Cormorant display, small-caps labels, one antique gold, zero shadows, Roman numerals.

---

## 2. Hard rules（不可协商）

1. 圆角 `0`；`box-shadow: none`。
2. 只允许 `1px` 实线；边框颜色 `--line`，装饰线用 `--gold`。
3. 全页居中对称；不要左右不对称的“创意排版”。
4. 一屏最多 1 个旧金强调，面积 ≤ 5%；小字金必须用 `--gold-ink`（对比度达标）。
5. 禁止：渐变、玻璃、发光、阴影、卷草花纹、emoji。
6. 标题最多 2 行，用 `text-wrap: balance`；中文标题字距 `-0.01em` ~ `0.005em`。
7. 英文小标题全大写 + `0.14em` 字距；中文不做全大写。
8. 动效 ≥ 400ms，只允许淡入、轻微上移、线条展开；不要弹跳、不要视差。
9. 触控目标 ≥ 44×44；焦点环 2px 实线 + 2px offset。
10. 一屏最多 1 张图片；没有图片时用字与线，不要用插画填充。

冲突时优先级：**可访问性 > 品牌与内容 > 本文件 > 个人偏好**。

---

## 3. 色彩

### Light（默认）

| Token | 值 | 用途 |
|---|---|---|
| `--paper` | `#F4EFE4` | 页面底色，占 ~85% |
| `--surface` | `#FBF7EE` | 需要时的高光块，极少用 |
| `--ink` | `#1C1A17` | 标题、正文、深色线 |
| `--muted` | `#5C5448` | 次级正文、说明 |
| `--line` | `#D8D0BF` | 1px 分隔线、外框 |
| `--gold` | `#9A7B4F` | 装饰线、菱形、印章；**不用于小字** |
| `--gold-ink` | `#7A5C34` | 小号金色文字（9–14px） |

### Dark

| Token | 值 |
|---|---|
| `--paper` | `#161411` |
| `--surface` | `#1D1A16` |
| `--ink` | `#EFE8DA` |
| `--muted` | `#A79C8A` |
| `--line` | `#332E27` |
| `--gold` | `#C2A36B` |
| `--gold-ink` | `#D8BC8A` |

### 用量

- 85% 纸色
- 10% 墨色文字与线
- 5% 旧金（线、印章、编号）

### 对比度（实测）

| 组合 | 比值 | 可用性 |
|---|---|---|
| ink / paper | 15.2:1 | 正文、标题 |
| muted / paper | 6.5:1 | 正文、说明 |
| gold-ink / paper | 5.3:1 | 小字标签 |
| gold / paper | 3.4:1 | 仅 ≥24px 或非文本装饰 |
| line / paper | 1.3:1 | 仅装饰 |

### 规则

- 金色分两档：`--gold` 做线，`--gold-ink` 做字。不要用 `--gold` 写 10px 标签。
- 深色模式不是反色：纸色变暖黑，金色提亮；不要用纯黑 `#000`。
- 需要强调时优先用字重和字号，不要增加第二种颜色。

---

## 4. 字体

### 角色

| 角色 | 字体 | 字重 | 说明 |
|---|---|---|---|
| Display | Cormorant Garamond | 400–500 | 中文回退 Songti SC / 思源宋体 |
| Small caps | Cormorant Garamond | 400 | 英文副标题，大写 + `0.14em` |
| Body | Inter | 400 | 中文回退 PingFang SC |
| Label | JetBrains Mono | 400–500 | 9–10px 大写 + `0.3em` |
| Roman | Cormorant Garamond italic | 400 | 罗马数字、编号 |

Cormorant 的高对比笔画是这套系统的核心；不要用它排正文（小字号会断笔）。

### 字阶

| Token | size / line-height / tracking | 用途 |
|---|---|---|
| `display` | `clamp(44px, 7.2vw, 104px)` / 1.04 / `0.005em` | H1，最多 2 行 |
| `display-en` | `0.42em` / 1.2 / `0.14em`，大写 | 英文副标题 |
| `h2` | `clamp(28px, 4vw, 44px)` / 1.1 / `0.005em` | 区块标题 |
| `body` | `14px` / 1.75 / `0.02em` | 正文 |
| `small` | `11px` / 1.6 / `0.04em` | 注释、页脚 |
| `label` | `9.5px` / 1 / `0.3em`，大写 | 导航、eyebrow |
| `roman` | `13px` / 1 / `0.1em`，斜体 | 罗马数字 |

中文正文行长 **28–34 字**；英文 55–70 字符。

### 中文规则

- 中文标题用 Songti SC **500**，不要 700；宋体加粗会糊。
- 中文不做 `text-transform`；不单独加宽字距（超过 `0.02em` 会散）。
- 行高：标题 1.04–1.1；正文 1.75。
- 中文标点用全角；数字与单位不空格（`2026`、`240ms`）。

---

## 5. 布局

### 结构

- 居中容器：max-width `1240px`，页边距 ≥1080 用 `72px`，760–1080 用 `32px`，<760 用 `24px`
- 外框：距视口 `58px 16px 16px`，`1px` 实线；内框再内缩 `5px`，用 `--gold` 35% 透明度
- 首屏高度 `100svh - 46px`（46px 为顶部标签条）；内容垂直居中

### 间距

`4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 / 128`

- 首屏上下：48–64
- 标题 → 英文副标题：10
- 副标题 → 分隔饰线：24
- 饰线 → 正文：24
- 正文 → 链接：26

### 形状

- radius 0
- border `1px`
- shadow none
- 允许的装饰：双线框、菱形饰线、圆形印章、罗马数字

### 响应式

| 断点 | 行为 |
|---|---|
| ≥1080 | 双线框 + 三栏服务；标题 104px |
| 760–1079 | 保持居中；标题降级；三栏保持 |
| 620–759 | 服务改单列，用横线分隔；印章隐藏 |
| <620 | 外框 inset 8px；导航只留居中 wordmark；标题 clamp 最小 38px |

移动端：框架仍保留（这是风格的一部分），但缩到 8px；不要隐藏正文。

---

## 6. 组件

### 导航

三栏对称：左 `Atelier`、中 wordmark、右 `Shanghai`；9px 大写 + `0.3em`；底部 1px 线。

```html
<header class="grid grid-cols-[1fr_auto_1fr] items-center border-b border-line py-5
               font-mono text-[9px] uppercase tracking-[0.3em] text-muted">
  <span>Atelier</span>
  <span class="justify-self-center text-[11px] tracking-[0.34em] text-ink">Studio Null</span>
  <span class="justify-self-end">Shanghai</span>
</header>
```

### 首屏

- eyebrow：`MMXXVI — 独立设计工作室`，9.5px，`--gold-ink`，`0.34em`
- H1 居中，2 行；英文副标题在下一行，字距 `0.14em`
- 饰线：`64px 线 + 5px 旋转方块 + 64px 线`
- 正文：max-width 40ch，居中
- 链接：文字 + 1px 下划线，高 44px

### 链接 / CTA

- 不使用填充按钮；用文字 + 下划线
- 9.5px 大写 + `0.24em`，下划线偏移 5px
- hover：下划线变 `--gold-ink`，颜色同步，250ms

### 罗马数字栏目

三栏，居中，`I / II / III` 用 Cormorant italic + `--gold-ink`；标题 10.5px 大写；说明 11px。

```html
<div class="grid grid-cols-3 border-t border-line pt-5 text-center">
  <div class="px-4">
    <b class="font-serif text-[13px] italic text-gold-ink">I</b>
    <h3 class="mt-2.5 font-mono text-[10.5px] uppercase tracking-[0.22em]">品牌</h3>
    <p class="mt-1.5 text-[11px] text-muted">命名 · 标识 · 视觉系统</p>
  </div>
  <!-- II / III 同理，+ div 用 border-l 分隔 -->
</div>
```

### 印章

- 双圆环 + 环绕文字 + 中心字母；`64–88px`；旋转 `-8°`；`--gold`
- 只在 ≥620px 显示；不要做多个印章

```html
<svg viewBox="0 0 100 100" class="h-20 w-20 text-gold" aria-hidden="true">
  <defs><path id="seal" d="M50,50 m-37,0 a37,37 0 1,1 74,0 a37,37 0 1,1 -74,0"/></defs>
  <circle cx="50" cy="50" r="47" fill="none" stroke="currentColor"/>
  <circle cx="50" cy="50" r="43" fill="none" stroke="currentColor" stroke-width=".5"/>
  <text font-size="7" letter-spacing="2.4" fill="currentColor">
    <textPath href="#seal">STUDIO NULL · SHANGHAI · EST MMXXI ·</textPath>
  </text>
  <text x="50" y="56" text-anchor="middle" font-size="15" fill="currentColor">SN</text>
</svg>
```

### 页脚

- 顶部 1px 线，四栏；11px；最后一行版权 + 年份
- 不要社交媒体彩色图标；用文字链接

---

## 7. 动效

| Token | 值 |
|---|---|
| `--dur` | `600ms` |
| `--dur-slow` | `900ms` |
| `--ease` | `cubic-bezier(.22,.61,.36,1)` |

### 编排

- 首屏：eyebrow → 标题 → 饰线 → 正文 → 链接，依次淡入 + 上移 8px，间隔 80ms
- 饰线：`scaleX(0 → 1)`，700ms，单独触发
- 链接 hover：下划线颜色变化，250ms
- 页面内**没有**持续运动；不要浮动、呼吸、视差
- 允许一次滚动触发：标题淡入，仅一次

### 降级

`prefers-reduced-motion: reduce` → 所有位移取消，元素直接显示；饰线不做展开。

---

## 8. 图像与图标

- 最多 1 张图；静物、建筑、档案照片；暖色调 duotone
- 图片加 1px 细框 + 8px 白边（像装裱），不要圆角、不要阴影
- 没有图片时：用标题、饰线、留白，不要插画
- 图标：如必须，1px 线性、方形端点、16/20；不混填充
- 禁止：3D、渐变、发光、emoji、卷草花纹、金色渐变字

---

## 9. 文案

- 正式但不古板；短句，名词优先
- 标题 4–12 字；避免感叹号、网络用语
- 英文小标题 2–4 个词，全大写
- 示例：
  - 好：“让想法，落到屏幕上。”
  - 好：“少一点，准一点。”
  - 差：“尊享极致奢华体验，开启非凡之旅！”

---

## 10. Do / Don't

| Do | Don't |
|---|---|
| 严格居中，左右对称 | 左右不对称的“创意”错位 |
| 双线框 + 菱形饰线 | 卷草花纹 / 金色渐变 |
| 一个旧金，5% 面积 | 金色铺满按钮和标题 |
| Cormorant 大字 + Inter 正文 | 全站 Cormorant（小字断笔） |
| 一座印章 | 每屏都有印章 |
| 1px 线、无阴影 | 卡片阴影 + 圆角 |
| 600–900ms 淡入 | 弹跳、旋转、视差 |

### 如果要收敛（保留风格的降级版）

- 双线框 → 单线框
- 印章 → 可去掉
- 旧金 → 只保留 `--gold-ink` 用于线
- 动效 → 400ms，仅淡入

---

## 11. Tailwind v4

```css
@import "tailwindcss";

:root {
  --paper: #F4EFE4;
  --surface: #FBF7EE;
  --ink: #1C1A17;
  --muted: #5C5448;
  --line: #D8D0BF;
  --gold: #9A7B4F;
  --gold-ink: #7A5C34;
}

[data-theme="dark"] {
  --paper: #161411;
  --surface: #1D1A16;
  --ink: #EFE8DA;
  --muted: #A79C8A;
  --line: #332E27;
  --gold: #C2A36B;
  --gold-ink: #D8BC8A;
}

@theme inline {
  --color-paper: var(--paper);
  --color-surface: var(--surface);
  --color-ink: var(--ink);
  --color-muted: var(--muted);
  --color-line: var(--line);
  --color-gold: var(--gold);
  --color-gold-ink: var(--gold-ink);

  --font-display: "Cormorant Garamond", "Songti SC", "Times New Roman", serif;
  --font-sans: "Inter", "PingFang SC", "Hiragino Sans GB", sans-serif;
  --font-mono: "JetBrains Mono", ui-monospace, monospace;

  --text-display: clamp(2.75rem, 7.2vw, 6.5rem);
  --text-display--line-height: 1.04;
  --text-display--letter-spacing: 0.005em;

  --text-h2: clamp(1.75rem, 4vw, 2.75rem);
  --text-h2--line-height: 1.1;
}
```

---

## 12. 给 AI 的 prompt（可直接粘贴）

```
Build a neoclassical editorial [page type] for [audience].
Read DESIGN.md and treat it as a hard constraint.

Non-negotiables:
- Symmetrical, centered layout; max-width 1240px; ivory #F4EFE4; ink #1C1A17;
  one antique gold #9A7B4F used only for hairlines, ornament and seal (≤5%).
- Double hairline frame inset 58px/16px; 0 radius; no shadows; no gradients.
- Type: Cormorant Garamond 400–500 for display (Chinese falls back to Songti SC),
  Inter for body, JetBrains Mono 9–10px uppercase +0.3em for labels.
- Small gold text must use #7A5C34 (contrast), never #9A7B4F.
- One ornament rule (line–diamond–line), one SVG seal, Roman numerals I/II/III.
- Motion: 600–900ms opacity + 8px rise, 80ms stagger; no bounce, no parallax.
- Mobile: keep the frame at 8px inset, stack the three columns, 44px targets.

Output semantic HTML + Tailwind v4, mobile-first, with visible focus states.
```

---

## 13. 验收清单

- [ ] 全页居中对称，没有一侧偏重
- [ ] 双线框完整，没有缺口
- [ ] 圆角 0、阴影 0、渐变 0
- [ ] 旧金只出现 1–2 处，面积 ≤5%
- [ ] 小字金使用 `--gold-ink`，对比度 ≥4.5:1
- [ ] 中文标题用宋体 500，不是 700
- [ ] 标题 ≤2 行，无孤字
- [ ] 印章 ≤1 个，旋转 -8°
- [ ] 600–900ms 动效，无持续运动
- [ ] reduced-motion 下内容完整
- [ ] 620px 下导航不挤、服务单列
- [ ] 没有卷草花纹 / 金色渐变 / emoji

---

变更记录：v1.0 — 初版，基于 style-probe-2 N1。
