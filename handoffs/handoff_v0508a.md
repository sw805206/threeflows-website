# Three Flows Solutions — Website Reference & Handoff
## Version 0508A — Updated May 8, 2026

---

## What Changed Since v0508

### Service Pages Audit & Fixes (May 8, 2026)

A full code-level audit of `svc1.html`, `svc2.html`, `svc3.html`, `svc4.html` was performed covering structure, hero sections, tab JS, CTA buttons, CSS variables, and typography. The following fixes were applied:

**Structural fixes:**
- `svc3.html` — DOM order of tab panels corrected: `svc3-ws-2` (3C Process improvement) was swapped with `svc3-ws-3` (3D System integration). Now correctly ordered `svc3-ws-0 → 1 → 2 → 3`.
- `svc2.html` — Tab 2A: closed `.mob-section` div before `.bg-off` opens, so the FAQ off-white background is no longer clipped to 1100px.

**Class name unification:**
- `svc1.html`, `svc2.html` — Migrated `.svc-hero-wrap / .svc-hero / .svc-hero-sub / .svc-hero-img` → `.hero-wrap / .hero / .hero-sub / .hero-img` to match svc3/svc4. Hero image height standardized to 400px across all 4 pages.
- `svc1.html` — Migrated `.svc-bottom-cta / .svc-bottom-inner` → `.bottom-cta / .bottom-inner` to match svc2/svc3/svc4.

**Tab JS unification (svc2 + svc3):**
- `svc2.html` — Migrated `setTab(idx)` from `el.style.display` toggle to `.ws-content.active` class-toggle pattern, matching svc3. Tab panel divs now carry `class="ws-content"` (or `class="ws-content active"` for tab-0).
- `svc3.html` — Renamed `.svc3-tab-btn` → `.tab-btn` in both HTML and CSS. Both pages now share identical `.tab-btn / .tab-btn.active` rules.

**Button fixes (all 4 pages):**
- Replaced inline `style="background:#333"` on `.btn-dark` and `style="color:white;border-color:rgba(255,255,255,0.4)"` on `.btn-outline` in bottom CTA sections with CSS modifier classes `.btn-dark.on-dark` and `.btn-outline.on-dark`.
- Removed `target="_blank"` from all `<a href="inquiry.html">` and `<a href="intake.html">` links. External calendar booking links confirmed as `target="_blank" rel="noopener"`.

**CSS variable cleanup (all 4 pages):**
- Added `--grey`, `--green-dark`, `--blue-light`, `--blue` to `:root`.
- Replaced hardcoded hex values: `#AAA` → `var(--grey)`, `#EAF3DE` → `var(--green-light)`, `#3B6D11` → `var(--green-dark)`, `#E6F1FB` → `var(--blue-light)`, `#185FA5` → `var(--blue)`.
- Exception preserved: `.nav-cta:hover { background: #333 }` is intentional.

**FAQ background standardization (svc2 + svc3):**
- Target pattern established for all tabs: **grey intro → white main content → grey FAQ → dark bottom CTA**.
- `svc3.html` — All 4 tab FAQ sections wrapped in `bg-off` (previously bare `<div class="section">`).
- `svc2.html` tab 2B — FAQ wrapped in `bg-off` (previously bare `<div class="section">`).
- `svc2.html` tab 2D — Financial callout block ("A contract is a cashflow commitment in disguise") changed from `bg-off` to bare `<div class="section">` (white), eliminating the double-grey run. FAQ keeps its `bg-off`.
- Tabs 2A and 2C were already correct — no change needed.

### Updated CSS Variables

Two new color tokens added to `:root` across all service pages:

```css
--grey: #AAAAAA;
--green-dark: #3B6D11;
--blue-light: #E6F1FB;
--blue: #185FA5;
```

