# text-to-elegant-image

> Turn Markdown or plain text into beautifully typeset, high-resolution long images (share cards / posters) — with 18 built-in visual styles.

Generates a self-contained HTML file and renders it to a crisp PNG via headless Chrome (Puppeteer). Designed for AI agents (OpenClaw / Claude Code / Cursor, etc.) as a skill, but the scripts also run standalone.

## Features

- **18 built-in visual styles** — Cyberpunk/Tech, Minimalist, Apple Premium, Cowork Light-Tech, Newspaper, Bloomberg Terminal, Ink Scroll, Steampunk, XiaoHongShu/REDNote, Morandi, Glassmorphism, Palace, Fresh, Earthy, Dreamy, Macaron, Carbon, Vivid.
- **High-DPI output** — 2× `deviceScaleFactor` for retina-sharp PNGs.
- **Auto height cropping** — measures the real content height and trims trailing whitespace precisely.
- **No external assets** — icons are pure CSS/inline SVG; nothing loads over the network, so rendering never breaks.
- **Cross-platform Chrome detection** — Linux / macOS / WSL, no manual config.
- **Configurable output dir** — via `T2EI_OUTPUT_DIR` env var (defaults to `./output`).
- **Footer control** — default footer, custom author line, or no footer.

## Requirements

- **Node.js** ≥ 18
- **Chrome / Chromium** (any recent build; auto-detected)
- **puppeteer-core** (installed on first run via `setup.sh`)

## Quick Start

```bash
# Clone
git clone https://github.com/Songhonglei/text-to-elegant-image.git
cd text-to-elegant-image

# Install dependency (puppeteer-core)
bash scripts/setup.sh

# Render an HTML file to PNG
node scripts/export_image.js /path/to/page.html ./output/card.png 600
```

As an AI-agent skill, point your agent at `SKILL.md` — it describes the full workflow (parse content → pick a style from `resources/styles_reference.md` → generate HTML → screenshot).

## Output directory

Resolved in this priority order:

1. Path passed explicitly on the command line
2. `T2EI_OUTPUT_DIR` environment variable
3. Default: `./output`

```bash
export T2EI_OUTPUT_DIR="$HOME/my-images"   # optional, persist in ~/.bashrc
```

## Styles

All 18 styles ship with complete CSS + HTML skeletons in [`resources/styles_reference.md`](./resources/styles_reference.md). Each uses a `.container` base plus a namespaced class set (e.g. `.mo-*` for Morandi, `.gl-*` for Glass), so styles never collide.

> ⚠️ **No emoji in generated HTML** — headless Chrome lacks color-emoji fonts and renders them as tofu boxes. Use CSS shapes / inline SVG instead. (Enforced in `SKILL.md`.)

## Image delivery

This open-source edition focuses purely on **text → elegant image** generation and returns a local PNG path. Auto-pushing images to IM channels (WeChat / Telegram / Slack, etc.) is **not built in** — wire up your platform's Bot/API downstream if you need it (optional adapters may come in a future version).

## Install in your AI agent

| Agent | Install |
|---|---|
| OpenClaw | `clawhub install text-to-elegant-image` |
| Claude Code | Manual: copy to `~/.claude/skills/` |
| Cursor | Manual: copy to `.cursor/skills/` |

## License

MIT — see [LICENSE](./LICENSE).

## Author

