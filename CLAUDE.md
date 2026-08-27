# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Project Overview

Static personal website for abdulmir.com. Pure HTML and CSS, no build step. Deployed on Vercel (project `abdulmir.com`, linked via `.vercel/`); `CNAME` is kept for the custom domain. Design is a close adaptation of david.kjelkerud.com — see `DESIGN-NOTES.md` for the full design system (fonts, sizes, colors, spacing, components).

## Structure

- `index.html` — home: `@creativesoldr` wordmark + nav (about / work / blog), photo, two-line intro, contact links
- `about/index.html` — about page (`.page-about` class scopes its 36px headings)
- `work/index.html` — text-only project list; `work/<slug>/index.html` detail pages: `favorite`, `human-delta`, `built-by-abdul`, `combat`
- `resume.html` — redirect to the Google Drive resume
- `site.css` — the single stylesheet; `fonts/` — self-hosted Minion 3 (licensed Adobe font); `icons/` — project icons
- Media lives next to its page (`work/combat/journal/`, `work/combat/techpacks/`, `work/favorite/`, `work/human-delta/`)

## Conventions

- All asset paths are absolute (`/site.css`, `/work/...`) so pages work at any depth.
- Nav "blog" links out to Substack; project pages end with a `nav.work` footer listing all four projects in the same order as the work page.
- Copy is short and plain; no em dashes in body text where a colon or period works.
- Detail-page media: `.strip` (horizontal scroll-snap with prev/next) for many images, `.pair` (two side by side, click to enlarge via `.lightbox`) for two.

## Performance rules

- Images are WebP, sized to 2x their largest display width (home photo 540px, article images 1024–1320px, strip pages 1024px tall, icons 96px), encoded with `sharp` at quality 75–82. Never commit a raw camera JPEG or PNG screenshot; convert first (`npm i sharp` in a scratch dir, `sharp(src).resize({width}).webp({quality}).toFile(out)`).
- Every `<img>` carries `width`/`height`; below-the-fold images get `loading="lazy" decoding="async"`; the home photo gets `fetchpriority="high"`.
- Lightbox images use a separate larger file (`-1800.webp`) so the inline thumbnail stays small.
- Videos: `preload="none"` + play on scroll-in (see the Favorite page), not `autoplay`.
- The body font is preloaded on every page; `font-display: swap`.
- `vercel.json` sets long-lived `Cache-Control` for `/fonts` and media; HTML/CSS stay `must-revalidate`.

## Development

```
npx serve .
```
