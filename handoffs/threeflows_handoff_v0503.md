# Three Flows Solutions — Website Reference & Handoff
## Version 0503 — Updated May 3, 2026

---

## What Changed Since v0502C

- Posts 013–020 published (Amazon Supply Chain series, 7 posts + post 013)
- Post 013 publish date: Feb 25, 2026
- Post 016 publish date updated to Feb 23, 2026 (was Jan 12)
- `blog.html` reordered to reflect all new posts in correct newest-first sequence
- `blog.html` card images updated: 014 → warehouse interior, 016 → red button (`assets/images/red_button.jpg`)
- `assets/images/red_button.jpg` added to repo (blog-016 card thumbnail)
- Series navigation added to all Amazon series posts (014–020): "Inside Amazon's Supply Chain" section at bottom of each post, showing all 7 posts with current post highlighted
- Draft banners stripped from all Amazon series posts (014–020)
- All Amazon series posts contain embedded base64 images (no external image hosting required)
- Next available post ID: **021**

---

## Overview

**Three Flows Solutions** is an e-commerce operations consultancy helping retail brands launch and scale. The website is a static multi-page HTML/CSS/JS site hosted on GitHub Pages.

- **Live site:** https://threeflows.com
- **GitHub repo:** https://github.com/sw805206/threeflows-website
- **Local working copy:** `/Users/swai/multipage/`
- **Blog draft source files:** `/Users/swai/multipage/blogs/` — local only, never committed to git
- **No build tools. No framework.** Each page is self-contained with inline `<style>` and `<script>`.
- **Source of truth:** Always read the live files from GitHub before making any changes. Do not rely on any handoff doc for current code — the repo is always more up to date.

---

## Current File Structure

```
index.html              — Home page
svc1.html               — Stage 01: Business Planning
svc2.html               — Stage 02: Sourcing Consultation (4 tabs)
svc3.html               — Stage 03: Launch Hypercare (4 tabs)
svc4.html               — Stage 04: Ongoing Management
intake.html             — Intake / inquiry form
about.html              — About / team page
inquiry.html            — Inquiry page
webinars.html           — Webinars & seminars page
livestream.html         — Livestream discussions page
free-tools.html         — Free tools / spreadsheets page
useful-websites.html    — Resource directory (3 tabs)
blog.html               — Blog index page (5 posts per page, paginated)
blog-000-template.html  — Blog post template — DO NOT add a card for this in blog.html
blog-001.html           — Post 001: Welcome to Three Flows Solutions
blog-002.html           — Post 002: How to Legally Cut Import Costs by Up to 48%
blog-003.html           — Post 003: Factory Data Problems Are Costing You More Than You Think
blog-004.html           — Post 004: Navigating the US-China Tariff War
blog-005.html           — Post 005: Why Data Integrity Is the Foundation of a Scalable Supply Chain
blog-006.html           — Post 006: Is FedEx's 2026 Rate Increase Really Just 5.9%?
blog-007.html           — Post 007: Where Should Your Third US Warehouse Be?
blog-008.html           — Post 008: Is a $1.40 Product Worth Selling in the US?
blog-009.html           — Post 009: Why Your Whatnot Livestream Needs a Sell-Through Model
blog-010a.html          — Post 010A: Dedicated 3PL Service — From $23.33 to $5.71 Per Order
blog-010b.html          — Post 010B: The Fifth M — Why Measurement Makes the Others Work
blog-011.html           — Post 011: What the One Big Beautiful Bill Means for Your Business
blog-012.html           — Post 012: Amazon's Two New Policies: What They Mean for Sellers
blog-013.html           — Post 013: [read live file for title]
blog-014.html           — Post 014: Inside Amazon's Supply Chain: A View from the Inside
blog-015.html           — Post 015: How Amazon Built a Global Logistics Network from Scratch
blog-016.html           — Post 016: The Little Red Button: What Happens to Amazon When a Blizzard Hits
blog-017.html           — Post 017: Amazon's US Warehouse Network: How 150+ Fulfillment Centers Actually Work
blog-018.html           — Post 018: Getting Into Amazon's Warehouse: The Inbound Process Every FBA Seller Should Know
blog-019.html           — Post 019: From Shelf to Doorstep: Inside Amazon's Fulfillment Center Operations
blog-020.html           — Post 020: The Culture That Built Amazon: Leadership Principles, Bar Raisers, and What It Really Takes
assets/images/          — logo_claude.svg + team/hero photos + red_button.jpg
CNAME                   — threeflows.com domain config
.gitignore              — excludes .claude/, blogs/blog_old/, blogs/blog_old2/, blogs/files.zip, blogs/blog_*_*.html
```

