# DESIGN.md — Glitch Art / 故障艺术

> 版本 1.0 · 2026-11
> 适用：音乐 / 游戏 / 开发者活动、独立品牌、实验影像、H5 传播页
> 字体：Space Grotesk（标题）/ Inter（正文）/ JetBrains Mono（数据与标签）
> 使用方式：先读 §2「Hard rules」，按 §3–§9 实现，交付前逐条过 §13。
> 视觉基准：`../../style-probe-2.html#n3`

---

## 1. 定位

把“信号出错”当成视觉语言：RGB 分离、坏帧色带、扫描线、时间码、乱码 ticker。故障必须是被设计过的、低频的、局部的，不是把整页做成噪点墙。

- **它相信**：错误本身有信息量；克制的故障比持续的闪烁更可信。
- **它拒绝**：全屏闪烁、暗底霓虹、赛博 UI、JPEG 压缩包式的脏。

| 适合 | 不适合 |
|---|---|
| 音乐 / 游戏 / 数字艺术 | 医疗、金融、政务 |
| 开发者工具 / 黑客松 | 面向大众的电商 |
| 实验影像、活动主视觉 | 长文阅读站 |
| 潮流品牌、H5 传播 | 需要“温暖可信”的品牌 |
| 产品发布（技术向） | 高密度后台 |

**一句话给 AI**：Glitch-editorial — light grey canvas, black corrupted media panel, RGB-split display type, signal bands, timecode ticker, mono data labels, no neon.

---

## 2. Hard rules（不可协商）

1. 故障只作用于 **≥40px 的标题**、媒体块和 ticker；正文永不 glitch。
2. 每屏故障元素 ≤ **3** 个（标题 / 媒体块 / ticker 各算一个）。
3. 闪烁 ≤ **3 次/秒**，单次 ≤ 200ms，间隔 ≥ 5s；禁止全屏亮度反转。
4. RGB 分离偏移 2–3px；`#FF2D55`・`#00D9FF` 只做偏移和装饰，不做正文颜色。
5. 浅灰底 `#E9E9E7` + 纯黑媒体块；**不要**暗底霓虹（那是赛博朋克）。
6. 扫描线不透明度 ≤ 5%；噪点只出现在媒体块内部。
7. 数据标签 mono 9–11px + `0.14em`；正文 Inter 14/1.75。
8. 两栏：左文案、右媒体；≤1080 改上下，媒体横幅 2:1；≤560 改 4:3。
9. ticker `aria-hidden="true"`；`prefers-reduced-motion` 下停止。
10. 对比度：红色小字用 `#C81E3C`（4.7:1），`#FF2D55` 仅装饰；青色永不用于文字。

冲突时优先级：**可访问性 > 品牌与内容 > 本文件 > 个人偏好**。

> 光敏安全：任何闪烁元素必须能在系统「减少动态效果」下完全静止。不要用闪白、闪黑或连续高频故障。

---

## 3. 色彩

### Light（默认）

| Token | 值 | 用途 |
|---|---|---|
| `--bg` | `#E9E9E7` | 页面底色，占 ~80% |
| `--ink` | `#0A0A0A` | 正文、标题、线 |
| `--muted` | `#55554F` | 次级文字、数据标签 |
| `--red` | `#C81E3C` | 小字红（对比达标） |
| `--red-signal` | `#FF2D55` | RGB 偏移、色带、非文本装饰 |
| `--cyan` | `#00D9FF` | RGB 偏移、色带、扫描线；**不做文字** |
| `--media` | `#0B0B0B` | 媒体块底色 |

### Dark

| Token | 值 |
|---|---|
| `--bg` | `#0B0B0C` |
| `--ink` | `#EDEDED` |
| `--muted` | `#9A9A96` |
| `--red` | `#FF6B82` |
| `--red-signal` | `#FF2D55` |
| `--cyan` | `#35E0FF` |
| `--media` | `#050505` |

### 对比度（实测，浅色底）