Full canonical `:root` is now:

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
  --green-dark: #3B6D11;
  --grey: #AAAAAA;
  --blue-light: #E6F1FB;
  --blue: #185FA5;
  --radius: 12px;
  --radius-sm: 8px;
  --font-body: 16px;
  --line-height: 1.7;
  --transition: 0.18s ease;
  --warm: #F8F8F8;
  --warm-border: rgba(180,150,100,0.2);
}
```

---

## To-Do List (Future Work)

### 🔴 Do before launch

- **Footer Privacy & Terms links** — All 4 service pages (and all other pages) have `<a href="#">Privacy</a><a href="#">Terms</a>` as placeholders. Replace with real URLs before site goes live. Affects: every page in repo.

### 🟡 Technical debt — schedule when capacity allows

- **Extract shared stylesheet** — Every page currently embeds full CSS inline, with the same `:root`, nav, footer, button, and utility rules duplicated 2–3× per file. Long-term fix is a single `styles.css` linked from every page. This is a significant refactor — do not attempt piecemeal. When ready, audit every page for any per-page-only rules that should not be in the shared sheet.

- **CSS duplication within files** — Related to above. Each service page redefines the same blocks (`:root`, `.btn-red`, `nav`, `.logo`, `.eyebrow`, etc.) 2–3× internally due to copy-paste accumulation. Resolve as part of the shared stylesheet refactor.

- **Inline styles → CSS classes** — Many recurring inline styles should be promoted to named classes. Key offenders across all pages:
  - `style="text-decoration:none;color:inherit"` on breadcrumb links → `.breadcrumb-link`
  - `style="text-align:center;display:block;padding:14px;width:100%;text-decoration:none"` on hero btn-red → `.btn-red.hero-cta`
  - `style="font-size:16px;color:var(--mid);line-height:1.75;font-weight:300"` on section `<p>` tags → `.section-body`
  - Bottom CTA button inline size/padding overrides → consolidate into `.btn-red`, `.btn-dark`, `.btn-outline` base rules

### 🟢 Design / content — review when relevant

- **Continuity banner tone (svc1 vs svc2/3/4)** — svc1's banner explains the fee discount ("Your Stage 01 fee is an investment, not a cost…"), while svc2/3/4 ask about prior engagement. This is a tone divergence, not a bug. Review if you want a more unified voice across the progression.

- **Hero CTA box punctuation** — svc1/svc4 end subtitle with `.`, svc2 ends with `.`, svc3 ends with no period. Minor but worth aligning in a future copy pass.

- **svc4 section padding rhythm** — Philosophy and Control Tower sections use `72px` top/bottom padding vs the standard `64px` on other sections. Creates a slightly looser feel. Intentional or not — flag for design review.

---

## Audit Notes (Decisions Made — No Action Required)

These items were flagged during the May 8 audit and explicitly resolved as non-issues:

- **svc1 "Problem" section vs svc4 "Philosophy" section** — Structural difference is intentional. svc1 and svc4 serve different audiences at different stages. No change needed.
- **svc2 repeated FAQ question** — "How do I know which service (2A/2B/2C/2D) I need?" appears in all 4 tabs. This is a valid UX choice since users may land on any tab. Leave as-is.
- **FAQ section backgrounds on svc1/svc4** — svc1 and svc4 are single-scroll pages; their FAQ sections sit on white and are followed by the dark bottom CTA. This is correct — the grey wrapping pattern only applies inside tab panels on svc2/svc3.

---

## Tab System — Updated Rules

The audit established the following as the canonical tab implementation. Any future tab pages must follow these patterns exactly.

### Tab button class
- Both svc2 and svc3 now use `.tab-btn` / `.tab-btn.active` — do not create new tab button class variants.

### Tab panel show/hide
- All tab panels carry `class="ws-content"` (hidden) or `class="ws-content active"` (visible).
- Show/hide is controlled by `el.classList.toggle('active', i === idx)` — never `el.style.display`.
- CSS rule: `.ws-content { display: none } .ws-content.active { display: block }`

### Tab panel DOM order
- DOM order of tab panels must always match visual tab order (left to right). Never swap panel positions.

### Tab content background rhythm
- Every tab panel follows: **grey (`bg-off`) intro → white (`section`) main content → grey (`bg-off`) FAQ**
- If a tab has an additional grey block before the FAQ, convert it to white to avoid consecutive grey sections.

---

## Button Rules — Updated

Three standard buttons only. Classes, labels, and destinations are fixed.

| Class | Label | Destination | target |
|---|---|---|---|
| `btn-red` | Submit an inquiry | inquiry.html | same tab |
| `btn-outline` | Fill in an intake form | intake.html or `#` | same tab |
| `btn-dark` | Book a call | Booking link or `#` | `_blank` + `rel="noopener"` |