**Local-only — not in git:**
```
blogs/                  — draft source files (local archive only)
  blog-template.html
  blog_001_welcome.html
  blog_drafts_review.html    (contains posts 002–005)
  blog_006_fedex_2026.html
  blog_007_warehouse_placement.html
  blog_008_10usd_product.html
  blog_009_whatnot_breakeven.html
  blog_010a_fulfillment_cost.html
  blog_010b_measurement.html
  blog_011_obbba.html
  blog_012_amazon_policies.html
  amz1.pdf – amz8.pdf        (source PDFs for Amazon series posts 014–020)
  blog_old/             — archive folder
  blog_old2/            — archive folder
  files.zip             — archive
```

**Pages in repo whose content is not fully documented (read live file before editing):**
- `about.html` — About/team page. Nav currently links to `index.html#about-anchor` — verify if nav should be updated to point here directly.
- `inquiry.html` — Alternate/expanded inquiry form distinct from `intake.html`. Nav CTA on all pages links here.
- `threeflows_complete_v6.html` — Full-site consolidated file or design reference. Do not publish.

**Planned future pages (not yet built):**
- Newsletter signup
- Additional intake forms per service
- Additional blog posts (next available ID: **021**)

---

## Design System

Canonical `:root` CSS variables — every file must match this exactly:

```css
:root {
  --red: #D63B3B;
  --red-dark: #B82E2E;
  --red-light: #FDF0F0;
  --red-mid: rgba(214, 59, 59, 0.12);
  --dark: #1A1A1A;
  --mid: #5C5C5C;
  --muted: #909090;
  --off-white: #F8F8F8;
  --white: #FFFFFF;
  --border: rgba(0,0,0,0.09);
  --border-dark: rgba(0,0,0,0.18);
  --green: #00B050;
  --green-light: #EAF3DE;
  --radius: 12px;
  --radius-sm: 8px;
  --font-body: 16px;
  --line-height: 1.7;
  --transition: 0.18s ease;
  --warm: #F8F8F8;
  --warm-border: rgba(180,150,100,0.2);
}
```

**Fonts:** Google Fonts — DM Serif Display (headings) + DM Sans (body)

Do not hardcode hex values outside `:root`. Exception: `.nav-cta:hover { background: #333; }` is intentional.

---

## Shared Elements

### Nav

Identical across all pages. Structure:

```
Logo (assets/images/logo_claude.svg + "Three Flows Solutions / from Start to Scale") → index.html
├── Home → index.html
├── Services ▾
│   ├── 01 — Business Planning → svc1.html
│   ├── 02 — Sourcing Consultation → svc2.html
│   ├── 03 — Launch Hypercare → svc3.html
│   └── 04 — Ongoing Management → svc4.html
├── About → index.html#about-anchor
├── Resources ▾
│   ├── Blogs & Articles → blog.html
│   ├── Useful Websites → useful-websites.html
│   ├── Checklists & Calculators → free-tools.html
│   ├── Recorded Webinars & Seminars → webinars.html
│   └── Livestream Discussions → livestream.html
├── Contact → index.html#contact-anchor
└── [CTA] "Submit an inquiry" → inquiry.html
```

- Both dropdowns use `toggleDropdown(id, event)` with `event.stopPropagation()` — without stopPropagation the dropdown closes immediately on open
- `toggleDropdown` adds/removes `.open` class on the `<li class="nav-dropdown">` element — not on the menu div directly
- Nav is designed to accommodate future top-level items without layout changes

### Footer

Identical across all pages. Always outside tab panels, appears exactly once per page:

```html
<footer>
  <div style="display:flex;align-items:center;gap:12px">
    <img src="assets/images/logo_claude.svg" alt="Three Flows Solutions" style="width:34px;height:34px;">
    <span>© 2026 Three Flows Solutions LLC. All rights reserved.</span>
  </div>
  <div class="footer-links">
    <a href="#">Privacy</a><a href="#">Terms</a>
  </div>
</footer>
```

---

## CTA Buttons

Three standard buttons only. Do not create variants, rename labels, or restyle inline.

| Class         | Label                    | Destination                        |
|---------------|--------------------------|------------------------------------|
| `btn-red`     | Submit an inquiry        | inquiry.html                       |
| `btn-outline` | Fill in an intake form   | intake.html or `#`                 |
| `btn-dark`    | Book a call              | Booking link or `#`                |

Every bottom CTA section uses this set (or a subset of 1–2 as appropriate). Labels must not be reworded.

---

## Page Notes

### index.html
Sections in order:
1. Hero — "Launch your retail business with confidence"
2. Partner strip
3. Client case study (dark bg, proof-wrap) — above "How we work"
4. `id="services-anchor"` → How we work (interactive 4-step process flow)
5. Services grid — 4 tiles linking to svc1–4.html
6. `id="about-anchor"` → Team section
7. `id="resources-anchor"` → Knowledge Bank (resource tiles including "Useful websites" → useful-websites.html)
8. `id="contact-anchor"` → Get started / CTA grid
9. Footer

