# DESIGN.md — Swiss Minimal / 极简瑞士

> 版本 1.0 · 2026-11
> 适用：作品集、品牌官网、编辑型落地页、移动端 H5
> 字体：Inter（主）/ Instrument Serif（每屏最多一处）
> 使用方式：先读 §2「Hard rules」，按 §3–§9 实现，交付前逐条过 §13。
> 视觉基准：`../../style-probe.html#s1`

---

## 1. 定位

用网格、留白和字重建立秩序；整套页面只允许一个暖红作为“事件”，其余是纸色、墨色和灰。

- **它相信**：秩序来自对齐和克制，不来自装饰。
- **它拒绝**：渐变、玻璃、发光、圆角卡片、彩色插画、居中堆叠的 SaaS 模板。

| 适合 | 不适合 |
|---|---|
| 设计师 / 工作室作品集 | 儿童、游戏类产品 |
| 品牌官网、机构介绍 | 需要强角色感的营销页 |
| 编辑型长文、年度报告 | 高密度数据后台 |
| 高客单 B 端落地页 | 大促、促销页 |
| 展览、出版物配套站点 | 大量插画 / 3D 的页面 |

**一句话给 AI**：Swiss editorial minimal — strict 12-column grid, paper & ink, one vermillion accent, zero radius, hairline rules, typography does all the work.

---

## 2. Hard rules（不可协商）

1. 圆角 `0px`；`box-shadow: none`。
2. 只允许 `1px` 实线，颜色 `--line`；不要 2px、3px 边框。
3. 一屏最多 **1** 个强调色（暖红），面积 ≤ 3%，不用于正文。
4. 禁止：渐变、玻璃拟态、发光、噪点纹理、emoji 图标、3D。
5. 字号只能取 §4 阶梯里的值，不要临时写 17px、22px。
6. 中文标题字距 `-0.02em`，英文 `-0.04em`；全大写只用于 ≤11px 的英文标签。
7. 所有数字 `font-variant-numeric: tabular-nums`。
8. 动效 ≤ 420ms，只允许位移、透明度、下划线伸缩；不要缩放卡片、不要弹跳。
9. 12 栏网格内对齐；元素不得“差不多居中”。
10. 触控目标 ≥ 44×44；焦点环 2px 实线 + 2px offset，不能用阴影代替。

冲突时优先级：**可访问性 > 品牌与内容 > 本文件 > 个人偏好**。

---

## 3. 色彩

### Light（默认）

| Token | 值 | 用途 |
|---|---|---|
| `--paper` | `#F2F0E9` | 页面底色，占 90% |
| `--surface` | `#FBFAF5` | 卡片 / 输入框，仅需要时 |
| `--ink` | `#141414` | 标题、正文、深色按钮 |
| `--muted` | `#6B6B63` | 次级文字、说明、标签 |
| `--line` | `#D8D6CE` | 1px 分隔线、边框 |
| `--accent` | `#D9482B` | 方块、编号、链接 hover |
| `--accent-ink` | `#FFFFFF` | 强调色上的文字（少用） |

### Dark

| Token | 值 |
|---|---|
| `--paper` | `#121211` |
| `--surface` | `#1A1A18` |
| `--ink` | `#F2F0E9` |
| `--muted` | `#9C9C92` |
| `--line` | `#2E2E2A` |
| `--accent` | `#FF6A4D`（提亮，保证暗底对比） |
| `--accent-ink` | `#121211` |

### 用量

- 90% 纸色 / 白
- 8% 墨色文字与线
- 2% 暖红

### 对比度（实测）

| 组合 | 比值 | 可用性 |
|---|---|---|
| ink / paper | 16.2:1 | 正文、标题 |
| muted / paper | 4.7:1 | ≥14px 文本 |
| accent / paper | 4.9:1 | ≥16px 文本或非文本 |
| line / paper | 1.35:1 | 仅装饰，不承载信息 |

### 规则

- 强调色不做大面积背景，不做主按钮填充；主按钮用墨色。
- 深色模式不是简单反色：暖红提亮到 `#FF6A4D`。
- 需要区分层级时，用字重和线，不要引入第二种颜色。

---

## 4. 字体

### 角色

| 角色 | 字体 | 字重 | 说明 |
|---|---|---|---|
| Display | Inter | 500–600 | 中文回退 PingFang SC 500/600 |
| Body | Inter | 400 | 正文 16px |
| Label | Inter | 500 | 10–11px 全大写，`+0.12em` |
| Accent | Instrument Serif | 400 / italic | 每屏最多 1 处；1–3 个词或超大编号 |
| Mono | 系统 monospace | 400 | 只用于代码、token、版本号 |

Instrument Serif 是这套系统的“破格”：只出现一次，制造编辑感；出现两次就失效。
中文回退 **Songti SC / 思源宋体**。

### 字阶

