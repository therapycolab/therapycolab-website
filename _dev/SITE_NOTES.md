# Therapy Colab — Developer Site Notes

> Internal dev notes — conventions, quirks, placeholder inventory.
> Not for clients. Not web-served (blocked by netlify.toml).

---

## Known CSS Quirks & Gotchas

### overflow-x and sticky nav
**Do not use `overflow-x: hidden` on `body`.** It breaks `position: sticky` on the nav.
The fix is `overflow-x: clip` on `html` only (already set in styles.css). This is correct and intentional — do not change it.

### Footer background bleed
On pages with a dark footer (`#251F1A`), the body background color (`--bg` ivory) can bleed below the footer on short content or fast scroll. Fix already applied on `how-it-works.html` with a page-scoped `body { background: #251F1A }`. If this appears on other pages, apply the same fix.

### Mobile nav "Book a Tour" button
`.wf-nav__mobile-cta` is set to `display: none` in `styles.css` for desktop. It shows inside the hamburger menu on mobile. Do not remove the `display: none` rule — it prevents a duplicate CTA button from appearing on desktop.

### Step connectors (how-it-works.html)
The arrows between steps use `::after` pseudo-elements with `content: '→'`. They are `position: absolute; right: -22px`. If the grid gap changes, the arrow position needs updating. The steps use `display: flex; flex-direction: column` on each `.step`, with `flex: 1` on `.step__body` to align links at the bottom — do not remove these.

### Hero photo (index.html)
The hero uses a 2-col split grid. The right column fills with `hero.jpg` using `object-fit: cover; object-position: center top`. The hero has no padding and the inner has `width: 100%` — this is intentional to prevent whitespace on the right side.

---

## File Architecture Notes

### Shared vs. page-scoped styles
`styles.css` contains all shared styles. Page-specific styles (hero variants, section layouts unique to one page) live in a `<style>` block in the `<head>` of that page. This keeps the shared stylesheet clean.

### No build step
This is a plain static site. No Sass, no PostCSS, no bundler. What you write is what gets served. CSS custom properties (`var()`) handle theming.

### Custom cursor
The cursor JS (`#cursor-ring` + `#cursor-dot`) is duplicated in each page's inline `<script>` block at the bottom of `<body>`. It is not in a shared JS file. If you update the cursor behavior, update it on all 6 pages.

### Hamburger nav
Same situation — the hamburger toggle JS is duplicated per page. Shared logic, not shared file.

---

## Placeholder Inventory

Everything below still needs real content before or at launch.

| Placeholder | File(s) | Notes |
|-------------|---------|-------|
| Room photos — Discovery | `memberships.html` carousel, slide 1 | Unsplash: `photo-1497366216548` |
| Room photos — Roundtable | `memberships.html` carousel, slide 2 | Unsplash: `photo-1524758631624` |
| Room photos — Sandbox | `memberships.html` carousel, slide 3 | Unsplash: `photo-1555212697` |
| Room photos — Commons | `memberships.html` carousel, slide 4 | Unsplash: `photo-1497366754035` |
| Room photos — Forum | `memberships.html` carousel, slide 5 | Unsplash: `photo-1497215842964` |
| Hero photo | `index.html` right column, `assets/hero.jpg` | Compressed from 5760×3840 — may need swap when real rooms are shot |
| Background (how-it-works) | `how-it-works.html` steps section | `hero.jpg` at 5% opacity — placeholder label in bottom-right corner |
| Founder headshot | `about.html` team carousel, slide 1 | **Real headshot received** — `vsmith Headshot.png` in client assets folder. Needs copying to `assets/` and updating src. |
| Founder bio | `about.html` team carousel | **Real bio received** — update carousel card text + add pull quote |
| Testimonials (×3) | `about.html` testimonials grid | 3 testimonials received |
| Mailchimp embed | `index.html` waitlist section | **Embed code received** — Wire up and style to match site. |
| Acuity booking link | All 5 pages (`#book-tour` hrefs) | **Link received** — `https://app.acuityscheduling.com/schedule.php?owner=39277070`. Swap all `href="#book-tour"` occurrences. |
| Privacy Policy content | `privacy-policy.html` | |
| Story photo | `about.html` story section | Unsplash `photo-1497366216548` — may remain until room photography arrives |

### Placeholder labels in HTML
Placeholder images are marked with `<span class="...placeholder-tag">` elements visible on the page. Remove these when real images are swapped in.

---

## Membership Tiers (reference)

| Tier | Price | Hours/mo | Notes |
|------|-------|----------|-------|
| Starter | $580 | 16 hrs | |
| Essential | $880 | 28 hrs | |
| Professional | $1,280 | 40 hrs | "Most Popular" — `transform: scale(1.04)`, orange badge |
| Clinical Partner | $1,840 | 60 hrs | |

Below the 4 cards: "Need more than 60 hours, or scheduling for a larger team? Let's talk →" → `contact.html`
À la carte note: "Occasional use? À la carte from $45–$60/hr — limited availability"

---

## Room Names (confirmed by Veronica)

| Room | Type |
|------|------|
| Discovery | Assessment & evaluation |
| Roundtable | Private office / small groups |
| Sandbox | Pediatric play therapy |
| Commons | Social skills groups |
| Forum | Group training & conference |

---

## Memberships Carousel (Our Spaces)

Located in `memberships.html`. Auto-advances every 5 seconds, pauses on hover. No external library — custom JS in the page. Prev/next buttons + dot indicators. If adding rooms: add a new `.space-card` slide and update the dot count in the JS.