The "Useful websites" tile in the Knowledge Bank has a "Go →" CTA linking to useful-websites.html (not a full card hyperlink).

### svc1.html — Business Planning
- Breadcrumb "← Services" → `index.html#services-anchor`
- Sections: Hero → Continuity banner → Problem → Process steps → Deliverables → FAQ → Bottom CTA

### svc2.html — Sourcing Consultation
- 4 tabs: 2A Make-or-buy | 2B Sourcing playbook | 2C Factory visit | 2D Contract support
- Tab switching: `setTab(idx)` toggles `tab-0` through `tab-3` by `el.style.display`
- **Never use `querySelectorAll('.ws-content')` inside `setTab()`** — bleeds into svc3
- Each tab has its own FAQ + shared Q2O routing question
- Bottom CTA: "Ready to source smarter?"

### svc3.html — Launch Hypercare
- 4 tabs: 3A Brand assets | 3B Launch supply bootcamp | 3C Process improvement | 3D System integration
- Tab switching: `setSvc3Tab(idx)` toggles `.active` class on IDs `svc3-ws-0` through `svc3-ws-3`
- **Never use positional `querySelectorAll('.ws-content')` inside `setSvc3Tab()`**
- Pricing summary card at bottom (4 cards: 3A / 3B / 3C / 3D) — keep this
- Each tab has its own FAQ section

### svc4.html — Ongoing Management
- Sections: Hero → Continuity banner → Philosophy → Services split (core/optional) → Control tower → What you keep → Growth path → FAQ → Bottom CTA

### intake.html
- Intake / inquiry form page
- Form submits to a live Google Apps Script URL — do not change the submission endpoint

### useful-websites.html — Resource Directory
Three tabs. Tab switching uses an isolated function (check the live file for the exact function name). Do not rename tabs, reorder tabs, or modify tab IDs without explicit instruction.

**Tab 1 — Market Insights & Compliance**
Three category sections in this order:
1. Global Trade Data
2. Market Research
3. Compliance & IP (includes: Amazon Brand Registry, CBP ACE Portal, CNIPA, CPSC, FCC, FDA, FTC, GS1 US, USPTO, USITC HTS)

**Tab 2 — Business Management**
Ten category sections in this order:
1. Company Formation
2. Domain & Hosting
3. Website Builder
4. Product & Analytics
5. Marketing & Growth
6. Collaboration
7. CRM
8. Logistics & Ops
9. Finance & Payments (includes COI vendors: CoverWallet, Hiscox, Next Insurance, Thimble)
10. HR & Hiring

**Tab 3 — Top E-Commerce Marketplaces**
Three sections:
1. Top US e-commerce marketplaces (open signup group + curated/vendor group)
2. Amazon Seller Central by market (North America, Europe, Middle East & Africa, Asia-Pacific)
3. Regional marketplaces (Europe, Latin America, Far East, Southeast Asia, Middle East & Africa)

---

## Blog System

### Overview

The blog is a flat-file system. Every post is a self-contained HTML page in the repo root. There is no CMS, no database, no build step. Adding a new post = create the HTML file + add a card to `blog.html`.

### blog-000-template.html — Blog Post Template

The canonical starting point for every new post. Lives in the repo root. **Never add a card for this file in `blog.html`.**

When starting a new post in Claude Chat, always fetch the template first:
```
https://raw.githubusercontent.com/sw805206/threeflows-website/main/blog-000-template.html
```

The template contains:
- Full `:root` CSS variables
- Correct nav (with live Resource links and `inquiry.html` CTA)
- Breadcrumb (`← Blog` → `blog.html`)
- `.post-nav` block positioned **above** `.layout` — this is mandatory
- `.post-meta` row: date left + all 8 tag pills right (`primary` / `secondary` / `empty`)
- `.layout` content wrapper
- Correct footer
- `toggleDropdown` script

### blog.html — Blog Index Page

- **Hero:** "Notes from the Field" heading + subtitle
- **Tag filter bar:** 9 clickable buttons with client-side JS filtering
  - Tags: All | Plan | Source | Launch | Scale | Data | Setup | Compliance | Others
  - Multi-select, OR logic
  - "All" clears selection and shows everything
  - Active tag: `--red` background, white text
  - Each post card has `data-tag="[tag]"` attribute used by the filter JS