Evan Song · [github.com/Songhonglei](https://github.com/Songhonglei)

## Changelog

### v1.0.0 (2026-07-13)

- Initial public release: 18 visual styles, high-DPI headless-Chrome rendering, configurable output dir.

---

## Appendix: Style Gallery / 附录：样式画廊

Below are rendered samples of all 18 built-in styles. Each is generated from the same content with a different style applied.

以下是全部 18 种内置样式的渲染示例。每张图使用相同内容、套用不同样式生成。

### 1. Cyberpunk / 赛博科技风
> Dark background, neon glow, SVG honeycomb grid — for AI reports, tech analysis, bold posters.
> 深色霓虹发光、SVG 蜂窝网格 — 适合 AI 报告、科技分析、炫酷海报。

![Cyberpunk 赛博科技风](./assets/01-cyberpunk.png)

### 2. Minimalist / 极简优雅风
> White background, serif type, generous whitespace — for essays, journals, humanities.
> 白底衬线、大量留白 — 适合随笔、日记、人文知识。

![Minimalist 极简优雅风](./assets/02-minimalist.png)

### 3. Apple Premium / 苹果质感风
> Light gray, frosted-glass cards, colored window controls — for tools, recaps, methodology.
> 浅灰毛玻璃卡片、彩色窗口按钮 — 适合效率工具、复盘总结、方法论。

![Apple 苹果质感风](./assets/03-apple.png)

### 4. Cowork Light-Tech / Cowork 轻科技风
> Apple gray-white with accent blue, frosted hero, neural-node motifs — for internal sharing, product handbooks.
> 苹果灰白 + 点缀蓝、磨砂 Hero、神经网络节点 — 适合内部分享、产品手册。

![Cowork 轻科技风](./assets/04-cowork.png)

### 5. Newspaper / 报纸杂志风
> Cream paper, letterpress grain, black-and-white print — for history, timelines, deep narratives.
> 米黄纸感、铅字颗粒、黑白印刷 — 适合历史事件、时间轴、深度叙事。

![Newspaper 报纸杂志风](./assets/05-newspaper.png)

### 6. Bloomberg Terminal / Bloomberg 终端风
> Dark terminal, data rows, monospace numerics — for finance, data dashboards, market reviews.
> 深色终端、数据行、等宽数字 — 适合金融、数据看板、行情复盘。

![Bloomberg 终端风](./assets/06-bloomberg.png)

### 7. Ink Scroll / 水墨卷轴风
> Rice-paper tone, ink strokes, seal stamp — for classical culture, poetry, calligraphy themes.
> 宣纸色调、水墨笔触、印章 — 适合古典文化、诗词、书法主题。

![Ink Scroll 水墨卷轴风](./assets/07-ink-scroll.png)

### 8. Steampunk / 蒸汽朋克风
> Brass gears, rivets, pipe dividers — for mechanical, retro-tech, worldbuilding content.
> 黄铜齿轮、铆钉、管道分隔 — 适合机械、复古科技、世界观设定。

![Steampunk 蒸汽朋克风](./assets/08-steampunk.png)

### 9. XiaoHongShu / 小红书风
> White base, coral red, rounded note cards — for lifestyle notes, tips, share cards.
> 白底珊瑚红、圆角笔记卡片 — 适合生活笔记、种草、分享卡片。

![XiaoHongShu 小红书风](./assets/09-xiaohongshu.png)

### 10. Morandi / 莫兰迪高级灰风
> Muted warm grays, low saturation — for elegant, understated, high-end presentation.
> 低饱和暖灰、高级感 — 适合优雅内敛、高端呈现。

![Morandi 莫兰迪高级灰风](./assets/10-morandi.png)

### 11. Glassmorphism / 玻璃拟态风
> Colorful gradient background, backdrop-blur translucent cards — for modern, fresh UI.
> 彩色渐变背景、毛玻璃半透明卡片 — 适合现代清爽界面。

![Glassmorphism 玻璃拟态风](./assets/11-glassmorphism.png)

### 12. Palace / 故宫风
> Deep base, gold-and-vermilion, calligraphy fonts, square corners — for Chinese-classical, cultural themes.
> 深底金红、书法字体、方角 — 适合国风、文化主题。

![Palace 故宫风](./assets/12-palace.png)

### 13. Fresh / 清新自然绿风
> Light greens, natural tones — for health, wellness, nature, eco topics.
> 浅绿自然色调 — 适合健康、养生、自然、环保主题。

![Fresh 清新自然绿风](./assets/13-fresh.png)

### 14. Earthy / 大地原木风
> Warm earth tones, wood texture — for handmade, coffee, slow-living, craft content.
> 温暖大地色、原木质感 — 适合手作、咖啡、慢生活、匠心内容。

![Earthy 大地原木风](./assets/14-earthy.png)

### 15. Dreamy / 优雅紫梦幻风
> Purple gradients, dreamy soft glow — for beauty, aesthetics, romantic themes.
> 紫色渐变、梦幻柔光 — 适合美妆、美学、浪漫主题。

![Dreamy 优雅紫梦幻风](./assets/15-dreamy.png)

### 16. Macaron / 马卡龙粉彩风
> Pastel candy colors — for desserts, kids, cute, playful content.
> 马卡龙粉彩糖果色 — 适合甜品、亲子、可爱、俏皮内容。

![Macaron 马卡龙粉彩风](./assets/16-macaron.png)

### 17. Carbon / 暗色极简风
> Deep dark base, high-contrast minimal — for technical docs, code, developer content.
> 深色极简、高对比 — 适合技术文档、代码、开发者内容。

![Carbon 暗色极简风](./assets/17-carbon.png)

### 18. Vivid / 活力渐变风
> Tri-color gradient (purple-pink-orange), gradient-clip text — for events, campaigns, energetic promos.
> 三色渐变（紫粉橙）、渐变文字 — 适合活动、campaign、活力宣传。

![Vivid 活力渐变风](./assets/18-vivid.png)