| Token | size / line-height / tracking | 用途 |
|---|---|---|
| `display` | `clamp(56px, 8.3vw, 122px)` / 0.98 / `-0.04em` | 首屏 H1，最多 2 行 |
| `h2` | `clamp(32px, 4.6vw, 56px)` / 1.05 / `-0.03em` | 区块标题 |
| `h3` | `20px` / 1.35 / `-0.01em` | 卡片标题 |
| `body-lg` | `18px` / 1.6 / 0 | 导语 |
| `body` | `16px` / 1.65 / 0 | 正文 |
| `small` | `13px` / 1.55 / 0 | 注释、页脚 |
| `label` | `10px` / 1 / `+0.12em`，大写 | 分区标签、编号 |
| `serif` | `clamp(40px, 6vw, 96px)` / 1 / `-0.02em` | 衬线点缀 |

中文正文行长 **28–34 字**；英文 60–75 字符。

### 中文规则

- 标题 500–600，不用 700+，不描边。
- 中英混排：英文 Inter，中文自动回退 PingFang SC，不要给中文单独加字距（超过 ±0.02em 会散）。
- 行高：标题 0.98–1.1；正文 1.65。
- 不用伪斜体；强调用衬线或 1px 下划线。
- 标点不单独换行；数字与单位之间不空格（`240ms`）。

---

## 5. 布局

### 网格

- 12 栏，gutter `24px`，max-width `1440px`
- 页边距：≥1080px 用 `64px`；760–1080 用 `32px`；<760 用 `20px`
- 正文列宽 640px / 8 栏；全宽区块可到 1440

### 间距

`4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 / 128`

- 区块上下：96–160
- 标题 → 正文：24
- 段落之间：16
- 标签 → 标题：16–24

### 形状

- radius 0
- border `1px var(--line)`
- shadow none
- 允许的装饰：细分隔线、12 栏浅色网格线（透明度 5%）、8px 实心方块

### 响应式

| 断点 | 行为 |
|---|---|
| ≥1080 | 12 栏；H1 与侧栏并排 |
| 760–1079 | H1 占满；侧栏移到标题下方横排 |
| <760 | 单栏；导航只留 logo + 菜单；服务列表变行式；H1 最小 46px |

移动端：正文不小于 14px；不隐藏关键信息；CTA 保持 44px；无横向滚动。

---

## 6. 组件

### 导航

- 高 72px，底部 1px 线；左 logo（14px/600），中间链接（12.5px），右 CTA 描边按钮
- hover：链接下划线从左展开（scaleX 0→1，300ms）
- <760：隐藏链接，保留 logo + “菜单”文字按钮

```html
<header class="flex h-[72px] items-center justify-between border-b border-line">
  <a href="/" class="text-sm font-semibold tracking-tight">STUDIO NULL<sup class="text-[8px]">®</sup></a>
  <nav class="hidden gap-6 text-xs text-muted md:flex">
    <a href="#work" class="transition-colors hover:text-ink">作品</a>
    <a href="#about" class="transition-colors hover:text-ink">关于</a>
    <a href="#contact" class="transition-colors hover:text-ink">联系</a>
  </nav>
  <a href="#contact" class="inline-flex h-11 items-center border border-ink px-4 text-xs transition-colors hover:bg-ink hover:text-paper">
    开始项目 ↗
  </a>
</header>
```

### 按钮

- 高 44–48，padding `0 20px`，字号 13，radius 0
- Primary：墨色填充 + 纸色文字；hover 反转
- Secondary：1px 描边；hover 填充
- 禁止圆角、渐变、阴影；箭头放右侧

```html
<a class="inline-flex h-12 items-center gap-2 border border-ink px-5 text-[13px] font-medium
          transition-colors duration-200 hover:bg-ink hover:text-paper
          focus-visible:outline-2 focus-visible:outline-offset-2">
  开始项目 <span aria-hidden="true">↗</span>
</a>
```

### 链接

- 1px 下划线，offset 4px；hover 线加粗到 2px 或变强调色；箭头右移 4px

### 卡片

- 1px 边框，padding 24，radius 0，无阴影
- hover 只加深边框（墨色 30%），不位移、不放大

### 表单

- 标签 11px 大写 `+0.12em`
- 输入高 48，1px 边框；focus 2px 墨色 + offset 2
- 错误：文字 + 左侧 2px 红条，不能用颜色单独表意

### 标签 / Tag

- 10px 大写，1px 边框，padding `3px 8px`，无圆点

### 页脚

- 顶部 1px 线，四列；最后一行版权 + 年份，11px，muted

---

## 7. 动效

| Token | 值 |
|---|---|
| `--dur-fast` | `150ms` |
| `--dur` | `220ms` |
| `--dur-slow` | `420ms` |
| `--ease` | `cubic-bezier(.2,.8,.2,1)` |

### 编排

- 首屏：eyebrow 先出现，H1 两行遮罩上移（间隔 90ms）
- 滚动：每个区块只揭示一次，位移 12–16px + 透明度，stagger 60ms
- 链接：下划线 scaleX 300ms
- **戏剧化只允许一次**：一个 sticky 标题 + 三张图依次替换；其余保持静态
- 禁止视差、缩放 hover、自动轮播

### 降级