| 组合 | 比值 | 可用性 |
|---|---|---|
| ink / bg | 16.4:1 | 正文、标题 |
| muted / bg | 6.1:1 | 数据标签 |
| `#C81E3C` / bg | 4.7:1 | 小字红、链接 |
| `#FF2D55` / bg | 3.0:1 | **仅非文本** |
| `#00D9FF` / bg | 1.4:1 | **仅非文本** |

### 规则

- 红分两档：文字 `--red`，信号 `--red-signal`；不要混用。
- 青色只出现在偏移阴影、色带、扫描线里，不做文字、不做按钮底色。
- 媒体块是唯一允许纯黑的地方；页面其余部分保持浅灰。
- 深色模式只换底色与文字，不增加发光；色带仍是 3 条，扫描线仍 ≤5%。

---

## 4. 字体

### 角色

| 角色 | 字体 | 字重 | 说明 |
|---|---|---|---|
| Display | Space Grotesk | 700 | 中文回退 PingFang SC 700 |
| Body | Inter | 400 | 正文、说明 |
| Data / Label | JetBrains Mono | 400–700 | 时间码、hex、帧号 |
| Eyebrow | JetBrains Mono | 400 | `[ SIGNAL LOST ]` 式标签 |

### 字阶

| Token | size / line-height / tracking | 用途 |
|---|---|---|
| `display` | `clamp(40px, 5.8vw, 80px)` / 1.02 / `-0.045em` | H1，最多 2 行 |
| `h2` | `clamp(28px, 3.6vw, 44px)` / 1.1 / `-0.03em` | 区块标题 |
| `body` | `14px` / 1.75 / `0` | 正文 |
| `label` | `10px` / 1 / `0.22em`，大写 | eyebrow |
| `data` | `9–11px` / 1 / `0.14em`，大写 | 帧号、hex、ticker |
| `code` | `12px` / 1.9 | 终端块 |

中文标题用 PingFang SC 700；中文不做全大写、不做负字距超过 `-0.02em`。

---

## 5. 布局

### 网格

- max-width `1400px`；页边距 ≥1080 用 `48px`，760–1080 用 `32px`，<760 用 `20px`
- 首屏：`1.08fr / 0.92fr` 两栏，gap `clamp(24px, 4vw, 56px)`
- 顶部状态条：左 `Studio_Null`、中 `REC — Signal 98%`、右 `ERR / 0x04`
- 底部 ticker 贯穿内容宽度，1px 上边线

### 间距

`4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 80 / 120`

- 首屏上下：28–48
- 标题 → 正文：20
- 正文 → 按钮：28
- 按钮 → 数据行：26

### 形状

- radius 0
- 媒体块直角，1px 白/黑边可选
- 按钮直角，无圆角
- 允许：水平色带、像素块、竖向拉丝、扫描线

### 响应式

| 断点 | 行为 |
|---|---|
| ≥1081 | 两栏；媒体 4:4.7 竖幅 |
| 560–1080 | 单栏；媒体横幅 2:1 |
| <560 | 单栏；媒体 4:3；ticker 保留；数据行换行 |

---

## 6. 组件

### 顶部状态条

```html
<header class="flex items-center justify-between border-b border-ink py-3.5
               font-mono text-[9.5px] uppercase tracking-[0.14em]">
  <span>Studio_Null</span>
  <span class="text-red">● Rec — Signal 98%</span>
  <span>Err / 0x04</span>
</header>
```

### 标题（RGB 分离）

- 3px 红偏移 + 3px 青偏移，只做 `text-shadow`
- 不复制文本节点；不做 clip-path 切片（会伤可读性）
- 每 7s 一次 200ms 的轻微位移 burst

```html
<h1 class="font-display text-display font-bold
           [text-shadow:3px_0_rgba(255,45,85,.5),-3px_0_rgba(0,217,255,.55)]">
  让想法，<br>落到屏幕上。
</h1>
```

### 媒体块

