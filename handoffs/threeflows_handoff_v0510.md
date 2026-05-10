# Three Flows Solutions — Website Reference & Handoff
## Version 0510 — Updated May 10, 2026

---

## How to use this file

This file covers **operational rules only** — file structure, page inventory, component IDs, git workflow, and content decisions.

**For all visual and UX rules, see `STYLE.md` in the repo root.** Do not add style-related content here.

---

## What Changed Since v0509A

### Style Audit & Infrastructure Session (May 10, 2026)

This session covered a full site-wide code audit against v0509A, creation of `STYLE.md` and `CLAUDE.md`, resolution of 13 style consistency issues, and establishment of the Claude Code workflow protocol.

---

### New Files Added

**`STYLE.md`** — Visual and UX source of truth. All style decisions live here. Read before writing any code.

**`CLAUDE.md`** — Standing instructions for every Claude Code session. Auto-loaded by Claude Code at startup. Contains the mandatory git sync sequence and file-reading requirements.

---

### Code Audit Fixes (May 10, 2026)

The following issues were identified and resolved across the repo:

**Global (all pages):**
- Services dropdown number prefixes (`01 — ` etc.) removed from all remaining pages that still had them (contact, about, free-tools, all tool-ck, all blog posts, blog.html, inquiry, intake, livestream, useful-websites, webinars)
- Nav CTA button removed from all blog post pages and tool-ck001–004
- Contact nav link fixed to `contact.html` on all blog posts and tool-ck001–004

**contact.html:**
- Hero eyebrow changed from "GET IN TOUCH" → "CONTACT US"
- `<h2 class="contact-h2">` → `<h1 class="contact-h1">` with matching CSS rename
- Panel 3 button class changed from `btn-red` → `btn-outline`
- Bespoke `.contact-eyebrow` class replaced with standard `.eyebrow.red`

**svc1–4.html:**
- Hero top padding aligned — all four service pages now match resource page eyebrow Y position
- FAQ wrapper on svc1 changed from `.svc-section` → `.section` to match svc2/3/4
- FAQ eyebrow on svc1 changed from `eyebrow` → `eyebrow muted` to match svc2/3/4
- svc4 non-standard 72px padding on `.philosophy-inner` and `.tower-inner` corrected to 64px

**tool-ck001–004.html:**
- White tool footer card class renamed from `.bottom-cta` → `.tool-cta-card` (`.bottom-cta` is now exclusively the dark sitewide bar)
- Duplicate `inline-cta` paragraph removed from `.below-table` on ck001/002/003

**free-tools.html + index.html:**
- Resource and tool cards converted to flex column layout with `margin-top:auto` on `.cta-link` — pins `Go →` / `Get it for free →` links to card bottom
- `btn-red on-dark` modifier standardized on all bottom CTA buttons that sit on dark backgrounds

**blog posts:**
- Hardcoded inline callout styles (`style="background:#F8F8F8; border-left-color:#1A1A1A"`) replaced with `.callout-grey` class
- blog-021 stray `btn-red` → `inquiry.html` replaced with `.cta-link` → `contact.html`

**All pages:**
- `.cta-link` class introduced — replaces all inline red text link styles
- Arrow direction standardized: `→` for internal links, `↗` for external links with `target="_blank" rel="noopener"`
- `.section-title` duplicate CSS declarations cleaned up — canonical value is 36px

---

### Claude Code Workflow — Established

Every Claude Code session must begin with:

```
1. cd /Users/swai/multipage
2. git fetch origin
3. git checkout main
4. git pull origin main
5. Create a new working branch from this clean state
6. Read STYLE.md from the repo root
7. Read handoffs/threeflows_handoff_v0510.md from the repo root
```

This is now encoded in `CLAUDE.md` at the repo root and auto-loads every session.

**Root cause of stale file issues:** Local files at `/Users/swai/multipage` are not always in sync with GitHub. The git sync sequence above guarantees local = GitHub main before any file is read or edited.

---

## Current File Structure

```
CLAUDE.md               — Standing instructions for every Claude Code session (NEW)
STYLE.md                — Visual and UX source of truth (NEW)
contact.html            — Contact Us page — 3-card step strip (inquiry / intake / feedback)
index.html              — Home page
svc1.html               — Business Planning
svc2.html               — Sourcing Consultation
svc3.html               — Launch Hypercare
svc4.html               — Ongoing Management
about.html              — About page (id="selected-work" on clients section)
free-tools.html         — Checklists & calculators hub
tool-ck001.html         — CK001: Pre-Launch Planning Checklist
tool-ck002.html         — CK002: Sample Sourcing Checklist
tool-ck003.html         — CK003: Voice of Customer Checklist
tool-ck004.html         — CK004: Company and Brand Setup Checklist
blog.html               — Blog index
blog-001.html           — blog-021.html: Blog posts
blog-000-template.html  — Blog post template
inquiry.html            — Inquiry form (destination from contact.html panel 1)
intake.html             — Intake form (destination from contact.html panel 2)
useful-websites.html    — Useful websites resource page
webinars.html           — Webinars & seminars resource page
livestream.html         — Livestream schedule resource page
```