- **Post list:** vertical, one card per row, sorted newest-first (descending by publish date)
- **Pagination:** 5 posts per page. Controls appear below the list when total visible posts > 5. Resets to page 1 on every filter change. Auto-hides when ≤ 5 posts are visible.
- **Card structure per post:**
  - Image left (260px, Unsplash or `assets/images/`) with onerror fallback
  - All 8 tag pills (primary / secondary / empty)
  - Date top-right of the card body
  - Title, excerpt, "Read ↗"
  - `data-tag` attribute contains space-separated tag names used by filter JS

### Post Meta — Tag Pills

Every post card in `blog.html` and every post page shows all 8 tag pills in this fixed order:

```
Plan | Source | Launch | Scale | Data | Setup | Compliance | Others
```

Each pill has one of three classes:
- `primary` — the post's main tag (pink background)
- `secondary` — an additional relevant tag (grey background)
- `empty` — not applicable (very faint, decorative)

### Unsplash Images Per Post

Each post card on `blog.html` uses a fixed photo. Append `?w=520&h=360&fit=crop&auto=format` to Unsplash URLs. All have onerror fallback. Posts 014–020 use either Unsplash or a local `assets/images/` file.

| ID | Image source |
|---|---|
| 001 | photo-1522202176988-66273c2fd55f |
| 002 | photo-1570126618953-d437176e8c79 |
| 003 | photo-1504307651254-35680f356dfd |
| 004 | photo-1611974789855-9c2a0a7236a3 |
| 005 | photo-1454165804606-c3d57bc86b40 |
| 006 | photo-1601584115197-04ecc0da31d7 |
| 007 | photo-1586528116311-ad8dd3c8310d |
| 008 | photo-1579621970563-ebec7560ff3e |
| 009 | photo-1516321318423-f06f85e504b3 |
| 010A | photo-1553413077-190dd305871c |
| 010B | photo-1551288049-bebda4e38f71 |
| 011 | photo-1554224155-6726b3ff858f |
| 012 | photo-1523474253046-8cd2748b5fd2 |
| 013 | [read live blog.html] |
| 014 | photo-1504307651254-35680f356dfd |
| 015 | photo-1553413077-190dd305871c |
| 016 | assets/images/red_button.jpg |
| 017 | photo-1586528116311-ad8dd3c8310d |
| 018 | photo-1586528116311-ad8dd3c8310d |
| 019 | photo-1454165804606-c3d57bc86b40 |
| 020 | photo-1522202176988-66273c2fd55f |

### Post ID System

- **Format:** 3-digit numeric, e.g. `001`, `007`, `021`
- **Sequels / multi-part series:** suffix letters A, B, C… e.g. `010A`, `010B`
- **IDs are permanent.** Once published, an ID never changes and its filename never changes.
- **IDs are not publish-date order.** They are assigned sequentially as posts are created.
- **Next available ID:** `021`
- **Filename convention:** `blog-[ID].html` using hyphens, e.g. `blog-001.html`, `blog-010a.html`

### Tag System

Eight tags — mapped to services where possible. Use short labels everywhere.

| Short tag | Full name | Maps to |
|---|---|---|
| Plan | Business Planning | Stage 01 — svc1.html |
| Source | Sourcing Consultation | Stage 02 — svc2.html |
| Launch | Launch Hypercare | Stage 03 — svc3.html |
| Scale | Ongoing Management | Stage 04 — svc4.html |
| Data | Data Model | Cross-service analytical posts |
| Setup | Setup | Operational setup / infrastructure |
| Compliance | Compliance | Trade, legal, regulatory posts |
| Others | Others | Company / general |

### Published Posts — Master Table

Sorted by publish date, newest first (matches blog.html card order).