`prefers-reduced-motion: reduce` → 取消所有位移与遮罩，只保留瞬时透明度；内容必须完整可读。

---

## 8. 图像与图标

- 摄影：黑白或低饱和；4:5 / 1:1 / 3:2；直角裁切，不加圆角与阴影
- 没有图片时：用大字号 + 留白 + 一条线，不要用插画填充
- 图标：1.5px 描边、方形端点、16/20/24 三档；只用线性，不混填充
- 允许一个几何图形（圆 / 方 / 线）作为视觉锚点，一屏最多一个
- 禁止：3D、玻璃、渐变网格、emoji、iconfont

---

## 9. 文案

- 短句；名词和动词优先；标题 4–10 字
- 不用感叹号、不用“赋能 / 一站式 / 闭环”
- 英文标签全大写，2–3 个词

| 好 | 差 |
|---|---|
| 把复杂留给自己。 | 致力于为您提供一站式数字化解决方案。 |
| 让想法，落到屏幕上。 | 以创新驱动，赋能品牌增长。 |
| 少一点，准一点。 | 极致体验，由此开启！ |

---

## 10. Do / Don't

| Do | Don't |
|---|---|
| 12 栏对齐，留白 ≥48 | 用居中 flex 堆 hero |
| 一个暖红，≤3% 面积 | 红 / 蓝 / 绿三个强调色 |
| 1px 线分隔 | 卡片阴影 + 12px 圆角 |
| Inter 500 大字标题 | 800 粗黑 + 渐变文字 |
| 数字等宽 | 数字用衬线斜体 |
| 一处 Instrument Serif | 每个标题都换字体 |
| 150–250ms 位移 | 弹跳、旋转、视差 |
| 直角图片 | 圆角 + 投影的“高级感”模板 |

---

## 11. Tailwind v4

```css
@import "tailwindcss";

:root {
  --paper: #F2F0E9;
  --surface: #FBFAF5;
  --ink: #141414;
  --muted: #6B6B63;
  --line: #D8D6CE;
  --accent: #D9482B;
  --accent-ink: #FFFFFF;
}

[data-theme="dark"] {
  --paper: #121211;
  --surface: #1A1A18;
  --ink: #F2F0E9;
  --muted: #9C9C92;
  --line: #2E2E2A;
  --accent: #FF6A4D;
  --accent-ink: #121211;
}

@theme inline {
  --color-paper: var(--paper);
  --color-surface: var(--surface);
  --color-ink: var(--ink);
  --color-muted: var(--muted);
  --color-line: var(--line);
  --color-accent: var(--accent);

  --font-sans: "Inter", "PingFang SC", "Hiragino Sans GB", sans-serif;
  --font-serif: "Instrument Serif", "Songti SC", serif;

  --text-display: clamp(3.5rem, 8.3vw, 7.625rem);
  --text-display--line-height: 0.98;
  --text-display--letter-spacing: -0.04em;

  --text-h2: clamp(2rem, 4.6vw, 3.5rem);
  --text-h2--line-height: 1.05;
  --text-h2--letter-spacing: -0.03em;

  --radius-none: 0px;
}
```

Tailwind v3：把同样的值放进 `theme.extend.colors / fontFamily / fontSize`，颜色写 `var(--paper)` 即可支持 `[data-theme="dark"]`。

---

## 12. 给 AI 的 prompt（可直接粘贴）

```
Build a Swiss-minimal [page type] for [audience].
Read DESIGN.md and treat it as a hard constraint.

Non-negotiables:
- 12-column grid, max-width 1440px, 24px gutters, 0 radius, 1px hairlines, no shadows.
- Palette: paper #F2F0E9, ink #141414, muted #6B6B63, line #D8D6CE, one accent #D9482B (≤2% of surface).
- Type: Inter everywhere; display 500–600, tracking -0.04em Latin / -0.02em CJK;
  labels 10–11px uppercase +0.12em; at most one Instrument Serif accent per viewport.
- No gradients, glass, glow, emoji, icon fonts, or rounded cards.
- Motion: 150–250ms translate/opacity only; respect prefers-reduced-motion.
- Mobile: single column ≤760px, 44px targets, no horizontal scroll.

Output semantic HTML + Tailwind v4, mobile-first, with visible focus states.
```

---

## 13. 验收清单

- [ ] 圆角全部 0，阴影全部 none
- [ ] 只有一种强调色，面积 ≤3%，正文未使用强调色
- [ ] 正文对比度 ≥4.5:1，大字 ≥3:1（暗色模式单独测）
- [ ] 字号全部来自 §4 阶梯
- [ ] 中文标题字距 -0.02em，英文 -0.04em
- [ ] 数字 tabular-nums
- [ ] 焦点环可见，键盘可完成主流程
- [ ] 触控目标 ≥44px
- [ ] 760px 下无横向滚动，CTA 仍可见
- [ ] reduced-motion 下无位移，内容完整
- [ ] Instrument Serif 每屏 ≤1 处
- [ ] 没有渐变 / 玻璃 / emoji / 3D

---

变更记录：v1.0 — 初版，基于 style-probe S1。
