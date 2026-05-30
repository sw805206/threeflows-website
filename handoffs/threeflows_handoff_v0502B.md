# Three Flows Solutions — Website Reference & Handoff
## Version 0502B — Updated May 2, 2026

---

## What Changed Since v0502

- Blog infrastructure fully published to GitHub (commit `fece9ef`)
- Blog index page redesigned: vertical layout, Unsplash photos, short tag names, prev/next nav on all posts
- Tag system renamed to short labels (see Tag System section)
- Blog post files live in repo root — not in `blogs/` subfolder
- `.gitignore` updated to exclude `blogs/` archive folders
- `webinars.html`, `livestream.html`, `free-tools.html` confirmed in repo and updated with nav fix
- Nav "Blogs & articles" link updated from `#` to `blog.html` on all pages

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
blog.html               — Blog index page
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
assets/images/          — logo_claude.svg + team/hero photos
CNAME                   — threeflows.com domain config
.gitignore              — excludes .claude/, blogs/blog_old/, blogs/blog_old2/, blogs/files.zip, blogs/blog_*_*.html
```

**Local-only — not in git:**
```
blogs/                  — draft source files (local archive only)
  blog_001_welcome.html
  blog_drafts_review.html     (contains posts 002–005)
  blog_006_fedex_2026.html
  blog_007_warehouse_placement.html
  blog_008_10usd_product.html
  blog_009_whatnot_breakeven.html
  blog_010a_fulfillment_cost.html
  blog_010b_measurement.html
  blog_old/             — archive folder
  blog_old2/            — archive folder
  files.zip             — archive
```

**Pages in repo whose content is not fully documented (read live file before editing):**
- `about.html` — About/team page. Nav currently links to `index.html#about-anchor` — verify if nav should be updated to point here directly.
- `inquiry.html` — May be an alternate or expanded inquiry form distinct from `intake.html`.
- `webinars.html` — Webinars & seminars. Nav currently shows `#` placeholder.
- `livestream.html` — Livestream discussions. Nav currently shows `#` placeholder.
- `free-tools.html` — Free spreadsheets/tools. Nav currently shows `#` placeholder.
- `threeflows_complete_v6.html` — Full-site consolidated file or design reference. Do not publish.

**Planned future pages (not yet built):**
- Newsletter signup
- Additional intake forms per service
- Additional blog posts (next available ID: 011)

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
│   ├── Blogs & articles → blog.html
│   ├── Business launch checklist → # (placeholder)
│   ├── Useful websites → useful-websites.html
│   ├── Free spreadsheets → # (placeholder)
│   ├── Recorded webinars & seminars → # (placeholder)
│   └── Livestream discussions → # (placeholder)
├── Contact → index.html#contact-anchor
└── [CTA] "Submit an inquiry" → live Google Forms URL (do NOT change)
```

- Both dropdowns use `toggleDropdown(id, event)` with `event.stopPropagation()` — without stopPropagation the dropdown closes immediately on open
- Nav is designed to accommodate future top-level items without layout changes
- `webinars.html`, `livestream.html`, and `free-tools.html` exist in the repo — their nav items currently show `#` placeholders. Update only with explicit instruction.

### Footer

Identical across all pages. Appears exactly once per page, always outside tab panels:

```html
<footer>
  <img src="assets/images/logo_claude.svg" ...> <!-- same as nav logo -->
  <span>© 2026 Three Flows Solutions LLC. All rights reserved.</span>
  <div class="footer-links">
    <a href="mailto:contact@threeflows.com">contact@threeflows.com</a>
    <a href="#">Privacy</a>
    <a href="#">Terms</a>
  </div>
</footer>
```

---

## CTA Buttons

Three standard buttons only. Do not create variants, rename labels, or restyle inline.

| Class         | Label                    | Destination                        |
|---------------|--------------------------|------------------------------------|
| `btn-red`     | Submit an inquiry        | Live Google Forms URL              |
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

Card style across all three tabs:
- Favicon logo (16x16px) left-aligned, fetched from `https://www.google.com/s2/favicons?sz=32&domain=[domain]`
- Name next to logo on same row
- Short intro note below name
- Stage badge (startup / established only — no badge for "both") positioned absolute top-right, no border
- CTA link left-aligned at bottom of card using `margin-top: auto` so CTAs align across cards in the same row
- Tab 3 access type badges: Open / Curated / Vendor — positioned absolute top-right, no border

---

## Blog System

### Overview

The blog is a flat-file system. Every post is a self-contained HTML page in the repo root. There is no CMS, no database, no build step. Adding a new post = create the HTML file in `/Users/swai/multipage/` + add a card to `blog.html`.

### blog.html — Blog Index Page

- **Hero:** "Notes from the Field" heading + subtitle
- **Tag filter bar:** 9 clickable buttons with client-side JS filtering
  - Tags: All | Plan | Source | Launch | Scale | Data | Setup | Compliance | Others
  - Multi-select, OR logic (clicking two tags shows posts matching either)
  - "All" clears selection and shows everything
  - Active tag: `--red` background, white text
  - Each post card has `data-tag="[tag]"` attribute used by the filter JS
