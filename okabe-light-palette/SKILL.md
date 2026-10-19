---
name: okabe-light-palette
description: Scientific Okabe–Ito light-theme web and chart color system (cream background, 8 distinguishable series colors, CSS variables + chart PAL). Use when the user asks for "Okabe-Ito palette", "科研配色", "sci paper chart colors", "色盲友好图表配色", light-theme finance/dashboard charts, or to reuse the Xiaomi earnings page color scheme on other websites. Do NOT use for dark neon UI kits, brand-only recolors that ignore series distinction, or image generation color prompts.
---

# Okabe–Ito Light Palette

Proven light-theme system from a multi-series earnings dashboard: readable on cream backgrounds, high series distinction, colorblind-friendly (Okabe–Ito 8-color scientific palette).

## When to apply

- Multi-series bar / line / stacked charts on a **light** page
- Finance, research, or data dashboards needing 4–8 categorical colors
- User mentions Okabe–Ito, 科研色板, sci-paper charts, or this Xiaomi page style

## Core tokens (CSS)

```css
:root {
  --bg: #f7f1ec;
  --bg-soft: #fffaf6;
  --card: #fffdfb;
  --card-2: #faf4ef;
  --line: rgba(46, 44, 105, 0.10);
  --line-strong: rgba(46, 44, 105, 0.16);
  --ink: #111111;
  --ink-2: #333333;
  --ink-3: #666666;
  --accent: #d55e00;
  --accent-soft: rgba(213, 94, 0, 0.10);
  --ok: #009e73;
  --ok-soft: rgba(0, 158, 115, 0.10);
  --warn: #d55e00;
  --warn-soft: rgba(213, 94, 0, 0.10);
  --info: #0072b2;
  --info-soft: rgba(0, 114, 178, 0.10);
  --radius: 16px;
  --shadow: 0 10px 30px rgba(46, 44, 105, 0.08);
  --font: "Inter", "PingFang SC", "Microsoft YaHei", "Noto Sans SC", system-ui, sans-serif;
  --mono: "SF Mono", "JetBrains Mono", "Cascadia Code", ui-monospace, monospace;
}

body {
  color: var(--ink);
  background:
    radial-gradient(1100px 520px at 8% -8%, rgba(213, 94, 0, 0.08), transparent 55%),
    radial-gradient(900px 480px at 92% 8%, rgba(0, 114, 178, 0.08), transparent 50%),
    var(--bg);
  font-family: var(--font);
}
```

## Chart series palette (JS `PAL`)

Use **exactly** these for categorical series on light backgrounds. Keep order: primary metric first (orange), then blue, green, vermillion, purple-pink, sky.

| Role | Hex | Notes |
|------|-----|--------|
| bar / primary / 综合 | `#E69F00` | Okabe orange |
| line / YoY / 手机 | `#0072B2` | Okabe blue |
| IoT / 经营现金流 / 正向 | `#009E73` | Okabe bluish green |
| 互联网 / 次要系列 | `#CC79A7` | Okabe reddish purple |
| EV / 强调 / 负向警示 | `#D55E00` | Okabe vermillion |
| 其他 / 浅色填充 | `#56B4E9` | Okabe sky blue |
| 黄 | `#F0E442` | Use sparingly on light bg; prefer for dark accents |
| 黑 / 选中标签 | `#000000` | Axis labels selected |
| 暗色辅助 | `#666666` | Unselected labels |
| 正文 | `#111111` | |
| 网格 | `rgba(0,0,0,0.10)` | |
| 零线 | `rgba(0,114,178,0.28)` | |

```js
const PAL = {
  bar: "#E69F00",
  line: "#0072B2",
  series1: "#E69F00",
  series2: "#0072B2",
  series3: "#009E73",
  series4: "#CC79A7",
  series5: "#D55E00",
  series6: "#56B4E9",
  dim: "#666666",
  ink: "#111111",
  grid: "rgba(0,0,0,0.10)",
  zero: "rgba(0,114,178,0.28)",
};
```

## Mapping checklist (same as earnings page)

1. **营收/主指标柱** → orange `#E69F00`
2. **同比/折线** → blue `#0072B2`
3. **手机/系列 A** → blue `#0072B2`
4. **IoT/正向现金流** → green `#009E73`
5. **互联网/粉紫** → `#CC79A7`
6. **汽车/告警/负值强调** → vermillion `#D55E00`
7. **未选中季度** opacity ≈ 0.48–0.55 bars; **选中** ≈ 0.95 + darker label
8. Value labels above bars in `#111111` (selected) / `#666666` (idle); do not use pale fills on cream background

## UI chrome

- Cards: `#fffdfb` on `#f7f1ec`, border `rgba(46,44,105,0.10)`
- Active pill / tab: solid `#0072B2` or `#E69F00` with white text; **no transparent border** (causes 1px light seam)
- Controls height: outer 40px, inner chips 32px, `line-height: 1`
- Accent for brand strips: `#D55E00` vermillion

## Important

- Do **not** put light cream `#F0E442` or pale tints as text on light cards
- Do **not** reuse two purples or two roses in one chart
- Yellow `#F0E442` is low contrast on `#f7f1ec` — avoid as a main series on light theme
- For dark theme variants, lift luminance of the same hues; do not switch to neon orange/blue pairs

## Example

User: 「用科研配色画一个四季度营收 + 毛利率对比页」  
→ Apply `:root` tokens + map 营收 to `#E69F00`, 毛利率分部 to blue/green/purple/vermillion; cream page, white cards, dark ink.

User: 「暗色主题财报仪表盘」  
→ Reuse Okabe hues, raise brightness, keep cream ink `#F7E2DB` only if Kokomi-style; default remains this light kit unless they ask for dark.
