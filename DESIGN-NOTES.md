# abdulmir-v2 — design notes (duplicate of david.kjelkerud.com)

Static site, no build step. Serve with `npx serve .` (clean URLs: `/work` → `work/index.html`).

## Structure (Abdul's version)
- `index.html` — home: top-bar (bold `@creativesoldr` wordmark → `/`, nav: about / work / blog), carousel photo, short intro, contact nav (contact / linkedin / instagram / x)
- `about/index.html` — article layout with the copy from abdulmir.com/about.html (h1, paragraphs, h2 sections, list, end photo)
- `work/index.html` — text-only list in the 660px column: `.project` blocks = h2 (favicon + title, links to the detail page; hover = black underline, no color change), description, then small gray `.years` date line (16px, not italic). No media on the list page. Order: favorite, human delta, built by abdul, combat / mir (same order in every detail page's `nav.work` footer). "output" is kept in the source inside an HTML comment (`<!-- hidden for now`).
- Detail pages (article layout after david.kjelkerud.com/work/*): `work/favorite/`, `work/human-delta/`, `work/built-by-abdul/`, `work/combat/`. Copy is deliberately short and plain (Abdul asked for no fluff / no AI-sounding text). Favorite makes no mention of a cofounder.
  - favorite: copy + media from ahunbaev.com/work/favorite (two autoplay videos, five site shots)
  - combat: Mir Studio tech packs (28 pages rendered from the Drive PDF → `techpacks/`) and Combat Journal Vol. I (68 pages from ahunbaev.com → `journal/`), both in a horizontal scroll-snap `.strip` with prev/next buttons and a page counter
  - human delta: written for a stranger — "In 3 months I shipped" list, then The audit tool / Outbound / Dinners / Ads / Automations / Handoff, in plain language with the numbers. Sourced from the Human-Delta-LeadMagnet repo docs (gtm-onboarding-aug-2026.md); public-safe only — no pricing, deal states, prospect/contact names. The two screenshots sit side by side in a `.pair` grid (stacks on mobile) and open in a `.lightbox` on click (Escape / click closes).
  - built by abdul: about-page story + n8n creator profile (9 templates, 74k+ uses), hero is a crop of the n8n profile
- "blog" nav item links out to https://abdulmirr.substack.com/ (original "photos" page removed)
- `site.css` — all styles (single file). Wordmark under `.top-bar .logo-link`: leerob.com treatment (local Iowan Old Style Bold, Palatino/Georgia fallback, -0.02em, #282828, hover opacity .72) at 28px desktop / 22px mobile
- Favicons (`favicon-16/32`, `apple-touch-icon`) generated from `abdul-pfp.jpg`
- `_reference/original/` — raw HTML/CSS as scraped, untouched

## Typography
- Font: **Minion 3** (Adobe, `minion-3-1`), regular 400 + italic 400. Original loads via Typekit kit `byd3dcy`;
  here it's self-hosted from `fonts/*.woff2` via `@font-face` at the top of `site.css`.
  NOTE: Minion 3 is a licensed Adobe font — for production either use your own Adobe Fonts kit
  (swap the `@font-face` block for `<link rel="stylesheet" href="https://use.typekit.net/XXXX.css">`)
  or a free stand-in (closest: Crimson Pro / EB Garamond / Source Serif 4).
- body: 20px / line-height 1.5, `-webkit-font-smoothing: antialiased`, color #333
- h1 60px, h2 40px, h3 30px, weight 400, line-height 1.3
- captions 16px gray, centered, not italic
- mobile (≤768px): body 16px, h1 40px, h2 25px

## Colors (CSS vars in :root)
- text `--core-black #333333` · muted `--core-gray #808080`
- accent: the var is still named `--core-blue` but is now abdulmir.com red `#b31d1d`; link underline `--core-light-blue` = `#f3dcdc`, `--core-middle-blue` = `#ecc9c9`
- `--core-light-gray #E7E7E7` · `--core-ultralight-gray #F9F9F9`
- the original's violet image wash (`--core-wash`) is no longer used as a background: `.image-background` and `.strip-container` are transparent, media sits on white with the `.image-box` shadow

## Layout
- `.main-container` max 1280px, padding 20px 20px 80px
- widths: `--viewport-max 1280px`, `--viewport-half 768px` (was 960), `--viewport-para 660px` (all text blocks); `.image-container` capped at 1024px, `.video-container` / `.image-container-small` at 768px — media is ~20% narrower than the original
- `.top-bar` flex space-between, margin 60px auto (30px mobile); nav gap 10px 30px, gray links, selected = black + 1px bottom border
- `.intro-section` / `.headshot` max 512px, margin 100px auto (60px mobile)
- p margin 30px 0 (20px mobile); `--item-margin 80px auto` (30px mobile) for images/galleries
- links: no underline, 1px light-blue bottom border → blue on hover
- single breakpoint: 768px

## Home photo
- `abdul-carousel.jpg` in a `.polaroid` frame copied from myfavoriteapp.com (white, 5.5% sides / 15% bottom, soft shadow). Straight at rest; hover lifts 8px and tilts -1.2°. 270px wide, centered.

## Logo
- Original had an animated hand sprite (`ani-logo3.png` + `logo.js`) — replaced with the `@creativesoldr` text wordmark.
- Wordmark uses Iowan Old Style (system font on macOS/iOS, same as leerob.com) so it gets a true bold; other platforms fall back to Palatino Linotype / Georgia.