- **Post list:** vertical, one card per row, sorted by publish date ascending
  - Each card: image left (260px, Unsplash) | tag pill | date | title | description | "Read →"
  - No post ID badge on cards
  - "+" button for secondary tags — hidden (`display:none`) until `data-extra-tags` attribute is set; hover shows tooltip with extra tag names
- **Tab JS:** none — blog.html has no tabs, filter is standalone JS
- **Breadcrumb:** none — blog.html is a top-level nav page

### Unsplash Images Per Post

Each post card on blog.html uses a fixed Unsplash photo. Append `?w=520&h=360&fit=crop&auto=format` to each URL. All have onerror fallback.

| ID | Unsplash photo ID |
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

### Post ID System

- **Format:** 3-digit numeric, e.g. `001`, `007`, `011`
- **Sequels / multi-part series:** suffix letters A, B, C… e.g. `010A`, `010B`
- **IDs are permanent.** Once published, an ID never changes and its filename never changes.
- **IDs are not publish-date order.** They are assigned sequentially as posts are created.
- **Next available ID:** `011`
- **Filename convention:** `blog-[ID].html` using hyphens, e.g. `blog-001.html`, `blog-010a.html`

### Tag System

Eight tags — mapped to services where possible. Use short labels everywhere (index cards, post meta, filter buttons).

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

Each post currently has one primary tag. Multi-tag support is built in to blog.html (the "+" button) but secondary tags have not yet been assigned. When secondary tags are confirmed, add `data-extra-tags="Tag1, Tag2"` to the relevant post card's `post-tag-more` span — the button will appear automatically.

### Published Posts — Master Table

Sorted by publish date. Tag column uses short labels.

| ID | Filename | Publish Date | Tag | Title |
|---|---|---|---|---|
| 001 | blog-001.html | Mar 5, 2025 | Others | Welcome to Three Flows Solutions: Where Education Meets Execution |
| 002 | blog-002.html | May 26, 2025 | Source | How to Legally Cut Import Costs by Up to 48% |
| 010A | blog-010a.html | Jun 5, 2025 | Launch | Dedicated 3PL Service Can Cost $23.33 Per Order — or $5.71 |
| 004 | blog-004.html | Jun 23, 2025 | Source | Navigating the US-China Tariff War |
| 010B | blog-010b.html | Jul 15, 2025 | Scale | The Fifth M: Why Measurement Is the One That Makes All the Others Work |
| 007 | blog-007.html | Jul 18, 2025 | Scale | Where Should Your Third US Warehouse Be? |
| 003 | blog-003.html | Aug 2, 2025 | Source | Factory Data Problems Are Costing You More Than You Think |
| 005 | blog-005.html | Aug 25, 2025 | Source | Why Data Integrity Is the Foundation of a Scalable Supply Chain |
| 008 | blog-008.html | Sep 12, 2025 | Plan | Is a $1.40 Product Worth Selling in the US? |
| 006 | blog-006.html | Jan 16, 2026 | Scale | Is FedEx's 2026 Rate Increase Really Just 5.9%? |
| 009 | blog-009.html | Feb 2, 2026 | Launch | Why Your Whatnot Livestream Needs a Sell-Through Model |

### Prev/Next Navigation — Publish Date Order

Every post page has a `.post-nav` block above `.post-footer` with prev/next tiles. Order is strictly by publish date:

| Post | ← Previous | Next → |
|---|---|---|
| blog-001 | — | blog-002 |
| blog-002 | blog-001 | blog-010a |
| blog-010a | blog-002 | blog-004 |
| blog-004 | blog-010a | blog-010b |
| blog-010b | blog-004 | blog-007 |
| blog-007 | blog-010b | blog-003 |
| blog-003 | blog-007 | blog-005 |
| blog-005 | blog-003 | blog-008 |
| blog-008 | blog-005 | blog-006 |
| blog-006 | blog-008 | blog-009 |
| blog-009 | blog-006 | — |

### Individual Post Page Rules

Every blog post page must follow these rules:

1. **Breadcrumb:** "← Blog" linking to `blog.html` — immediately below nav, same pattern as svc1–4 breadcrumbs
2. **Nav and footer:** copied exactly from index.html — identical to all other pages
3. **One footer per page** — never inside any content section
4. **Page title format:** `[Post Title] — Three Flows Solutions`
5. **Post meta block:** every post has a `.post-meta` row containing:
   - Post ID badge (e.g. `POST 010A`) — class `post-num`, red background — present on post pages only, not on index cards
   - Publish date — class `post-date`, muted
   - Tag badge — class `post-tag`, short tag name, red text on red-light background
6. **Interactive JS** (charts, maps, simulators) is preserved exactly as written. Do not refactor or simplify.
7. **Review banner** (`<div class="review-banner">`) is present in draft files only — always stripped before publishing.
8. **Prev/next nav** — `.post-nav` block above `.post-footer` on every post (see table above)

### Posts With Interactive Elements