| ID | Filename | Publish Date | Tag (primary) | Title |
|---|---|---|---|---|
| 020 | blog-020.html | Mar 20, 2026 | Others | The Culture That Built Amazon: Leadership Principles, Bar Raisers, and What It Really Takes |
| 019 | blog-019.html | Mar 3, 2026 | Others | From Shelf to Doorstep: Inside Amazon's Fulfillment Center Operations |
| 013 | blog-013.html | Feb 25, 2026 | [read live file] | [read live file] |
| 016 | blog-016.html | Feb 23, 2026 | Others | The Little Red Button: What Happens to Amazon When a Blizzard Hits |
| 018 | blog-018.html | Feb 16, 2026 | Others | Getting Into Amazon's Warehouse: The Inbound Process Every FBA Seller Should Know |
| 009 | blog-009.html | Feb 2, 2026 | Launch | Why Your Whatnot Livestream Needs a Sell-Through Model |
| 017 | blog-017.html | Jan 28, 2026 | Others | Amazon's US Warehouse Network: How 150+ Fulfillment Centers Actually Work |
| 006 | blog-006.html | Jan 16, 2026 | Scale | Is FedEx's 2026 Rate Increase Really Just 5.9%? |
| 015 | blog-015.html | Dec 22, 2025 | Others | How Amazon Built a Global Logistics Network from Scratch |
| 014 | blog-014.html | Dec 5, 2025 | Others | Inside Amazon's Supply Chain: A View from the Inside |
| 007 | blog-007.html | Nov 17, 2025 | Scale | Where Should Your Third US Warehouse Be? |
| 008 | blog-008.html | Sep 12, 2025 | Plan | Is a $1.40 Product Worth Selling in the US? |
| 005 | blog-005.html | Aug 25, 2025 | Source | Why Data Integrity Is the Foundation of a Scalable Supply Chain |
| 012 | blog-012.html | Aug 4, 2025 | Scale | Amazon's Two New Policies: What They Mean for Sellers |
| 003 | blog-003.html | Aug 2, 2025 | Source | Factory Data Problems Are Costing You More Than You Think |
| 011 | blog-011.html | Jul 6, 2025 | Others | What the One Big Beautiful Bill Means for Your Business |
| 010B | blog-010b.html | Jun 8, 2025 | Scale | The Fifth M: Why Measurement Is the One That Makes All the Others Work |
| 010A | blog-010a.html | Jun 5, 2025 | Launch | Dedicated 3PL Service Can Cost $23.33 Per Order — or $5.71 |
| 004 | blog-004.html | May 12, 2025 | Source | Navigating the US-China Tariff War |
| 002 | blog-002.html | Apr 29, 2025 | Source | How to Legally Cut Import Costs by Up to 48% |
| 001 | blog-001.html | Mar 5, 2025 | Others | Welcome to Three Flows Solutions: Where Education Meets Execution |

### Prev/Next Navigation — Publish Date Order

Every post page has a `.post-nav` block **above** the `.layout` div. Order is strictly by publish date, oldest to newest:

| Post | ← Previous | Next → |
|---|---|---|
| blog-001 | — | blog-002 |
| blog-002 | blog-001 | blog-004 |
| blog-004 | blog-002 | blog-010a |
| blog-010a | blog-004 | blog-010b |
| blog-010b | blog-010a | blog-011 |
| blog-011 | blog-010b | blog-003 |
| blog-003 | blog-011 | blog-012 |
| blog-012 | blog-003 | blog-005 |
| blog-005 | blog-012 | blog-008 |
| blog-008 | blog-005 | blog-007 |
| blog-007 | blog-008 | blog-006 |
| blog-006 | blog-007 | blog-014 |
| blog-014 | blog-006 | blog-015 |
| blog-015 | blog-014 | blog-017 |
| blog-017 | blog-015 | blog-009 |
| blog-009 | blog-017 | blog-018 |
| blog-018 | blog-009 | blog-016 |
| blog-016 | blog-018 | blog-013 |
| blog-013 | blog-016 | blog-019 |
| blog-019 | blog-013 | blog-020 |
| blog-020 | blog-019 | — |

### Amazon Series — Special Notes

Posts 014–020 form the **"Inside Amazon's Supply Chain"** series. They have two special properties not present in other posts:

**1. Embedded images (base64)**
All photos in posts 014–020 are embedded as base64 data URIs — they do not reference external URLs or `assets/images/`. The source images came from translated Chinese social media PDFs (amz1.pdf–amz8.pdf, stored locally in `blogs/`). Do not replace base64 images with Unsplash URLs in the post body — the images are original content.

**2. Series navigation block**
Each of the 7 posts contains a `.series-nav` block at the bottom of `.layout` listing all 7 posts. The current post is highlighted with `class="series-item series-current"` (non-clickable, red background). All other rows use `class="series-item"` (clickable links).

The series nav CSS is inlined in each post's `<style>` block. If editing a post, preserve the `.series-nav` styles and HTML. The reading order in the series nav is:

1. blog-014 — Dec 5, 2025
2. blog-015 — Dec 22, 2025
3. blog-017 — Jan 28, 2026
4. blog-018 — Feb 16, 2026
5. blog-016 — Feb 23, 2026
6. blog-019 — Mar 3, 2026
7. blog-020 — Mar 20, 2026

Note: The series reading order (by topic logic) differs from the publish date order because blog-016 was published after blog-018 but covers an earlier conceptual topic. The series nav uses the reading order above, not strict publish-date order.

---

## Individual Post Page Rules

Every blog post page must follow these rules:

1. **Always start from `blog-000-template.html`** — fetch the live template from GitHub, never build from scratch or copy from memory
2. **Breadcrumb:** `← Blog` linking to `blog.html` — immediately below nav
3. **Prev/next nav:** `.post-nav` block sits **above** `.layout`, immediately after the breadcrumb — never inside `.layout`
4. **Nav and footer:** identical to all other pages — copy from template exactly
5. **One footer per page** — never inside any content section
6. **Page title format:** `[Post Title] — Three Flows Solutions`
7. **Post meta block:** every post has a `.post-meta` row containing:
   - Publish date — class `post-date`, muted, format `Publish: Month D, YYYY`
   - All 8 tag pills — class `post-tags`, right-aligned via `margin-left: auto`
   - **No post ID badge on post pages** — the `post-num` badge does not appear
