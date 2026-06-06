# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static single-page website for the **West Seattle Golf Club (WSGC)** — a member-run golf club community (not affiliated with course management). The site itself is a single self-contained file, `index.html`; the repo also carries `README.md` (overview), `TECH.md` (developer reference), a `media/` directory of photos, and a `newsletters and minutes/` directory of club documents.

## Architecture

`index.html` is a self-contained, ~2630-line file with three parts (line numbers approximate — they drift as content is added):

1. **CSS** (lines ~9–1562): All styles inline in `<style>` tag. Organized by section with comments like `/* ===== NAVIGATION ===== */`.
2. **HTML** (lines ~1565–2542): Page structure with these sections in order:
   - `nav` — fixed navbar with scroll-triggered background change and mobile hamburger
   - `.hero` — full-viewport hero with animated fade-in content
   - `#about` — club history, stats grid, board of directors cards
   - `#course` — course info with hole cards in a scrollable carousel
   - `#membership` — membership tiers (Individual, Family, Junior)
   - `#events` — tournament schedule cards
   - `#gallery` — touch/drag swipeable photo gallery carousel
   - `#news` — news/update article cards
   - `#contact` — contact form + info
   - `footer`
3. **JavaScript** (lines ~2543–2632): Inline `<script>` tag with the handlers below. Note a Cloudflare `email-decode.min.js` script is auto-injected at the top of this block (CDN-added, not part of the source) — ignore it when editing.
   - Nav scroll handler (adds `.scrolled` class)
   - Mobile nav toggle (`toggleNav()`, `closeNav()`)
   - Carousel scroll (`scrollCarousel(id, dir)`)
   - Touch/drag swipe for gallery
   - Scroll reveal (IntersectionObserver on `.reveal` elements)
   - Smooth scroll for nav links

## Design System

CSS custom properties defined in `:root`:
- Colors: `--navy` (#0a1628), `--forest` (#1a4d2e), `--gold` (#a8852a), `--cream` (#f7f5f0)
- Typography: Playfair Display (headings/serif), Bebas Neue (display/numbers), Source Sans 3 (body) — all loaded from Google Fonts

## Development

No build tools, package manager, or dependencies. Open `index.html` directly in a browser or serve with any static file server:

```bash
python3 -m http.server 8000
# or
npx serve .
```

## Key Conventions

- All CSS uses the CSS custom properties (never hard-coded colors)
- Section structure: `section-label` (small caps) → `section-title` (Playfair Display) → `section-desc`
- Interactive cards use `hover` with `translateY(-4px)` lift and border-color transitions
- Scroll-reveal animations use `.reveal` class with IntersectionObserver
- Mobile breakpoint is at `@media (max-width: 768px)`