---

## Page Titles

| File | `<title>` |
|---|---|
| index.html | Three Flows Solutions — From Start to Scale |
| contact.html | Contact Us — Three Flows Solutions |
| svc1.html | Business Planning — Three Flows Solutions |
| svc2.html | Sourcing Consultation — Three Flows Solutions |
| svc3.html | Launch Hypercare — Three Flows Solutions |
| svc4.html | Ongoing Management — Three Flows Solutions |
| about.html | About — Three Flows Solutions |
| free-tools.html | Free Tools & Checklists — Three Flows Solutions |
| blog.html | Blog — Three Flows Solutions |
| blog-NNN.html | [Post title] — Three Flows Solutions |
| useful-websites.html | Useful Websites — Three Flows Solutions |
| webinars.html | Webinars & Seminars — Three Flows Solutions |
| livestream.html | Livestream Schedule — Three Flows Solutions |

Format rule: `[Page Name] — Three Flows Solutions`

---

## contact.html — Component Reference

**Step strip:**
- 3 cards side by side, no arrows between them
- Card 1 (Submit an inquiry) — default active, dark background `#1A1A1A`
- Card 2 (Fill in intake form) — inactive by default
- Card 3 (Send feedback) — inactive by default
- Clicking a card activates it and shows detail panel below

**Card IDs:** `id="inquiry"`, `id="intake"`, `id="feedback"`

**Card destinations:**
| Card | Button | Class | Destination |
|---|---|---|---|
| 1 — Submit an inquiry | Submit an inquiry | `btn-red` | `inquiry.html` |
| 2 — Fill in intake form | Fill in intake form | `btn-red` | `intake.html` |
| 3 — Send feedback | Send feedback | `btn-outline` | mailto (see below) |

**Feedback mailto:**
`contact@threeflows.com?subject=Feedback&body=Page%20URL%3A%20%0ATool%20name%20(if%20applicable)%3A%20%0AFeedback%3A%20`

**JS:** `setContactTab(n)` — scoped, does not conflict with `setTab()` (svc2) or `setSvc3Tab()` (svc3)

**No bottom CTA section** — contact.html ends at footer.

---

## Tool Pages — Component Reference

**Active tools:**
| ID | File | Title | Last revised |
|---|---|---|---|
| CK001 | tool-ck001.html | Pre-Launch Planning Checklist | May 8, 2026 |
| CK002 | tool-ck002.html | Sample Sourcing Checklist | May 8, 2026 |
| CK003 | tool-ck003.html | Voice of Customer Checklist | May 8, 2026 |
| CK004 | tool-ck004.html | Company and Brand Setup Checklist | May 8, 2026 |

**Next available ID:** CK005

**Standard tool page pattern:**
- Breadcrumb: `← Free Tools` → `free-tools.html`
- Email gate: side-by-side 50/50 flex layout (First name + Email)
- Gate button: `btn-red` "Access Tool →" — JS gate reveal
- No info banner
- Bottom section: `.tool-cta-card` (white bordered card, NOT `.bottom-cta`)
  - Plain text line: "Need a version built for your business? [Submit an inquiry →](inquiry.html)"
  - Plain text link: "Report a bug or suggest an improvement →" → feedback mailto

**Bug report mailto:**
`contact@threeflows.com?subject=Feedback&body=Page%20URL%3A%20%0ATool%20name%3A%20%0AFeedback%3A%20`

---

## Blog — Component Reference

**Chain:** blog-001 through blog-021 (21 posts as of May 10, 2026)
**Next post ID:** blog-022
**Template:** blog-000-template.html

**Standard blog post pattern:**
- Breadcrumb: `← Blog` → `blog.html`
- Prev/Next cards above post meta
- Tag pills row (primary tag highlighted)
- No bottom CTA section

**Callout variants in use:** `.callout`, `.callout-grey`, `.callout.green`, `.callout.blue`
Never use inline styles for callouts — always use the class. See STYLE.md section 6.

---

## Tab System Reference