8. **Interactive JS** (charts, maps, simulators) is preserved exactly as written. Do not refactor or simplify.
9. **Review banner** (`<div class="review-banner">`) is present in draft files only — always stripped before publishing.

### Posts With Interactive Elements

These posts contain embedded JS that must be preserved exactly:

| Post | Library | Feature |
|---|---|---|
| blog-007.html | D3.js | Interactive choropleth US map — 4 scenario toggles |
| blog-008.html | Chart.js | Waterfall cost stack chart |
| blog-009.html | Vanilla JS | Breakeven simulator — 6 sliders, live chart, profit verdict |

---

## Adding a New Blog Post — Full Workflow

### Step 1 — Draft in Claude Chat

1. Share the source material with Claude Chat
2. Specify: post ID (next available: **021**), tag (primary + secondary if any), publish date, any interactive element needed
3. Claude Chat will:
   - Fetch `blog-000-template.html` from GitHub to ensure structural consistency
   - Fetch a recent live post to verify tone
   - Draft the full post HTML with review banner included
4. Review the draft in the Claude Chat preview
5. Download the draft HTML

### Step 2 — Save files locally

| File | Save to |
|---|---|
| New post draft | `/Users/swai/multipage/blog-[ID].html` |
| Draft archive copy | `/Users/swai/multipage/blogs/blog_[ID]_[slug].html` |

### Step 3 — Determine chronological position

Insert the new post into the publish-date order. Identify:
- The post immediately **before** it (just above in the newest-first list)
- The post immediately **after** it (just below)

These two neighbors need their prev/next pointers updated.

### Step 4 — Send to Claude Code

```
`blog-[ID].html` has been saved to `/Users/swai/multipage/blog-[ID].html` (has review banner).

Read the live versions of `blog.html`, `blog-[PREV].html`, and `blog-[NEXT].html`
from `https://raw.githubusercontent.com/sw805206/threeflows-website/main/`
before making any edits.

1. In `blog-[ID].html`: strip the `<div class="review-banner">…</div>` block and save in place.

2. In `blog.html`: add a post card for [ID] in chronological position —
   after blog-[PREV] ([PREV DATE]) and before blog-[NEXT] ([NEXT DATE]).
   Use:
   - data-tag="[PRIMARY TAG]"
   - Unsplash photo: [PHOTO-ID]?w=520&h=360&fit=crop&auto=format
   - Date: [SHORT DATE]
   - Title: [POST TITLE]
   - Description: [1–2 sentence excerpt]

3. Update prev/next on three post files:
   - blog-[PREV].html: change Next → to blog-[ID].html / "[NEW POST TITLE]"
   - blog-[ID].html: set Prev → blog-[PREV].html / "[PREV TITLE]"
                     and Next → blog-[NEXT].html / "[NEXT TITLE]"
   - blog-[NEXT].html: change Prev → to blog-[ID].html / "[NEW POST TITLE]"

4. git add blog-[ID].html blog.html blog-[PREV].html blog-[NEXT].html &&
   git commit -m "Add post [ID]: [short title]" && git push

5. After the push, open https://threeflows.com/blog-[ID].html in Google Chrome
   and take a screenshot to confirm the page loads correctly.