These posts contain embedded JS that must be preserved exactly:

| Post | Library | Feature |
|---|---|---|
| blog-007.html | D3.js | Interactive choropleth US map — 4 scenario toggles (LAX only / EWR only / LAX+EWR / 5-node) |
| blog-008.html | Chart.js | Waterfall cost stack chart |
| blog-009.html | Vanilla JS | Breakeven simulator — 6 sliders, live chart, profit verdict |

### Draft Source Files

Draft files live at `/Users/swai/multipage/blogs/` — **local only, never committed to git** (excluded by `.gitignore`). They are the source originals used to create the published post files. Keep them as a local archive.

| Draft file | Published as |
|---|---|
| blog_001_welcome.html | blog-001.html |
| blog_drafts_review.html | blog-002.html, 003.html, 004.html, 005.html (split by `<article id="postXXX">`) |
| blog_006_fedex_2026.html | blog-006.html |
| blog_007_warehouse_placement.html | blog-007.html |
| blog_008_10usd_product.html | blog-008.html |
| blog_009_whatnot_breakeven.html | blog-009.html |
| blog_010a_fulfillment_cost.html | blog-010a.html |
| blog_010b_measurement.html | blog-010b.html |

### Adding a New Post (workflow)

1. Draft and review the post in Claude Chat (get HTML with review banner)
2. Save draft to `/Users/swai/multipage/blogs/blog_[ID]_[slug].html`
3. Strip the review banner, inject site nav/footer/breadcrumb, add tag pill + prev/next nav
4. Save published file to `/Users/swai/multipage/blog-[ID].html`
5. Add a card to `blog.html` (correct publish date order, correct `data-tag`, correct Unsplash photo)
6. Update prev/next on the neighboring posts (the one that was previously last gets a new "Next →" tile)
7. Add the ID, filename, and photo ID to the master tables in this handoff doc
8. `git add . && git commit -m "Add post [ID]: [title]" && git push`

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
Source: client fulfillment cost analysis Excel (OB cost analysis sheet only). 5-scenario model. Key finding: $23.33 baseline → $5.71 optimized (75% reduction). "July Ops" = Three Flows proposed start state ($15.00, single system, foam, 1 box size). Gradual approach rationale: consume existing foam inventory first; defer multi-box until demand patterns established.
- The $10/hr management fee = Three Flows control tower role (brief mention in 010A, expanded in 010B)
- Growth flywheel: lower cost → reinvest in ads/pricing → higher volume → further compression

**010B — The Fifth M: Measurement**
Companion to 010A. Opens with callback to 010A cost model. Measurement as connective tissue through the 5M framework (Man, Machine, Method, Materials, Measurement). Measurement runs through the entire process: builds the baseline, validates the plan, calibrates in real time, expands to demand forecasting / last-mile / inventory. Closes: "Measure, Model, Monitor, repeat." The Three Flows management fee = ongoing cycle of these three, not a one-time deliverable.

---

## Critical Rules

1. **Tab JS isolation**
   - `setTab()` (svc2): toggles only `tab-0` through `tab-3` by ID — never `querySelectorAll('.ws-content')`
   - `setSvc3Tab()` (svc3): toggles only `svc3-ws-0` through `svc3-ws-3` by ID — never positional querySelectorAll
   - `useful-websites.html` tab function: isolated to its own IDs — never shares class selectors with svc2 or svc3
   - `blog.html` filter JS: standalone, operates only on `.post-card[data-tag]` — no overlap with any tab system

2. **Nav dropdowns** must use `toggleDropdown(id, event)` with `event.stopPropagation()` on every dropdown trigger across all pages

3. **Breadcrumbs:**
   - svc1–4: "← Services" → `index.html#services-anchor`
   - blog-001 through blog-010b: "← Blog" → `blog.html`

4. **One footer per page** — never inside a tab panel or content section

5. **Three CTA buttons only** — no variants, no new classes, no relabelled text

6. **Do not hardcode colors** outside `:root`

7. **Logo file:** `assets/images/logo_claude.svg` — used in both nav and footer, identical in both locations

8. **Blog post IDs are permanent** — never rename a published blog filename

9. **Review banners are draft-only** — always strip `<div class="review-banner">` before publishing

10. **Blog draft files are local-only** — never `git add blogs/` — the `.gitignore` excludes these but verify before committing

11. **Interactive JS in posts** — never rewrite, reformat, or simplify D3 / Chart.js / simulator code in blog-007, blog-008, blog-009

---

## Git Hygiene

- **`.gitignore` excludes:** `.claude/`, `blogs/blog_old/`, `blogs/blog_old2/`, `blogs/files.zip`, `blogs/blog_*_*.html`
- **Baseline commit:** `fece9ef` — blog infrastructure: 11 post files + blog.html + nav updates on all pages
- **Before every commit:** confirm `git status` does not include anything from `blogs/` except the folder itself (which is empty in terms of tracked files)
- **Standard commit pattern for new posts:** `git add blog-[ID].html blog.html && git commit -m "Add post [ID]: [title]" && git push`

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
