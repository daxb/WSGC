# WSGC Technical Reference

Developer documentation for the West Seattle Golf Club website. See [README.md](README.md) for a general overview.

## Architecture

The entire site is a single self-contained file: **`index.html`**.

| Part | Approx. Lines | Description |
|------|--------------|-------------|
| CSS | Top ~1,460 | All styles in one `<style>` tag |
| HTML | ~1,460–2,200 | Page structure and content |
| JavaScript | Last ~80 | Inline `<script>` tag |

No build step, no bundler, no package manager. Dependencies are limited to Google Fonts loaded via CDN.

---

## CSS Architecture

### Custom Properties

All colors and most reusable values are defined as CSS custom properties on `:root`. **Never use hard-coded hex values.**

**Color palette:**

| Variable | Value | Role |
|----------|-------|------|
| `--navy` | `#0f1f33` | Primary dark background |
| `--navy-mid` | `#132240` | Mid-tone navy |
| `--navy-light` | `#1a3058` | Lighter navy |
| `--forest` | `#1a4d2e` | Green accent |
| `--forest-light` | `#2a7a47` | Light green |
| `--forest-accent` | `#1a6b38` | Accent green |
| `--gold` | `#a8852a` | Primary highlight |
| `--gold-light` | `#c8a95e` | Light gold |
| `--cream` | `#f7f5f0` | Light section backgrounds |
| `--white` | `#ffffff` | Pure white |
| `--text-dark` | — | Dark body text |
| `--text-body` | — | Standard body text |
| `--text-muted` | — | Subdued/secondary text |

### Section Naming Convention

Every content section follows this pattern:

```html
<span class="section-label">Small caps label</span>
<h2 class="section-title">Playfair Display Heading</h2>
<p class="section-desc">Supporting description text</p>
```

### Animation Keyframes

| Name | Duration | Effect |
|------|----------|--------|
| `heroFadeIn` | 1.5s ease-out | Staggered fade-in for hero elements (0.3s–1.1s delays) |
| `scrollBounce` | 2s infinite | Bounce animation on the hero scroll indicator |

Hover transitions: `0.3s–0.6s` for card lifts, border colors, and opacity.
Scroll reveal: `0.8s` fade + `translateY` via `.reveal` → `.visible` class toggle.

### CSS Section Comments

The stylesheet is organized with block comments in the form:

```css
/* ===== SECTION NAME ===== */
```

Sections in order: BASE, TYPOGRAPHY, NAVIGATION, HERO, SECTIONS, ABOUT, COURSE, MEMBERSHIP, EVENTS, GALLERY, NEWS, CONTACT, FOOTER, SCROLL REVEAL, MOBILE.

### Interactive Card Pattern

All interactive cards use:

```css
.card:hover {
  transform: translateY(-4px);
  border-color: var(--gold);
  transition: 0.3s ease;
}
```

---

## HTML Sections

### `<nav>`

- Fixed at top; `z-index` above all content
- `.nav-logo`: Bebas Neue "WSGC" text + fox icon image
- `.nav-links`: Horizontal list with smooth-scroll anchors; gains `.open` class on mobile
- `.hamburger`: 3-bar icon, visible only on mobile (`<= 768px`)
- `.nav-overlay`: Full-screen semi-transparent backdrop shown when mobile nav is open
- Gains `.scrolled` class when `window.scrollY > 50`, triggering white+blur background

### `#hero`

- Full-viewport (`100vh`) with a drone photograph background
- Layered gradient overlays applied via CSS for depth
- Animated badge: "Est. 1940 · West Seattle, Washington"
- Main heading uses `<em>` for gold italic accent
- Two CTA buttons linking to `#membership` and `#events`
- Scroll indicator with `scrollBounce` animation

### `#about`

- 2-column grid (image + content) on desktop, stacked on mobile
- **Stats grid**: 4 items using Bebas Neue for the numbers
- **YouTube embed**: Responsive `<iframe>` (1:1.78 aspect ratio wrapper)
- **History carousel** (`.history-carousel`): Horizontal scroll of 9 historical images with captions; navigated with `scrollCarousel()`
- **Board of Directors**: 6-card grid — President, Vice President, Treasurer, Secretary, Tournament Director, Membership Chair — each with a `mailto:` email link

### `#course`

- Hero subsection with background image and link to the course's external website
- **Feature cards**: 6 cards in a responsive 3→2→1 column grid, numbered with Bebas Neue
- **Tidbits accordion**: 18+ expandable history facts
  - Entire list visibility toggled by "Show/Hide Tidbits" button (`toggleTidbits()`)
  - Individual items expand/collapse via `toggleTidbit()` with a `+` → `−` icon

### `#events`

- **LiveTourney banner**: External link to tournament registration platform
- **Events carousel** (`.events-carousel`): 17 event cards
  - Each card has a `data-date="YYYY-MM-DD"` attribute
  - Cards have emoji icons, gradient backgrounds, month/day badge, type label
  - On page load, the carousel auto-scrolls to the first event with a date >= today