**On dark backgrounds (bottom CTA sections):** use modifier classes `.btn-dark.on-dark` and `.btn-outline.on-dark` — never inline style overrides.

**Internal links** (`inquiry.html`, `intake.html`) never use `target="_blank"`. Only external URLs (calendar, third-party) use `target="_blank" rel="noopener"`.

---

## What Changed Since v0503

### Free Tools Infrastructure (new)
- `free-tools.html` — redesigned as hub page: hero, three-bullet info banner, 2-column tool card grid, dark bottom CTA
- `tool-ck000-template.html` — master checklist template: 8-column table (✓ | # | Task | Tip | Weeks | Owner | Start | Finish), progress bar with 2 gate flags, email gate with 14-day cookie, Apps Script POST, @media print rules
- `tool-ca000-template.html` — master calculator shell: email gate, input/results placeholders, assumptions note
- `tool-000-template.html` — deleted (replaced by the two typed templates above)
- `FREE_TOOLS_APPS_SCRIPT.md` — Apps Script (Code.gs) for "Free Tool Responses" Google Sheet, with deployment instructions and live endpoint URL
- `TOOL_REGISTRY.md` — canonical tool ID registry (see Free Tools System section below)

### Checklists Published
- `tool-ck001.html` — CK001: Pre-Launch Planning Checklist (May 8, 2026)
- `tool-ck002.html` — CK002: Sample Sourcing Checklist (May 8, 2026)
- `tool-ck003.html` — CK003: Voice of Customer Checklist (May 8, 2026)

### Resource Page Standardization
- All 5 resource pages now have consistent hero layout: red label (page name) + H1 (catchy phrase) + subtitle
- Breadcrumbs removed from all resource pages
- Nav dropdown labels updated to sentence case across all pages
- `useful-websites.html` — major redesign: section blocks with off-white background, pills moved to card bottom row, Tab 3 headers collapsed to single combined labels, access types legend removed

### Nav Label Changes (applied to every page in repo)
| Old label | New label |
|---|---|
| Blogs & Articles | Blogs & articles |
| Useful Websites | Useful websites |
| Checklists & Calculators | Checklists & calculators |
| Recorded Webinars & Seminars | Webinars & seminars |
| Livestream Discussions | Livestream schedule |

### Resource Page Hero Standards
| Page | Red label | H1 | Subtitle |
|---|---|---|---|
| blog.html | BLOGS & ARTICLES | Notes from the Field | Analyses, frameworks, and real-world thinking on supply chain, fulfillment, and retail operations. |
| useful-websites.html | USEFUL WEBSITES | The Operator's Toolkit | A curated directory of tools, platforms, and resources for e-commerce sellers and retail businesses. |
| free-tools.html | CHECKLISTS & CALCULATORS | Do the Math. Check the Box. | Simplified tools to help you think through key decisions — no login, no paywall. |
| webinars.html | WEBINARS & SEMINARS | Learn Out Loud | Past sessions on e-commerce operations, sourcing, and retail launch strategy — watch anytime. |
| livestream.html | LIVESTREAM SCHEDULE | Live from the Floor | Join our live sessions on e-commerce operations, sourcing, and launch strategy — open to all or by invitation. |

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
livestream.html         — Livestream schedule page
free-tools.html         — Checklists & calculators hub page
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
tool-ck000-template.html — Checklist master template — DO NOT add a card for this in free-tools.html
tool-ca000-template.html — Calculator master template — DO NOT add a card for this in free-tools.html
tool-ck001.html         — CK001: Pre-Launch Planning Checklist
tool-ck002.html         — CK002: Sample Sourcing Checklist
tool-ck003.html         — CK003: Voice of Customer Checklist
FREE_TOOLS_APPS_SCRIPT.md — Apps Script source + deployment instructions
TOOL_REGISTRY.md        — Canonical tool ID and status registry
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
- Additional checklists: CK004–CK007 (see Pre-Assigned IDs below)
- All calculators: CA001–CA005 (see Pre-Assigned IDs below)

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
  --green-dark: #3B6D11;
  --grey: #AAAAAA;
  --blue-light: #E6F1FB;
  --blue: #185FA5;
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
│   ├── Useful websites → useful-websites.html
│   ├── Checklists & calculators → free-tools.html
│   ├── Webinars & seminars → webinars.html
│   └── Livestream schedule → livestream.html
├── Contact → index.html#contact-anchor
└── [CTA] "Submit an inquiry" → inquiry.html
```

- Both dropdowns use `toggleDropdown(id, event)` with `event.stopPropagation()`
- `toggleDropdown` adds/removes `.open` class on the `<li class="nav-dropdown">` element

### Footer

Identical across all pages:

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

⚠️ Privacy and Terms are placeholder `href="#"` links — replace with real URLs before launch (see To-Do list).

---

## CTA Buttons

Three standard buttons only. Do not create variants, rename labels, or restyle inline.

| Class | Label | Destination | target |
|---|---|---|---|
| `btn-red` | Submit an inquiry | inquiry.html | same tab |
| `btn-outline` | Fill in an intake form | intake.html or `#` | same tab |
| `btn-dark` | Book a call | Booking link or `#` | `_blank` + `rel="noopener"` |

**On dark backgrounds:** use `.btn-dark.on-dark` and `.btn-outline.on-dark` modifier classes — never inline style overrides.

---

## Service Pages — Design Patterns

### Hero
- All 4 pages use `.hero-wrap / .hero / .hero-sub / .hero-img` (unified as of v0508A)
- Hero image height: 400px on all pages
- Breadcrumb: "← Services" → `index.html#services-anchor` on all 4 pages

### Continuity Banner
- Present on all 4 pages with identical `.continuity-banner` structure
- Copy intentionally varies by stage (svc1 explains value; svc2/3/4 reference prior engagement) — this is not a bug

### Tab Pages (svc2, svc3)
- Tab buttons: `.tab-btn` / `.tab-btn.active` on both pages
- Tab panels: `class="ws-content"` (hidden) or `class="ws-content active"` (visible)
- Show/hide mechanic: `el.classList.toggle('active', i === idx)` — never `el.style.display`
- CSS: `.ws-content { display: none } .ws-content.active { display: block }`
- DOM order of panels must always match visual left-to-right tab order
- **Tab content background rhythm:** grey (`bg-off`) intro → white (`section`) main content → grey (`bg-off`) FAQ
- If a tab has an additional grey block immediately before the FAQ, convert it to white to prevent double-grey runs

### Bottom CTA
- All 4 pages use `.bottom-cta / .bottom-inner` (unified as of v0508A)
- Buttons on dark bg use `.btn-dark.on-dark` and `.btn-outline.on-dark`

### FAQ
- All FAQ sections use `.faq-list / .faq-item / toggleFaq(this)` pattern
- On svc2/svc3: FAQ sections are wrapped in `bg-off` on every tab (grey background)
- On svc1/svc4: FAQ sections are bare `section` (white) — correct for single-scroll pages

---

## Free Tools System

### Overview

Free tools are lead-generation assets gated behind a 14-day email cookie. Users submit their name, email, and consent once per tool per 14 days. Submissions are captured in the "Free Tool Responses" Google Sheet via Apps Script.

**Two tool types:**
- **Checklists (CK)** — interactive HTML table with checkboxes, progress bar, gate rows, download blank PDF
- **Calculators (CA)** — input fields with live calculation output, download blank PDF

### Apps Script Endpoint

- **Live URL:** `https://script.google.com/macros/s/AKfycbwEzk-yjtQHV43rF5RAi0dI57s8J3vEwopsc6V8bYwSZOTZWkS-CdegENA5B-ARzaL7Eg/exec`
- **Google Sheet name:** Free Tool Responses
- **Columns:** Timestamp | Tool ID | Tool Name | First Name | Email | Consent
- **Deployed:** May 8, 2026 — no redeployment needed unless script logic changes
- **Fail-open:** if POST fails, cookie is still set and tool is revealed — never block access due to backend failure

### Email Gate Rules

- Cookie name pattern: `tf_tool_ck001`, `tf_tool_ca001` etc.
- Cookie expiry: 14 days from submission
- Gate fields: First name (required), Email (required), Consent checkbox (required)
- Email validation: client-side regex disables submit until valid format entered; on submit calls api.mailcheck.ai to reject disposable domains
- If mailcheck fails: show inline error "Please enter a valid business or personal email address"
- Submit button label: "Access Tool →" — btn-red style
- No skip link

### Tool ID System

| Element | Format | Example |
|---|---|---|
| Checklist base | CK001 | CK001 |
| Checklist revision | CK001A–CK001Z | CK001A |
| Calculator base | CA001 | CA001 |
| Calculator revision | CA001A–CA001Z | CA001A |
| Filename | tool-ck001.html, tool-ca001.html | |
| Cookie | tf_tool_ck001, tf_tool_ca001 | |
| Display to user | Tool name + last revised date only — ID never shown | |

Revision rule: logic change = new letter suffix. At CK001Z, next revision becomes CK002 (may share same tool name). When a revision goes live, previous version card must be removed from free-tools.html.

### Checklist Template Rules (tool-ck000-template.html)

- Always start new checklists from `tool-ck000-template.html` — fetch from GitHub, never build from scratch
- 8-column table: ✓ | # | Task | Tip | Weeks | Owner | Start | Finish
- All table text: 12px, uniform font
- Three row types: phase header (off-white bg, uppercase muted label), task row (checkbox + fields), gate row (--red-light bg, no checkbox, 🚩 badge)
- Gate rows do NOT count toward total task count in progress bar
- Progress bar: 2 gate flag markers by default (3 for CK003 which has 3 gates)
- Flag positions: (tasks_before_gate / total_tasks * 100)%
- Cross-references in tip column: 11px, italic, --red, display block
- Download blank PDF: window.print() — @media print hides nav/footer/gate/banner/CTA; Weeks prints pre-populated; Owner/Start/Finish print as blank underlined lines; gate rows print light grey (#ececec); phase headers print light grey
- Bug report button: small, understated, right-aligned in tool header, mailto:contact@threeflows.com with pre-filled subject and body
- Bottom service CTA: always visible — btn-red (inquiry.html) + btn-outline (intake.html) + "Business Planning service →" (svc1.html)

### Calculator Template Rules (tool-ca000-template.html)

- Always start new calculators from `tool-ca000-template.html`
- Minimal shell — input/output layout varies per calculator, no pre-built rows
- Assumptions note always present below results: "This calculator uses simplified assumptions. Results are indicative only."
- Same gate, cookie, Apps Script, bug report, and CTA rules as checklists

### Bug Report Button (all tool pages)

Every tool page has a small bug report button in the tool header section:
- Right-aligned, same row as or immediately below h1/meta line
- Label: "Report a bug or issue" with ti-bug icon
- Style: 12px, --muted, transparent bg, 0.5px border, padding 6px 12px
- mailto: contact@threeflows.com
- Subject: [Tool Bug] (user completes)
- Body pre-fills: Page URL + Tool name (no ID shown)

### free-tools.html Card Rules

- 2-column grid desktop, 1-column mobile
- Checklists group first (CK ascending), calculators group second (CA ascending)
- Card order is manually specified — not auto-sorted
- Each card: tool name, 2-sentence description, type badge (Checklist/Calculator), last revised date, "Launch Tool →" button, "Need a custom version? Talk to us →" upsell line
- data-type="checklist" or data-type="calculator" on each card
- Tool ID never shown on cards

### TOOL_REGISTRY.md

Canonical registry for all tool IDs, filenames, and status. Always update after publishing a new tool or revision. Source of truth for next available IDs.

### Active Tools

| ID | Type | Tool Name | File | Last Revised |
|---|---|---|---|---|
| CK001 | Checklist | Pre-Launch Planning Checklist | tool-ck001.html | May 8, 2026 |
| CK002 | Checklist | Sample Sourcing Checklist | tool-ck002.html | May 8, 2026 |
| CK003 | Checklist | Voice of Customer Checklist | tool-ck003.html | May 8, 2026 |

### Pre-Assigned IDs

| ID | Type | Tool Name |
|---|---|---|
| CK001 | Checklist | Pre-Launch Planning |
| CK002 | Checklist | Sample Sourcing |
| CK003 | Checklist | Voice of Customer |
| CK004 | Checklist | Company and Brand Setup |
| CK005 | Checklist | Set Up Your Back Office |
| CK006 | Checklist | Launch Playbook |
| CK007 | Checklist | Vendor Scorecard |
| CA001 | Calculator | Landed Cost |
| CA002 | Calculator | Storage Fee |
| CA003 | Calculator | Last Mile Cost |
| CA004 | Calculator | Unit Economics |
| CA005 | Calculator | Inventory Turns |

### Adding a New Tool — Full Workflow

**Step 1 — Design content in Claude Chat**
- Propose task list / calculator logic
- Align on phases, gates, tips, cross-references
- Get sign-off before writing any code

**Step 2 — Send to Claude Code**
Always include in the prompt:
- Fetch tool-ck000-template.html or tool-ca000-template.html from GitHub first
- Fetch free-tools.html and TOOL_REGISTRY.md from GitHub first
- Metadata: tool ID, tool name, cookie name, Apps Script POST fields, mailto body
- Progress bar: total task count, gate flag positions as percentages
- Full table content with exact task text, tips, cross-refs, weeks values
- Print rules reminder
- Card content for free-tools.html
- TOOL_REGISTRY.md update
- Git commit and verify steps

**Step 3 — After commit**
Update this handoff doc: Active Tools table, next available ID

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

### svc1.html — Business Planning
- Breadcrumb "← Services" → `index.html#services-anchor`
- Sections: Hero → Continuity banner → Problem (`problem-bg`, two-col) → Process steps (5) → Deliverables → FAQ → Bottom CTA
- Note: "Problem" framing is intentionally different from svc4's "Philosophy" framing — different audiences, different stage

### svc2.html — Sourcing Consultation
- 4 tabs: 2A Make-or-buy modeling | 2B Sourcing project playbook | 2C Factory visit support | 2D Contract impact analysis
- Tab switching: `setTab(idx)` toggles `.ws-content.active` by ID `tab-0` through `tab-3`
- Tab button class: `.tab-btn` / `.tab-btn.active`
- **Never use `querySelectorAll('.ws-content')` inside `setTab()`**
- Tab background rhythm: grey intro → white content → grey FAQ (see Tab Pages rules above)

### svc3.html — Launch Hypercare
- 4 tabs: 3A Brand asset creation | 3B Launch supply bootcamp | 3C Process design & documentation | 3D System integration
- Tab switching: `setSvc3Tab(idx)` toggles `.ws-content.active` on IDs `svc3-ws-0` through `svc3-ws-3`
- Tab button class: `.tab-btn` / `.tab-btn.active`
- **Never use positional `querySelectorAll('.ws-content')` inside `setSvc3Tab()`**
- DOM order of panels: svc3-ws-0 → svc3-ws-1 → svc3-ws-2 → svc3-ws-3 (corrected in v0508A)
- Tab background rhythm: grey intro → white content → grey FAQ (see Tab Pages rules above)

### svc4.html — Ongoing Management
- Sections: Hero → Continuity banner → Philosophy → Core+Optional services → Control Tower → Boundaries → Growth Path → FAQ → Bottom CTA
- Note: "Philosophy" framing is intentionally different from svc1's "Problem" framing

### useful-websites.html — Resource Directory
Three tabs. Tab switching uses an isolated function (check live file for exact function name).

**Tab 1 — Market Insights & Compliance**
Three category sections: Global Trade Data | Market Research | Compliance & IP

**Tab 2 — Business Management**
Ten category sections: Company Formation | Domain & Hosting | Website Builder | Product & Analytics | Marketing & Growth | Collaboration | CRM | Logistics & Ops | Finance & Payments | HR & Hiring

**Tab 3 — Top E-Commerce Marketplaces**
Section headers use combined label format: "Amazon Seller Central — North America", "Regional marketplaces — Europe" etc.
Cards: pills at bottom row alongside Intro/Sign up link. No access types legend.

---

## Blog System

### Overview

Flat-file system. Every post is a self-contained HTML page. No CMS, no database, no build step. Adding a new post = create the HTML file + add a card to `blog.html`.

### blog-000-template.html

Always fetch from GitHub before starting a new post:
```
https://raw.githubusercontent.com/sw805206/threeflows-website/main/blog-000-template.html
```

### blog.html

- Hero: "Notes from the Field" + subtitle
- Tag filter: All | Plan | Source | Launch | Scale | Data | Setup | Compliance | Others
- Post list: newest-first, 5 per page, paginated
- Cards: image left (260px), 8 tag pills, date, title, excerpt, "Read ↗"

### Post Meta — Tag Pills

Fixed order: Plan | Source | Launch | Scale | Data | Setup | Compliance | Others
Classes: `primary` (pink bg), `secondary` (grey bg), `empty` (faint decorative)

### Published Posts — Master Table

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

**Next available post ID: 021**

### Prev/Next Navigation — Publish Date Order

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

### Unsplash Images Per Post

Append `?w=520&h=360&fit=crop&auto=format` to Unsplash URLs.

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

### Amazon Series — Special Notes

Posts 014–020 form the **"Inside Amazon's Supply Chain"** series:
- All photos embedded as base64 data URIs — do not replace with Unsplash URLs
- Each post contains a `.series-nav` block at bottom listing all 7 posts
- Current post highlighted: `class="series-item series-current"` (non-clickable, red bg)
- Series reading order: 014 → 015 → 017 → 018 → 016 → 019 → 020

---

## Individual Post Page Rules

1. Always start from `blog-000-template.html` — fetch live from GitHub
2. Breadcrumb: `← Blog` → `blog.html`
3. `.post-nav` block **above** `.layout`, immediately after breadcrumb
4. Nav and footer identical to all other pages
5. One footer per page
6. Page title: `[Post Title] — Three Flows Solutions`
7. `.post-meta` row: publish date left + all 8 tag pills right
8. No post ID badge on post pages
9. Interactive JS preserved exactly as written

### Posts With Interactive Elements

| Post | Library | Feature |
|---|---|---|
| blog-007.html | D3.js | Interactive choropleth US map — 4 scenario toggles |
| blog-008.html | Chart.js | Waterfall cost stack chart |
| blog-009.html | Vanilla JS | Breakeven simulator — 6 sliders, live chart |

---

## Critical Rules

1. **Always start new posts from `blog-000-template.html`** — fetch from GitHub, never build from scratch
2. **Always start new checklists from `tool-ck000-template.html`** — fetch from GitHub, never build from scratch
3. **Always start new calculators from `tool-ca000-template.html`** — fetch from GitHub, never build from scratch
4. **Prev/next nav position** — `.post-nav` block is always **above** `.layout`, never inside it
5. **No post ID badge on post pages** — `.post-num` does not appear; only date + tag pills in `.post-meta`
6. **No tool ID shown anywhere visible** — tool pages and free-tools.html cards never display CK/CA IDs
7. **blog.html card order is newest-first** — insert at correct chronological position
8. **free-tools.html card order** — checklists first (CK ascending), calculators second (CA ascending), manually overridden per deploy
9. **Three files always need prev/next updates** when inserting a new blog post in the middle of the chain
10. **Tab JS isolation**
    - `setTab()` (svc2): toggles only `tab-0` through `tab-3` by ID — never `querySelectorAll('.ws-content')`
    - `setSvc3Tab()` (svc3): toggles only `svc3-ws-0` through `svc3-ws-3` by ID
    - `useful-websites.html` tab function: isolated to its own IDs
    - `blog.html` filter + pagination JS: standalone, operates only on `.blog-card[data-tag]`
11. **Nav dropdowns** must use `toggleDropdown(id, event)` with `event.stopPropagation()`
12. **Breadcrumbs:**
    - svc1–4: "← Services" → `index.html#services-anchor`
    - All blog posts: "← Blog" → `blog.html`
    - All tool pages: "← Free Tools" → `free-tools.html`
    - Resource pages: no breadcrumb
13. **One footer per page** — never inside a tab panel or content section
14. **Three CTA buttons only** — no variants, no new classes, no relabelled text
15. **Do not hardcode colors** outside `:root`
16. **Logo file:** `assets/images/logo_claude.svg` — used in both nav and footer
17. **Blog post IDs are permanent** — never rename a published blog filename
18. **Tool IDs are permanent** — never rename a published tool filename
19. **Review banners are draft-only** — always strip `<div class="review-banner">` before publishing
20. **Blog draft files are local-only** — never `git add blogs/`
21. **Interactive JS in posts** — never rewrite blog-007, blog-008, blog-009 JS
22. **Amazon series posts (014–020)** — images are base64 embedded; preserve `.series-nav` block
23. **Tool Apps Script** — always use fail-open pattern; never block tool access due to POST failure
24. **tool-ck000-template.html and tool-ca000-template.html** — never get cards in free-tools.html
25. **TOOL_REGISTRY.md** — always update after publishing or retiring a tool
26. **Internal links never open in new tab** — `inquiry.html` and `intake.html` links must not have `target="_blank"`; only external URLs (calendar, third-party) use `target="_blank" rel="noopener"`
27. **Tab FAQ backgrounds** — on svc2/svc3, every tab FAQ section must be wrapped in `bg-off`; if a tab has another `bg-off` block immediately before the FAQ, convert that block to a bare `section` (white) to avoid double-grey

---

## Git Hygiene

- **`.gitignore` excludes:** `.claude/`, `blogs/blog_old/`, `blogs/blog_old2/`, `blogs/files.zip`, `blogs/blog_*_*.html`
- **Before every commit:** confirm `git status` does not include anything from `blogs/`
- **Standard commit pattern for new blog posts:**
  `git add blog-[ID].html blog.html blog-[PREV].html blog-[NEXT].html && git commit -m "Add post [ID]: [title]" && git push`
- **Standard commit pattern for new tools:**
  `git add tool-[ID].html free-tools.html TOOL_REGISTRY.md && git commit -m "Add [ID]: [tool name]" && git push`
- **For blog.html-only changes:**
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
| free-tools.html | Checklists & Calculators — Three Flows Solutions |
| blog.html | Blogs & Articles — Three Flows Solutions |
| tool-ck001.html | Pre-Launch Planning Checklist — Three Flows Solutions |
| tool-ck002.html | Sample Sourcing Checklist — Three Flows Solutions |
| tool-ck003.html | Voice of Customer Checklist — Three Flows Solutions |
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