竖幅（桌面）/ 横幅（平板）/ 4:3（手机），内部结构：

1. 纯黑底 `--media`
2. 扫描线：`repeating-linear-gradient(0deg, rgba(255,255,255,.05) 0 1px, transparent 1px 4px)`
3. 三条信号带：红 9% 高、青 3%、白 14%，`mix-blend-mode: screen`
4. 像素块：左上 36%×28%，低透明度网格
5. 竖向拉丝：`repeating-linear-gradient(90deg, …)` + `blur(2px)`
6. 右下大号轮廓数字（`-webkit-text-stroke: 1px rgba(255,255,255,.16)`）
7. 角标：`REC`、时间码 `00:04:21:18`、竖排 `ERR_04`

```html
<div class="relative aspect-[4/4.7] overflow-hidden bg-media">
  <div class="absolute inset-0 bg-[repeating-linear-gradient(0deg,rgba(255,255,255,.05)_0_1px,transparent_1px_4px)]"></div>
  <span class="absolute left-[-10%] top-[20%] h-[9%] w-[120%] bg-[#FF2D55]/80 mix-blend-screen"></span>
  <span class="absolute left-[-10%] top-[45%] h-[3%] w-[120%] bg-[#00D9FF]/90 mix-blend-screen"></span>
  <span class="absolute bottom-3 right-3 font-mono text-[9px] text-white/75">00:04:21:18</span>
</div>
```

### 数据行

按钮下方，1px 上边线，mono 9px，四项：`Frame 0218 / Buffer 78% / Retry 03 / Signal 98%`。

### Ticker

- 1px 上边线，mono 9.5px，`0.12em`
- 内容为 hex / 状态短语，重复两份，`translateX(-50%)`，45s linear
- `aria-hidden="true"`；`motion-reduce` 停止

### 按钮

- 黑底白字，46px 高，mono 11px + `0.12em`
- hover：`translate(2px,-2px)`，并出现红/青双向偏移阴影
- 不做圆角、不做渐变

---

## 7. 动效

| Token | 值 |
|---|---|
| `--dur-fast` | `120ms` |
| `--dur` | `180ms` |
| `--dur-slow` | `320ms` |
| `--burst` | `7s`（其中 200ms 为故障） |
| `--ticker` | `45s` linear |

### 编排

- 标题：每 7s 一次 200ms 位移 burst；hover 可再触发一次
- 媒体带：4–6.5s 缓慢横移 + `skewY(0.6deg)`
- ticker：持续横移，作为页面“底噪”
- 入场：30px 上移 + 透明度，四段 stagger 80ms
- 禁止：闪白、闪黑、全屏抖动、鼠标跟随、持续缩放

### 降级

`prefers-reduced-motion: reduce` → 取消 burst、色带位移、ticker；静态仍保留 RGB 阴影与媒体块。

---

## 8. 图像与图标

- 如使用真实图片：做双色调或扫描线处理，放在媒体块内，不要整页铺图
- 允许：像素化边缘、色差、坏帧条带
- 禁止：滤镜 App 式“故障贴纸”、emoji、3D、发光
- 图标：1.5px 线性，16/20；不要用故障效果处理图标

---

## 9. 文案

- 技术、短促、像系统日志；允许 `ERR`、`SIGNAL`、`0x` 等词
- 正文保持人话，不要整段乱码（乱码只出现在 ticker / 媒体角标）
- 示例：
  - 好：“信号丢了，想法还在。”
  - 好：“Frame 0218 — 重新解码。”
  - 差：“震撼上线！燃爆全场！”

---

## 10. Do / Don't

| Do | Don't |
|---|---|
| 浅灰底 + 黑媒体块 | 暗底霓虹（会变成赛博朋克） |
| RGB 偏移 2–3px | 10px 正文也加偏移 |
| 每 7s 一次 burst | 持续闪烁 |
| 红/青只做装饰 | 青色文字、红色正文 |
| 一条 ticker | 三条 ticker |
| 媒体块内噪点 | 全页噪点 |
| 9–11px mono 数据 | 数据用大号衬线 |

