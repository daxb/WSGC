# West Seattle Golf Club Website

The official website for the **West Seattle Golf Club (WSGC)** — a member-run community organization for golfers at West Seattle Golf Course. The club is independent and not affiliated with course management.

## Overview

This is a static single-page website built with no frameworks or build tools. Everything lives in one self-contained file (`index.html`) with inline CSS and JavaScript, making it trivially simple to deploy on any static host.

## Features

### Sections

| Section | Description |
|---------|-------------|
| **Navigation** | Fixed navbar with scroll-triggered background transition and mobile hamburger menu |
| **Hero** | Full-viewport landing area with staggered fade-in animations and CTA buttons |
| **About** | Club history, member stats, embedded YouTube video, scrollable history photo carousel, and board of directors |
| **Course** | Course overview, feature cards, and an expandable accordion of 18+ historical tidbits |
| **Events** | 2026 tournament schedule (17 events) with auto-scroll to the next upcoming event and a LiveTourney registration link |
| **Gallery** | Touch/drag swipeable photo carousel |
| **Membership** | Membership tiers (Individual, Family, Junior) with dues and a join CTA |
| **News** | Club announcements and newsletter highlights |
| **Contact** | Contact form and club contact details |

### Interactive Features

- Fixed navbar with scroll-triggered white/blur background
- Mobile slide-out navigation with overlay backdrop
- 3 horizontal carousels (history, events, gallery) with touch/drag and button navigation
- Expandable tidbits accordion (show/hide entire list + individual item toggle)
- Auto-scroll events carousel to the first upcoming 2026 event on load
- IntersectionObserver scroll-reveal animations on all major content blocks
- Smooth scroll for all in-page nav links
- Board of directors email links (mailto)

## Getting Started

No installation required. Serve the project root with any static file server:

```bash
# Python
python3 -m http.server 8000

# Node
npx serve .
```

Then open `http://localhost:8000` in a browser.

## Project Structure

```
WSGC/
├── index.html        # Entire website — CSS, HTML, and JS in one file
├── README.md         # This file
├── TECH.md           # Technical reference for developers
├── CLAUDE.md         # Guidelines for AI-assisted development
└── media/            # All images and PDFs used by the site
    ├── Fox Logo.png
    ├── DJI_20250603125429_0044_D.jpg   # Hero background (drone photo)
    ├── *.jpg / *.png                   # Course, event, and historical photos
    └── *.pdf                           # Bylaws and historical documents
```

## Design System

**Colors** (CSS custom properties):

| Variable | Value | Usage |
|----------|-------|-------|
| `--navy` | `#0f1f33` | Primary dark background |
| `--forest` | `#1a4d2e` | Green accent |
| `--gold` | `#a8852a` | Primary highlight/accent |
| `--cream` | `#f7f5f0` | Light section backgrounds |

**Fonts** (Google Fonts):

| Font | Weights | Usage |
|------|---------|-------|
| Playfair Display | 400, 700, 900 | Section headings and serif titles |
| Bebas Neue | 400 | Display numbers, stats, logo |
| Source Sans 3 | 300–700 | Body text and UI copy |

## Media Assets

The `media/` directory contains 27 files including:

- **Historical documents**: 1936–1953 course materials, scorecards, newspaper articles, USGA award ceremony materials
- **Photography**: Course landscapes, drone photo, tournament and member event photos
- **Branding**: Fox logo (club mascot)
- **PDFs**: Current bylaws, historical documents

## Development Notes

- All colors must use CSS custom properties — never hard-code hex values
- All new sections should follow the `section-label → section-title → section-desc` pattern
- Interactive cards use `translateY(-4px)` on hover with a border-color transition
- Mobile breakpoint is `768px`; a secondary breakpoint exists at `1024px`

See [TECH.md](TECH.md) for a full technical reference.
