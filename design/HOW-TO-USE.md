# 怎么用这些 DESIGN.md

一句话：**它不是组件库，是一份“约束文件”。** 你把它交给 AI，让 AI 在写代码时不能自由发挥；你负责验收。

```
选 1 份文档  →  放进项目  →  分 5 步让 AI 写  →  按清单验收  →  再迭代
```

---

## 最短路径（就在对话里用）

1. 打开你选中的 `design/xxx/DESIGN.md`，全选复制。
2. 新开一个对话，粘贴，并加一句：

```
这是硬约束，不是参考。先复述 §2 的 10 条规则，然后等我给任务。
```

3. 它复述完，再按下面的 Step 1–5 提需求。每轮开头都加一句「继续遵守 DESIGN.md」。

如果你用的是 Claude Code / 本 Harness 这类能读本地文件的工具，第 1 步可以省掉，直接说「先读 design/swiss/DESIGN.md」。

---

## 0. 先选一份，只选一份

| 项目 | 选 |
|---|---|
| 设计师 / 工作室作品集 | `swiss` 或 `neoclassic` |
| 品牌官网、文化机构 | `neoclassic` 或 `swiss` |
| 活动页、产品发布、独立品牌 | `brutalist` 或 `collage` |
| 音乐 / 游戏 / 开发者活动 | `glitch` |
| 杂志、展览、H5 传播 | `collage` |

**不要**把五份都放进同一个项目。AI 会混着抄，最后既不是 A 也不是 B。

---

## 1. 放进项目

```text
my-site/
├─ design/
│  └─ DESIGN.md        ← 把你选中的那份复制过来，改名
├─ app/
│  ├─ globals.css
│  ├─ layout.tsx
│  └─ page.tsx
└─ package.json
```

- 保留文件名 `DESIGN.md`（AI 对这个名字有先验，知道它是规范）。
- 文档里 `../../style-probe-2.html` 的链接只在文档库里有意义，进项目后可以删掉那一行。

---

## 2. 用哪个工具

| 工具 | 怎么给文档 | 注意 |
|---|---|---|
| **Claude Code / 本 Harness** | 文档放进项目，直接说「先读 design/DESIGN.md」 | 它能自己读文件，不用粘贴 |
| **Cursor** | `@DESIGN.md` 引用；或加进 `.cursor/rules` | Rules 会常驻上下文，适合长期项目 |
| **ChatGPT / Claude 网页版** | 第一轮上传文件，或整段粘贴 | 之后每轮都提醒「按 DESIGN.md」 |
| **v0 / Lovable / Bolt** | 只贴文档的 §12 prompt + §2 硬规则 | 上下文有限，别贴整份 |

关键动作：**第一句话必须是“先读 DESIGN.md，把它当硬约束”**。不要先描述需求再补一句“参考一下”，顺序反了，AI 会按自己的默认审美先入为主。

---

## 3. 分 5 步写，不要一次生成整站

一次生成整页，AI 会在细节上全面妥协。按阶段来，每步都能验收。

### Step 1 — Token 层

```text
先读 design/DESIGN.md，把 §2 Hard rules 当作不可协商。
这一步只做 token，不写任何组件：
1. app/globals.css：用 @theme inline 定义 §11 里的颜色、字体、字号、阴影。
2. 不要新增文档里没有的颜色或字号。
3. 输出后，逐条对照 §3 和 §4，列出你实际用的值。
```

验收：打开 `globals.css`，颜色值与 §3 完全一致；没有多出来的 `--blue-500`。

### Step 2 — 页面骨架

```text
只写结构和布局，不加视觉细节：
- 语义化 HTML（header/nav/main/section/footer）
- 按 §5 的栅格、间距、断点
- 文案用我给的，不要自己编
- 不写 hover、动效、装饰
```

验收：390 / 820 / 1440 三个宽度截图，看有没有横向滚动、内容是否按断点重排。

### Step 3 — 组件

```text
现在实现 §6 里的组件，一次一个：导航 → 主按钮 → 卡片 → 表单。
每个组件必须包含 hover / focus-visible / active / disabled 状态。
样式只能用 Step 1 的 token，不要写任意值（如 text-[17px]）。
```

验收：键盘 Tab 一遍，焦点环可见；按钮高度 ≥44px。

### Step 4 — 动效

```text
按 §7 加动效：只用文档里的 duration / easing。
必须支持 prefers-reduced-motion，并在代码里写出来。
不要加视差、缩放、鼠标跟随。
```