### 如果要收敛

- 去掉 burst，只保留静态 RGB 阴影
- 去掉色带位移，保留媒体块纹理
- ticker 改为静态一行
- 媒体块换成真实图片 + 扫描线

---

## 11. Tailwind v4

```css
@import "tailwindcss";

:root {
  --bg: #E9E9E7;
  --ink: #0A0A0A;
  --muted: #55554F;
  --red: #C81E3C;
  --red-signal: #FF2D55;
  --cyan: #00D9FF;
  --media: #0B0B0B;
}

[data-theme="dark"] {
  --bg: #0B0B0C;
  --ink: #EDEDED;
  --muted: #9A9A96;
  --red: #FF6B82;
  --red-signal: #FF2D55;
  --cyan: #35E0FF;
  --media: #050505;
}

@theme inline {
  --color-bg: var(--bg);
  --color-ink: var(--ink);
  --color-muted: var(--muted);
  --color-red: var(--red);
  --color-red-signal: var(--red-signal);
  --color-cyan: var(--cyan);
  --color-media: var(--media);

  --font-display: "Space Grotesk", "Inter", "PingFang SC", sans-serif;
  --font-sans: "Inter", "PingFang SC", sans-serif;
  --font-mono: "JetBrains Mono", ui-monospace, monospace;

  --text-display: clamp(2.5rem, 5.8vw, 5rem);
  --text-display--line-height: 1.02;
  --text-display--letter-spacing: -0.045em;

  --animate-ticker: ticker 45s linear infinite;
  --animate-burst: burst 7s steps(1) infinite;
}

@keyframes ticker { to { transform: translateX(-50%); } }
@keyframes burst {
  0%, 90%, 100% { transform: none; }
  91% { transform: translate(-2px, 1px) skewX(-1deg); }
  93% { transform: translate(2px, -1px) skewX(1deg); }
  95% { transform: translate(-1px, 0); }
  97% { transform: none; }
}
```

---

## 12. 给 AI 的 prompt（可直接粘贴）

```
Build a glitch-art editorial [page type] for [audience].
Read DESIGN.md and treat it as a hard constraint.

Non-negotiables:
- Light grey #E9E9E7 canvas, black #0B0B0B media panel, 0 radius, no gradients.
- Display type: Space Grotesk 700, 3px red/cyan text-shadow only, no clip-path slices.
- Red #C81E3C for small text; #FF2D55 and #00D9FF are decorative only.
- Max 3 glitch elements per screen; bursts ≤200ms every 7s; never on body text.
- One mono ticker, aria-hidden, stopped under prefers-reduced-motion.
- Media panel: scanlines ≤5%, three signal bands, pixel block, one outline number,
  timecode and REC labels.
- Layout: 2 columns desktop, stacked ≤1080 with a 2:1 banner, 4:3 on mobile.
- Motion: translate/opacity only; no flashing white/black, no full-screen shake.

Output semantic HTML + Tailwind v4, mobile-first, with visible focus states.
```

---

## 13. 验收清单

- [ ] 故障只在标题 / 媒体 / ticker，正文干净
- [ ] 每屏故障元素 ≤3
- [ ] 闪烁 ≤3 次/秒，reduced-motion 全停
- [ ] 小字红是 `#C81E3C`，不是 `#FF2D55`
- [ ] 青色没有用于任何文字
- [ ] 扫描线 ≤5%，只覆盖媒体块
- [ ] ticker aria-hidden，且不是唯一信息源
- [ ] 媒体块在手机上是 4:3，不撑破宽度
- [ ] 触控目标 ≥44px，焦点环可见
- [ ] 暗色模式下红/青对比度单独测过
- [ ] 没有暗底霓虹 / 渐变 / 发光
- [ ] 页面不引起明显眩晕（自测：盯 30 秒）

---

变更记录：v1.0 — 初版，基于 style-probe-2 N3。
