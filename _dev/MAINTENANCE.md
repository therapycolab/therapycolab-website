# Therapy Colab — Site Maintenance Guide

> For Veronica Smith or any future developer maintaining therapycolab.com.
> This file is in the repo but is not web-served (blocked by netlify.toml).
> Developer contact: Val Janoras — val.janoras@syntriqal.ai

---

## Site Overview

Therapy Colab is a static HTML/CSS/JS site — no build tools, no framework, no CMS. Every page is a plain `.html` file. To update content, you edit the HTML directly and deploy.

**Pages:**
- `index.html` — Home
- `memberships.html` — Membership plans + room spaces
- `how-it-works.html` — 4-step process
- `about.html` — Founder bio, team, testimonials
- `contact.html` — Inquiry form, address, FAQ
- `privacy-policy.html` — Privacy Policy

**Shared files:**
- `styles.css` — All shared styles. Edit here for sitewide changes.
- `assets/` — Logo files, hero photo, room photos (once added)

---

## How to Deploy

The site is hosted on Netlify under the Therapy Colab account.

**Option A — Manual deploy (drag and drop):**
1. Make your edits to the HTML/CSS files
2. Log in to netlify.com with the Therapy Colab account
3. Go to the site → Deploys tab → drag the `site/` folder onto the deploy area
4. The new version goes live immediately

**Option B — GitHub auto-deploy:**
1. Make your edits and commit: `git add . && git commit -m "your message"`
2. Push: `git push origin main`
3. Netlify detects the push and deploys automatically within ~30 seconds

---

## Common Content Updates

### Updating text copy on any page
Open the relevant `.html` file, find the text, edit it, save, and deploy.

### Swapping in room photos
Room photos appear in the carousel on `memberships.html` and as placeholder backgrounds elsewhere. When real photography arrives:
1. Add the new photos to `assets/` (use descriptive names, e.g. `room-discovery.jpg`)
2. In `memberships.html`, find the `.space-card` items for each room and update the `src` attribute on the `<img>` tag
3. Remove any `<span class="...placeholder-tag">` labels that were marking placeholder images
4. Check `index.html` — the feature section image may also need updating

### Updating the founder headshot (About page)
1. Add the new photo to `assets/` (e.g. `veronica-headshot.jpg`)
2. In `about.html`, find the team carousel slide for Veronica and update the `<img src="">` path

### Updating provider testimonials (About page)
The testimonials section is in `about.html`. Find the testimonials grid and update or add `.testimonial-card` blocks. Each card has a quote, name, and credential.

### Updating the Mailchimp waitlist embed (Home page)
1. Get the embed code from Mailchimp (Audience → Signup forms → Embedded forms)
2. In `index.html`, find the waitlist section (look for `<!-- Mailchimp waitlist -->` comment)
3. Replace the placeholder form with the Mailchimp embed code
4. The embed will be unstyled by default — apply the existing form styles to match the site

### Updating the Acuity booking link
All "Book a Tour" buttons link to the Acuity URL. If Veronica sends a new/updated link:
1. Search `index.html` for `acuityscheduling.com` — update that href
2. Repeat for `memberships.html`, `how-it-works.html`, `about.html`, `contact.html`
Current link: `https://app.acuityscheduling.com/schedule.php?owner=39277070`

### Updating the Privacy Policy
The `privacy-policy.html` page has a skeleton structure. When Veronica's attorney approves the final policy content:
1. Open `privacy-policy.html`
2. Replace the placeholder content sections with the final policy text
3. Update the "Last updated" date at the top of the policy

### Adding a new page
1. Copy an existing page as a starting point (e.g. copy `contact.html`)
2. Update the `<title>` and `<meta name="description">` tags
3. Update the nav: on the new page, add the link to the `<nav>` block; on all other pages, add a link to the new page
4. Add the page to the footer nav on all pages
5. Add it to `netlify.toml` if any special rules apply

---

## Brand Reference

**Colors:**
| Name | Hex | Use |
|------|-----|-----|
| Ivory (bg) | `#F5F0E8` | Default page background |
| Warm surface | `#EAE2D6` | Alternating section backgrounds |
| Border | `#D8CCBE` | Dividers, card borders |
| Sage | `#5C9F99` | Primary brand — buttons, links, accents |
| Orange | `#E17563` | Secondary accent — badges, highlights |
| Text | `#302C27` | Body text |
| Muted | `#7A7068` | Secondary/supporting text |
| Dark | `#251F1A` | Footer, dark sections |

**Fonts** (loaded from Google Fonts):
- Headings: DM Serif Display
- Body: DM Sans (weight 300 default)
- Logo wordmark only: Encode Sans Expanded

**Contact:**
- Email: `admin@therapycolab.com`
- Phone: `(702) 443-2584`
- Address: 7560 W. Sahara Ave Suite 101, Las Vegas NV 89117

---

## Maintenance Contract

Post-launch updates are billed at $125/hr (minimum 0.5 hrs per request) under Exhibit C of the Web Development Services Agreement. Contact Val Janoras at val.janoras@syntriqal.ai to request changes.