```

### Step 5 — Update this handoff doc

After publishing, update:
- The **Published Posts Master Table** — add the new row in correct date order
- The **Prev/Next Navigation table** — update the three affected rows
- The **Unsplash Images table** — add the new photo ID
- The **Next available ID** counter
- The **File Structure** list

---

## Blog Post Content Notes

**001 — Welcome**
Introduction post. Explains the Three Flows name (material flow, cash flow, information flow), the education + entrepreneurship mission, and the three service pillars. Tone should be warmer/less formal than analytical posts — currently slightly too formal, flagged for future revision.

**002, 003, 004, 005 — Whitepaper series**
Source: internal supply chain whitepaper (client anonymized as "a UK-based brand owner", "an origin consolidation provider"). Product category anonymized to "specialty consumer goods" / "licensed consumer products". All factory names, logistics partner names, and identifying details removed.

**006 — FedEx 2026 rates**
Source: translated from Chinese social media article (XHS, Jan 16 datestamp) + FedEx standard rate table (Excel). Key finding: stated 5.9% GRI is an average; effective increase for 10–30 lb Zone 7–8 shipments reaches 6.71%; residential surcharge compounds to 6.25% effective increase.

**007 — US warehouse placement**
Source: translated from Chinese social media (XHS, Jan 25 datestamp) + US shipment heatmap data (Excel). Contains interactive D3 choropleth map. Key finding: 5-node network (LAX → EWR → SAV → DAL → CHI) reduces mean order span from 7.51 to 4.70 zones.

**008 — $1.40 product viability**
Source: translated from Chinese social media (XHS, Jan 28 datestamp). The 7–10x factory-to-retail rule of thumb. Interactive Chart.js waterfall showing cost stack to $100 retail price.

**009 — Whatnot breakeven**
Source: client Excel model (watch batch simulation — 500 units, $15 retail, $70/hr promo + $20/hr labor). Interactive simulator with 6 sliders. Key finding: breakeven at ~12 units/hr; 10 units/hr = −$517 loss; 12 units/hr = +$203 profit.

**010A — Dedicated 3PL cost model**
Source: client fulfillment cost analysis Excel (OB cost analysis sheet only). 5-scenario model. Key finding: $23.33 baseline → $5.71 optimized (75% reduction). "July Ops" = Three Flows proposed start state ($15.00, single system, foam, 1 box size).
- The $10/hr management fee = Three Flows control tower role (brief mention in 010A, expanded in 010B)
- Growth flywheel: lower cost → reinvest in ads/pricing → higher volume → further compression

**010B — The Fifth M: Measurement**
Companion to 010A. Opens with callback to 010A cost model. Measurement as connective tissue through the 5M framework. Closes: "Measure, Model, Monitor, repeat."

**011 — OBBBA business tax provisions**
Source: CPA-authored article on the One Big Beautiful Bill Act (signed July 4, 2025). Scope limited to four business-side provisions: 100% bonus depreciation, §179 expensing, R&D immediate expensing, eased §163(j). Interactive 4-item checklist. Disclaimer: Three Flows is not a tax advisor.

**012 — Amazon new policies**
Source: AInvest article (Jul 31, 2025) + Amazon Seller Central Europe forum post. Two-policy post: Google Shopping ad withdrawal + star-rating-only feedback (Aug 4, 2025).

**013 — [read live file]**
Published Feb 25, 2026. Title and content: read from the live repo.

**014–020 — Inside Amazon's Supply Chain series**
Source: 8 Chinese social media PDFs (amz1.pdf–amz8.pdf) translated and reorganized into 7 English posts. All images are embedded as base64. Series covers:
- **014** — Amazon's position in US retail (~40% online share), flywheel effect, FBA origin story. Stats verified: ~16% of US retail is online; Amazon holds ~40% of that; Walmart ~6%; 600M products on platform; 98% from 3P sellers.
- **015** — Building the global network: AGL, ATS, Amazon Air, AMZL. AMZL handles ~70% of Amazon's own deliveries. S&OP planning cadence (weekly + annual rhythm).
- **016** — S&OP on-call story: LRB (Little Red Button) and the East Coast blizzard cascade. Publish date Feb 23, 2026.
- **017** — US warehouse network: 150 FCs in the US (200+ globally per Amazon MCF). 17M+ Amazon Logistics orders/day in 2024; 25M+ parcels/day at 2024 peak.
- **018** — FBA inbound process: 6 receiving paths (Case Receive, Each Receive, Prep, Problem Solve, Sideline, Discard). 7 seller best practices. Secondary tag: Scale.
- **019** — FC operations: stow (Kiva/chaotic storage) → pick → pack → SLAM → outbound sort → last mile. Images from amz8.pdf embedded.
- **020** — Amazon culture: 14 Leadership Principles, Bar Raiser hiring system, personal career narrative. LP link: https://www.amazon.jobs/content/en/our-workplace/leadership-principles

---

## Critical Rules

1. **Always start new posts from `blog-000-template.html`** — fetch from GitHub, never build from scratch

2. **Prev/next nav position** — `.post-nav` block is always **above** `.layout`, never inside it

3. **No post ID badge on post pages** — `.post-num` does not appear; only date + tag pills in `.post-meta`

4. **blog.html card order is newest-first** — when adding a card, insert it at the correct chronological position

5. **Three files always need prev/next updates** when inserting a new post in the middle of the chain. Only two files if inserting at either end.

6. **Tab JS isolation**
   - `setTab()` (svc2): toggles only `tab-0` through `tab-3` by ID — never `querySelectorAll('.ws-content')`
   - `setSvc3Tab()` (svc3): toggles only `svc3-ws-0` through `svc3-ws-3` by ID — never positional querySelectorAll
   - `useful-websites.html` tab function: isolated to its own IDs — never shares class selectors with svc2 or svc3
   - `blog.html` filter + pagination JS: standalone, operates only on `.blog-card[data-tag]`

7. **Nav dropdowns** must use `toggleDropdown(id, event)` with `event.stopPropagation()` — adds `.open` class to the `<li>`, not the menu div

8. **Breadcrumbs:**
   - svc1–4: "← Services" → `index.html#services-anchor`
   - All blog posts: "← Blog" → `blog.html`

