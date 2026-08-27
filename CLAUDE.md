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

## Development

```
npx serve .
```
