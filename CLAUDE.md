# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static personal website for abdulmir.com. Hosted on GitHub Pages (CNAME: `abdulmir.com`). No build tools, no frameworks — pure HTML and CSS.

## Architecture

- **Pages**: `index.html` (home), `about.html`, `projects.html`, `chat.html`
- **Styles**: `style.css` is the active stylesheet linked by all pages. `styles.css` is an older version (has fade-in animation, `link-blue` instead of `link-red`) — not currently used.
- **Navigation**: All subpages use `← Back to home` link pointing to `index.html`. Home links to subpages via a two-column nav grid.
- **Chat page**: Embeds Cal.com inline scheduler (`cal.com/abdulmirr/freeconsultation`).
- **Projects page**: Has page-specific `<style>` block for project items (`.project-item`, `.project-title`, `.project-repo-link`, `.tech-stack-list`).

## Design System

- **Fonts**: Geist (headings/body), Geist Mono (subtitle, nav links), DM Sans (about/projects text). Loaded via Google Fonts CDN + local `@font-face` fallbacks.
- **Colors**: Zinc palette — `#18181b` (text), `#3f3f46` (body text), `#71717a` (muted), `#a1a1aa` (back link), `#e4e4e7` (separator). Red accent: `#b31d1d`.
- **Layout**: Centered `.container` with `max-width: 620px`. Subpages use `.page-about` for extra vertical padding.
- **Responsive**: Single breakpoint at `640px`. Nav grid collapses to single column on mobile.

## Development

No build step. Open any `.html` file directly in a browser, or use a local server:
```
npx serve .
```

## Website Design Recreation Workflow

When the user provides a reference image (screenshot) and optionally some CSS classes or style notes:

1. **Generate** a single `index.html` file using Tailwind CSS (via CDN: `<script src="https://cdn.tailwindcss.com"></script>`). Include all content inline unless requested otherwise.
2. **Screenshot** the rendered page using Puppeteer (`npx puppeteer screenshot index.html --fullpage`). Capture distinct sections individually too.
3. **Compare** screenshot against the reference image. Check: spacing/padding (px), font sizes/weights/line-heights, colors (hex), alignment, border radii/shadows, responsive behavior, image sizing.
4. **Fix** every mismatch. Edit the HTML/Tailwind code.
5. **Re-screenshot** and compare again.
6. **Repeat** steps 3-5 until within ~2-3px of the reference. Always do at least 2 comparison rounds.

### Defaults for Recreation
- Placeholder images from https://placehold.co/ when source images aren't provided
- Mobile-first responsive design
- Heroicons (via CDN) or inline SVG for icons
- If fonts aren't web-safe, use closest Google Fonts alternative
- Implement basic hover/active states for interactive elements

### Stopping Criteria
- Visual differences ≤2-3px across all sections
- Colors match within 5% tolerance (or exact if provided)
- Typography visually indistinguishable
- User explicitly approves