9. **One footer per page** — never inside a tab panel or content section

10. **Three CTA buttons only** — no variants, no new classes, no relabelled text

11. **Do not hardcode colors** outside `:root`

12. **Logo file:** `assets/images/logo_claude.svg` — used in both nav and footer, identical in both locations

13. **Blog post IDs are permanent** — never rename a published blog filename

14. **Review banners are draft-only** — always strip `<div class="review-banner">` before publishing

15. **Blog draft files are local-only** — never `git add blogs/` — `.gitignore` excludes these but verify before committing

16. **Interactive JS in posts** — never rewrite, reformat, or simplify D3 / Chart.js / simulator code in blog-007, blog-008, blog-009

17. **blog-000-template.html** — committed to repo, never gets a card in `blog.html`

18. **Amazon series posts (014–020)** — images are base64 embedded; do not replace with external URLs. Preserve `.series-nav` block in each post.

---

## Git Hygiene

- **`.gitignore` excludes:** `.claude/`, `blogs/blog_old/`, `blogs/blog_old2/`, `blogs/files.zip`, `blogs/blog_*_*.html`
- **Before every commit:** confirm `git status` does not include anything from `blogs/`
- **Standard commit pattern for new posts:**
  `git add blog-[ID].html blog.html blog-[PREV].html blog-[NEXT].html && git commit -m "Add post [ID]: [title]" && git push`
- **For blog.html-only changes (e.g. pagination, reordering):**
  `git add blog.html && git commit -m "[description]" && git push`

---

## Page Titles

| File | `<title>` |
|---|---|
| index.html | Three Flows Solutions — From Start to Scale |
| svc1.html | Business Planning — Three Flows Solutions |
| svc2.html | Sourcing Consultation — Three Flows Solutions |
| svc3.html | Launch Hypercare — Three Flows Solutions |
| svc4.html | Ongoing Management — Three Flows Solutions |
| intake.html | Get Started — Three Flows Solutions |
| useful-websites.html | Useful Websites — Three Flows Solutions |
| blog.html | Blogs & Articles — Three Flows Solutions |
| blog-001.html | Welcome to Three Flows Solutions: Where Education Meets Execution — Three Flows Solutions |
| blog-002.html | How to Legally Cut Import Costs by Up to 48% — Three Flows Solutions |
| blog-003.html | Factory Data Problems Are Costing You More Than You Think — Three Flows Solutions |
| blog-004.html | Navigating the US-China Tariff War — Three Flows Solutions |
| blog-005.html | Why Data Integrity Is the Foundation of a Scalable Supply Chain — Three Flows Solutions |
| blog-006.html | Is FedEx's 2026 Rate Increase Really Just 5.9%? — Three Flows Solutions |
| blog-007.html | Where Should Your Third US Warehouse Be? — Three Flows Solutions |
| blog-008.html | Is a $1.40 Product Worth Selling in the US? — Three Flows Solutions |
| blog-009.html | Why Your Whatnot Livestream Needs a Sell-Through Model — Three Flows Solutions |
| blog-010a.html | Dedicated 3PL Service Can Cost $23.33 Per Order — or $5.71 — Three Flows Solutions |
| blog-010b.html | The Fifth M: Why Measurement Is the One That Makes All the Others Work — Three Flows Solutions |
| blog-011.html | What the One Big Beautiful Bill Means for Your Business — Three Flows Solutions |
| blog-012.html | Amazon's Two New Policies: What They Mean for Sellers — Three Flows Solutions |
| blog-013.html | [read live file] — Three Flows Solutions |
| blog-014.html | Inside Amazon's Supply Chain: A View from the Inside — Three Flows Solutions |
| blog-015.html | How Amazon Built a Global Logistics Network from Scratch — Three Flows Solutions |
| blog-016.html | The Little Red Button: What Happens to Amazon When a Blizzard Hits — Three Flows Solutions |
| blog-017.html | Amazon's US Warehouse Network: How 150+ Fulfillment Centers Actually Work — Three Flows Solutions |
| blog-018.html | Getting Into Amazon's Warehouse: The Inbound Process Every FBA Seller Should Know — Three Flows Solutions |
| blog-019.html | From Shelf to Doorstep: Inside Amazon's Fulfillment Center Operations — Three Flows Solutions |
| blog-020.html | The Culture That Built Amazon: Leadership Principles, Bar Raisers, and What It Really Takes — Three Flows Solutions |