**svc2.html:** `setTab(idx)` — tabs 2A, 2B, 2C, 2D
**svc3.html:** `setSvc3Tab(idx)` — tabs 3A, 3B, 3C, 3D
**contact.html:** `setContactTab(n)` — cards 1, 2, 3

JS function names are intentionally scoped per page — do not rename or consolidate.

---

## To-Do List (Future Work)

### 🔴 Do before launch

- **Footer Privacy & Terms links** — All pages have `<a href="#">Privacy</a><a href="#">Terms</a>` as placeholders. Replace with real URLs before site goes live. Affects every page in repo.

- **Google Form URLs** — Replace placeholder destinations on contact.html when live forms are ready:
  - Panel 1 "Submit an inquiry" → currently `inquiry.html` (may stay or swap to Google Form)
  - Panel 2 "Fill in intake form" → currently `intake.html` (may stay or swap to Google Form)
  - Panel 3 "Send feedback" → mailto already set, no form needed

- **`inquiry.html` and `intake.html` nav** — These pages still have the old nav structure. Update nav to match the rest of the site (no CTA button, correct Contact link, no number prefixes in Services dropdown).

### 🟡 Technical debt — schedule when capacity allows

- **Extract shared stylesheet** — Every page embeds full CSS inline with `:root`, nav, footer, button rules duplicated. Extract to single `styles.css` after STYLE.md is fully stable. Do not attempt piecemeal. See STYLE.md section 8 for full debt list.

- **`contact.html` mobile layout** — 3-card step strip collapses to vertical stack on mobile. Verify detail panels render correctly on small screens before launch.

- **Style audit — remaining chunks** — The following were not formally completed in Session C and should be covered in the next audit session:
  - Basic chunk 5: highlighted sections full alignment
  - In-page chunk 1: section separators
  - In-page chunk 2: tabs/toggles deeper review
  - In-page chunk 3: typography and spacing full pass

### 🟢 Design / content — review when relevant

- **Continuity banner tone (svc1 vs svc2/3/4)** — svc1 explains fee discount; svc2/3/4 reference prior engagement. Tone divergence is intentional. Review if unified voice is wanted.

- **Hero CTA box punctuation** — Minor inconsistency across service pages. Align in a future copy pass.

- **"Contact us →" anchor destinations** — In-page links on service pages point to `contact.html` root. Consider `contact.html#inquiry` for svc1 and `contact.html#intake` for svc2/3/4 to improve flow. Not urgent.

- **Blog prev/next card size** — Cards are currently large bordered boxes. Discussed reducing size in Session A — pending separate design decision.

---

## Audit Notes (Decisions Made — No Action Required)

Carried forward:
- **svc1 "Problem" section vs svc4 "Philosophy" section** — intentional structural difference.
- **svc2 repeated FAQ question** — valid UX choice, leave as-is.
- **"Book a call" absent from contact page** — deliberate process decision. Calls are team-initiated after inquiry review. Do not add without revisiting the contact page design.
- **Nav CTA button removed** — deliberate simplification. Do not re-add without a clear reason.
- **Bottom CTA is one button** — contact page handles routing. Do not revert to multi-button.
- **contact.html step-strip uses separate CSS namespace** from svc tab strips — intentional, do not merge.
- **Multi-color callouts in blog posts** — intentional. `.callout`, `.callout-grey`, `.callout.green`, `.callout.blue` are all valid. Inline style overrides are not.

New decisions May 10:
- **svc1–4 hero spacing** — all four service pages now match resource page eyebrow Y position. This is the canonical alignment going forward.
- **`.bottom-cta` class** — reserved exclusively for the dark sitewide bar. Tool page footer uses `.tool-cta-card`. Do not reuse `.bottom-cta` for white card contexts.
- **Arrow convention** — `→` for internal links, `↗` for external links. Never mix.

---

## Git Hygiene

**Standard workflow:**
- Always work on a branch — never commit directly to main
- Claude Code opens PRs via GitHub REST API — merging is always a manual step
- After merge, GitHub Pages redeploys in ~1–2 minutes. CDN propagation up to 10 minutes for new files.

**Before every Claude Code session:**

```
cd /Users/swai/multipage
git fetch origin
git checkout main
git pull origin main
```

This is encoded in CLAUDE.md and auto-loads. Never skip it.

**Commit message conventions:**
- Style fixes: `"Style audit fixes — [description] ([issue refs])"`
- New pages: `"Add [filename] — [one-line description]"`
- Content updates: `"[filename]: [what changed]"`
- Infrastructure: `"Add/Update [filename] — [purpose]"`