验收：DevTools → Rendering → Emulate `prefers-reduced-motion: reduce`，页面应完全静止且内容完整。

### Step 5 — 验收

把 §13 清单贴给 AI：

```text
对照 DESIGN.md §13 逐条审计当前代码。
输出表格：条目 | 通过/不通过 | 证据（file:line）。
先不要改代码，只报告。
```

报告出来后，再让它按“不通过”的条目逐项修。**先审计再修**，比让它“顺便优化一下”可靠得多。

---

## 4. 常见跑偏与纠正话术

AI 的训练先验非常强：圆角、阴影、渐变、居中大标题。发现就跑偏时，直接引用规则编号，不要描述感觉。

| 症状 | 直接说 |
|---|---|
| 加了圆角 / 阴影 | “违反 Hard rule 1/2：radius 0、shadow none。全项目搜出来改掉，列出每个文件。” |
| 多出颜色 | “只用 §3 的颜色。把 `#xxxxxx` 换成对应变量，列出替换清单。” |
| 字号乱 | “只能取 §4 的阶梯。把所有 `text-[..]` 映射到 token。” |
| 移动端横向滚动 | “390px 有横向溢出。按 §5 修，并说明是哪个元素撑破的。” |
| 动效过头 | “时长超过上限。只保留 opacity/translate，去掉视差和缩放。” |
| 全页居中堆叠 | “首屏必须按 §6 的结构，不要用居中 flex 堆。” |
| 自己发明组件 | “文档里没有的组件不要加；需要就先问我。” |

如果 AI 连续两轮不听话：**新开一个会话**，重新贴文档 + 当前代码，别在脏上下文里继续拉扯。

---

## 5. 字体怎么接

### 普通 HTML

用 README 里的 Google Fonts `<link>`；离线或想本地化时，把 `assets/fonts/` 整个复制到 `public/fonts/`，再引用：

```html
<link rel="stylesheet" href="/fonts/fonts.css">
```

（`fonts.css` 已经写好 9 个 `@font-face`，中文仍然走系统字体。）

### Next.js（推荐 `next/font`，下面以新古典为例）

```tsx
// app/layout.tsx
import { Inter, Cormorant_Garamond } from "next/font/google";

const inter = Inter({ subsets: ["latin"], variable: "--font-inter", display: "swap" });
const cormorant = Cormorant_Garamond({
  subsets: ["latin"],
  weight: ["400", "500", "600"],
  style: ["normal", "italic"],
  variable: "--font-cormorant",
  display: "swap",
});

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="zh-CN">
      <body className={`${inter.variable} ${cormorant.variable}`}>{children}</body>
    </html>
  );
}
```

```css
/* globals.css */
@theme inline {
  --font-sans: var(--font-inter), "PingFang SC", "Hiragino Sans GB", sans-serif;
  --font-display: var(--font-cormorant), "Songti SC", serif;
}
```

离线环境（或不想让构建依赖 Google）：把 `assets/fonts/` 里的 woff2 放进 `public/fonts/`，改用 `next/font/local`。中文不要下载整包，直接用系统 PingFang SC / Songti SC。

---

## 6. 验收时到底看什么

1. **三张截图**：390 / 820 / 1440。手机看溢出和字号，平板看断点，桌面看留白。
2. **对比度**：DevTools 选中文字 → 颜色选择器会显示 ratio；正文 ≥4.5，大字 ≥3。
3. **键盘**：Tab 走一遍，焦点环不能被 `outline: none` 干掉。
4. **减少动态效果**：DevTools Rendering 面板模拟，页面应静止。
5. **暗色模式**（如果做了）：单独测一遍对比度，不要假设亮色值能复用。
6. **清单**：§13 全部打勾，缺一项都不算完成。

---

## 7. 什么时候改文档

- 项目里出现了文档没覆盖的组件 → 先补文档，再写代码。
- 同一条规则被违反三次 → 说明规则写得不够具体，改写它。
- 改完在文末加一行 changelog，并升版本号。
- 不要在项目里偷偷改 token；改了就同步回 `design/` 的母版。

---

## 8. 最容易犯的三个错

1. **一次生成整站**：细节全丢。分阶段。
2. **把五份文档一起喂**：风格互相污染。一次一份。
3. **只让 AI 自查，不自己看截图**：AI 会说“已完成”，但圆角和阴影还在。截图 + 清单，自己过一遍。