### `#gallery`

- `.gallery-carousel`: Horizontal scroll container, 400px-wide items
- Touch/drag gesture support (see JS section)
- Hover overlay fades in caption text and date

### `#membership`

- 2-column layout: info blocks (left) + gradient CTA card (right)
- CTA card lists dues: Individual, Family, Junior with prices

### `#news`

- Featured article in a 2-column (image + text) layout
- Additional news cards with category tags

### `#contact`

- 2-column grid: contact form + contact info block
- Form fields: name, email, subject (select), message (textarea)

### `<footer>`

- Navy background, 4-column layout
- Columns: brand/description, Quick Links, Golf Links, Club Info
- Bottom bar: copyright, disclaimer, designer credit

---

## JavaScript Functions

All JavaScript lives in a single inline `<script>` tag at the bottom of `index.html`.

### Nav Scroll Handler

```javascript
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 50);
});
```

Adds `.scrolled` to `<nav>` when scrolled more than 50px, triggering the white+blur CSS transition.

### `toggleNav()`

Toggles `.open` on `.nav-links` and `.nav-overlay` to open/close the mobile sidebar menu.

### `closeNav()`

Removes `.open` from both `.nav-links` and `.nav-overlay`. Called on overlay click and nav link click.

### `toggleTidbit(header)`

Toggles `.open` on the parent `.tidbit-item` of the clicked header element. Used for individual accordion items in the Course section.

### `toggleTidbits(btn)`

Shows or hides the entire `.tidbits-list` container. Updates the button text between "Show Tidbits" / "Hide Tidbits" and toggles `aria-expanded`.

### `scrollCarousel(id, dir)`

```javascript
function scrollCarousel(id, dir) {
  const carousel = document.getElementById(id);
  const card = carousel.querySelector(':scope > *');
  const cardWidth = card.offsetWidth + 24; // 24px gap
  carousel.scrollBy({ left: dir * cardWidth, behavior: 'smooth' });
}
```

Smoothly scrolls any carousel by exactly one card width in the given direction (`1` = right, `-1` = left). Used by the events and history carousels.

### Touch/Drag Swipe Handler

Applied to both `.gallery-carousel` and `.events-carousel`:

- Tracks `mousedown` position as `startX`
- On `mousemove`, computes `walk = (x - startX) * 1.5` and sets `scrollLeft`
- Resets on `mouseup` / `mouseleave`
- Changes cursor between `grab` (idle) and `grabbing` (dragging)

### Events Carousel Auto-Scroll (IIFE)

Runs once on page load:

1. Collects all `.event-card` elements with a `data-date` attribute
2. Compares each date string to today's date
3. Finds the index of the first upcoming event
4. Calls `carousel.scrollBy()` to position that card at the left edge (minus one card for context)

### Scroll Reveal (IntersectionObserver)

```javascript
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) entry.target.classList.add('visible');
  });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

When a `.reveal` element enters the viewport (10% threshold), `.visible` is added, triggering the CSS `0.8s` fade + `translateY(0)` transition.

---

## Responsive Breakpoints

| Breakpoint | Behavior |
|------------|----------|
| `<= 1024px` | Course feature grid: 3 → 2 columns; some padding reductions |
| `<= 768px` | Primary mobile breakpoint: all multi-column grids become 1 column; hamburger nav active; hero text scales down; carousels adapt |

---

## External Dependencies

All loaded via CDN — no local font files.

| Dependency | Source | Usage |
|------------|--------|-------|
| Playfair Display (400, 700, 900) | Google Fonts | Section headings, serif titles |
| Bebas Neue (400) | Google Fonts | Display numbers, stats, logo |
| Source Sans 3 (300–700) | Google Fonts | All body and UI text |

---

## Media Assets

All assets live in the `media/` directory. The site references them with relative paths (e.g., `media/Fox Logo.png`).

**Categories:**

| Category | Description |
|----------|-------------|
| Historical documents | 1936 course naming proposal, 1940 opening materials, 1953 USGA award |
| Scorecards | 4 historic scorecard variants |
| Photography | Course landscapes, drone aerial, tournament photos, member events |
| Branding | Fox Logo.png (club mascot logo) |
| PDFs | Current bylaws (01.21.26), USGA ceremony document |

Total: ~27 files.

---

## Adding Content

### New Event Card

Copy an existing `.event-card` block in the `#events` section. Set `data-date="YYYY-MM-DD"` to a date in the future — the auto-scroll IIFE will handle positioning automatically.

### New Board Member

Add a new `.board-card` in the `#about` section following the existing pattern: role, name, and `mailto:` link.

### New Tidbit

Add a `.tidbit-item` inside `.tidbits-list` in the `#course` section:

```html
<div class="tidbit-item">
  <div class="tidbit-header" onclick="toggleTidbit(this)">
    <span>Fact title</span>
    <span class="tidbit-icon">+</span>
  </div>
  <div class="tidbit-content">
    <p>Fact body text.</p>
  </div>
</div>
```
