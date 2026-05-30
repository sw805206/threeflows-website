# Three Flows Solutions — Website Reference & Handoff
## Version 0509A — Updated May 9, 2026

---

## What Changed Since v0508A

### Contact Page & CTA Redesign Session (May 9, 2026)

This session covered the creation of a new `contact.html` page, a full redesign of the CTA system across the site, and a series of cleanup changes to the home page, service pages, free tools hub, and individual tool pages.

---

### New File: `contact.html`

A new top-level contact page was created. It replaces `inquiry.html` as the primary contact destination across the site.

**Page structure:**
- Hero: red label "CONTACT US", H1 "How should we connect?", subtitle "Choose the right path below — we'll make sure you reach the right place."
- Main section: 3-card step strip (see design pattern below)
- No bottom CTA section (removed — page ends at footer)

**Step strip design:**
- 3 cards side by side, no arrows between them
- Card 1 (Submit an inquiry) — default active, dark background `#1A1A1A`
- Card 2 (Fill in intake form) — inactive by default
- Card 3 (Send feedback) — inactive by default
- Clicking a card activates it (dark bg, white text, red number circle) and shows a detail panel below the strip
- All 3 cards are clickable — no permanently muted cards
- Detail panel sits directly below the strip, connected visually (border-top: none, rounded bottom corners only)

**Card destinations (detail panel buttons):**
| Card | Button label | Destination |
|---|---|---|
| 1 — Submit an inquiry | Submit an inquiry (btn-red) | `inquiry.html` |
| 2 — Fill in intake form | Fill in intake form (btn-red) | `intake.html` |
| 3 — Send feedback | Send feedback (btn-outline) | `mailto:contact@threeflows.com?subject=Feedback&body=Page%20URL%3A%20%0ATool%20name%20(if%20applicable)%3A%20%0AFeedback%3A%20` |

**Anchor IDs on cards:** `id="inquiry"`, `id="intake"`, `id="feedback"`

**Tab JS:** Function `setContactTab(n)` — scoped name, does not conflict with `setTab()` (svc2) or `setSvc3Tab()` (svc3). Cards carry `class="contact-tab-card"`, panels carry `class="contact-panel"`.

**Number circle behavior:** CSS-driven — `.contact-tab-card .num-circle` is outlined/muted by default; `.contact-tab-card.active .num-circle` becomes red filled. No hardcoded color classes on circles.

---

### Nav Changes (all pages)

- **Nav CTA button removed entirely** — the top-right "Submit an inquiry" / "Contact Us" button has been removed from the nav on all pages. Nav ends at the last nav link.
- **"Contact" nav link** updated to point to `contact.html` (was `index.html#contact-anchor`)
- **Services dropdown** — number prefixes removed from all 4 items:
  - "01 — Business Planning" → "Business Planning"
  - "02 — Sourcing Consultation" → "Sourcing Consultation"
  - "03 — Launch Hypercare" → "Launch Hypercare"
  - "04 — Ongoing Management" → "Ongoing Management"

---

### Bottom CTA — Updated Rules

The bottom CTA section (dark background, `.bottom-cta / .bottom-inner`) has been simplified across all pages.

**New standard pattern (all pages except `contact.html`):**
- Single btn-red button only — label "Contact Us", `href="contact.html"`, same tab
- No secondary text links below the button
- Two-column layout: headline + subtitle left (70%), button right (30%)

**`contact.html`:** No bottom CTA section at all — removed entirely.

**Per-page headlines:**
| Page | Headline |
|---|---|
| index.html | "Ready to build your e-commerce business?" |
| svc1.html | "Ready to build your plan?" |
| svc2.html | "Ready to find the right supplier?" |
| svc3.html | "Ready to launch with confidence?" |
| svc4.html | "Ready for ongoing support?" |
| All other pages | Inherited from prior version — verify live file |

**Subtitle (all service pages):** "Start with a discovery call or send us your question — we'll take it from there."
**Subtitle (index.html):** "First conversation is always free. Choose how you'd like to connect."

---

### Button Rules — Updated

The three-button system from v0508A has been replaced. The site now uses a simpler CTA hierarchy.

| Location | Element | Label | Destination |
|---|---|---|---|
| Bottom CTA (dark bg, all pages except contact) | `btn-red` | Contact Us | `contact.html` |
| In-page service CTAs (hero/mid-page) | Red text link | Contact us → | `contact.html` |
| contact.html panel 1 | `btn-red` | Submit an inquiry | `inquiry.html` |
| contact.html panel 2 | `btn-red` | Fill in intake form | `intake.html` |
| contact.html panel 3 | `btn-outline` | Send feedback | mailto (see above) |
| Tool pages gate | `btn-red` | Access Tool → | reveals tool (JS) |
| Tool pages inline | Red text link | Submit an inquiry → | `inquiry.html` |

**Old btn-dark ("Book a call") and btn-outline ("Fill in an intake form") have been removed from all bottom CTA sections.** They exist only inside `contact.html` panels now.

**In-page red text link style:**
```css
color: var(--red);
font-weight: 600;
font-size: 15px;
text-decoration: none;
/* hover: text-decoration: underline */
```

---

### `index.html` Changes

- **"See how we work →"** — `text-decoration:none` added
- **"See full details →"** (×4, one per stage) — `text-decoration:none` added
- **"Meet the full team" button** — removed
- **"Stay notified when new resources drop" newsletter block** — removed entirely
- **"Get started" section** (`id="contact-anchor"`) — removed entirely
- **Stage eyebrow labels** in the "How we work" step detail panels — removed ("Stage 01 — Plan" etc.)
- **Partner strip** — changed from "Trusted partner of · NYC Small Business Services · Webinar presenter & curriculum partner" to "Trusted partner of · NYC Small Business Services and [more...](about.html#selected-work)" — "more..." links to the Selected Work section on about.html
- **Bottom CTA** — new standard dark CTA added above footer (see Bottom CTA section above)

---

### Service Pages (`svc1–4.html`) Changes

- **"← Services" breadcrumb** — removed from all 4 pages
- **Stage eyebrow labels simplified:**
  - "Stage 01 — Plan" → "Plan"
  - "Stage 02 — Source" → "Source"
  - "Stage 03 — Launch" → "Launch"
  - "Stage 04 — Grow" → "Grow"
- **In-page "Submit an inquiry" btn-red** (hero/mid-page callout boxes) — replaced with red text link "Contact us →" pointing to `contact.html`
- **Bottom CTA** — redesigned to single "Contact Us" button, two-column layout (see Bottom CTA section above)

---

### `about.html` Changes

- **"← Home" breadcrumb** — removed
- **`id="selected-work"`** — added to the "Selected work / Some of our clients" section for direct linking from index.html

---

### `free-tools.html` Changes

- **Info banner** — "Every business is different. For a version built around your actual numbers: [Business Planning →] · [Submit an intake form →]" replaced with: "Every business is different. For a version built around your scenario, let's talk. [Contact us →](contact.html)" — red text link style
- **"Need a custom version? Talk to us →"** — removed from all 3 tool cards
- **"Launch Tool →" button** — replaced with red text link "Get it for free →" on all 3 cards, linking to same tool page

---

### Tool Pages (`tool-ck001`, `tool-ck002`, `tool-ck003`) Changes

- **Red/pink info banner** ("These tools are free and simplified…") — removed entirely
- **Email gate form fields** — First name and Email changed from stacked (full width) to side-by-side single row (50/50 flex), reducing vertical height of the gate box
- **"Need a version built for your business?" CTA** — all buttons removed; replaced with plain text line: "Need a version built for your business? [Submit an inquiry →](inquiry.html)" — red text link style
- **"Report a bug or issue" button** — removed from header area; replaced with plain text link "Report a bug or suggest an improvement →" placed below the inquiry line, pointing to feedback mailto
  - mailto: `contact@threeflows.com?subject=Feedback&body=Page%20URL%3A%20%0ATool%20name%3A%20%0AFeedback%3A%20`

---

## Updated File Structure

```
contact.html            — NEW: Contact Us page — 3-card step strip (inquiry / intake / feedback)
index.html              — Home page (updated: nav, partner strip, CTA sections, bottom CTA)
svc1.html               — Business Planning (updated: nav, breadcrumb, labels, CTAs, bottom CTA)
svc2.html               — Sourcing Consultation (updated: same as svc1)
svc3.html               — Launch Hypercare (updated: same as svc1)
svc4.html               — Ongoing Management (updated: same as svc1)
about.html              — About page (updated: breadcrumb removed, anchor added)
free-tools.html         — Checklists & calculators hub (updated: banner, card CTAs, buttons)
tool-ck001.html         — CK001: Pre-Launch Planning Checklist (updated: banner, form, CTAs)
tool-ck002.html         — CK002: Sample Sourcing Checklist (updated: same as ck001)
tool-ck003.html         — CK003: Voice of Customer Checklist (updated: same as ck001)
inquiry.html            — Inquiry form (unchanged — still the destination from contact.html panel 1)
intake.html             — Intake form (unchanged — still the destination from contact.html panel 2)
```

All other files unchanged from v0508A.

---

## Updated Page Titles

| File | `<title>` |
|---|---|
| contact.html | Contact Us — Three Flows Solutions |
| *(all others unchanged from v0508A)* | |

---

## To-Do List (Future Work)

### 🔴 Do before launch

- **Footer Privacy & Terms links** — All pages have `<a href="#">Privacy</a><a href="#">Terms</a>` as placeholders. Replace with real URLs before site goes live. Affects every page in repo.

- **Google Form URLs** — The following buttons on `contact.html` currently use placeholder `href="#"` or point to internal HTML pages. Replace with live Google Form URLs when ready:
  - Panel 1 "Submit an inquiry" → currently `inquiry.html` (may stay as-is or swap to Google Form)
  - Panel 2 "Fill in intake form" → currently `intake.html` (may stay as-is or swap to Google Form)
  - Panel 3 "Send feedback" → mailto set, no form needed

- **"Book a call" calendar link** — `contact.html` panel 3 references a team-sent invite. If a self-serve calendar link becomes available, update Panel 3 to re-enable the Book a Call card with a real `href`.

### 🟡 Technical debt — schedule when capacity allows

- **`style.md` — design system documentation** — Planned but not yet created. Should document: canonical `:root` CSS variables, all button classes and usage rules, nav/footer shared HTML patterns, tab system patterns, section background rhythm, in-page CTA text link style, bottom CTA layout spec, mobile breakpoint rules. This will serve as the reference for Claude Code when building new pages or components. **Create this file before the next major page build.**

- **Extract shared stylesheet** — Every page currently embeds full CSS inline, with the same `:root`, nav, footer, button, and utility rules duplicated across files. Long-term fix is a single `styles.css` linked from every page. Do not attempt piecemeal. When ready, audit every page for per-page-only rules before extracting. `style.md` should be completed first to define what goes in the shared sheet.

- **CSS duplication within files** — Each page redefines the same blocks (`:root`, `.btn-red`, `nav`, etc.) 2–3× internally. Resolve as part of the shared stylesheet refactor.

- **Inline styles → CSS classes** — Recurring inline styles that should be promoted to named classes:
  - Red text link CTA (`color:var(--red); font-weight:600; text-decoration:none`) → `.cta-link`
  - `style="text-decoration:none;color:inherit"` on breadcrumb links → `.breadcrumb-link`
  - `style="font-size:16px;color:var(--mid);line-height:1.75;font-weight:300"` on section `<p>` tags → `.section-body`
  - Bottom CTA secondary text links (now removed, but style pattern should be documented in `style.md`)

- **`.nav-cta` CSS rule** — The nav CTA button class and its CSS rule (`.nav-cta:hover { background: #333 }`) still exist in every page's `<style>` block even though the button has been removed from the HTML. Clean up the dead CSS as part of the shared stylesheet refactor.

- **`contact.html` — mobile layout** — The 3-card step strip collapses to a vertical stack on mobile. Verify the detail panels render correctly below each card on small screens. No report of issues yet — flag for QA before launch.

### 🟢 Design / content — review when relevant

- **`inquiry.html` and `intake.html`** — These pages still exist as standalone destinations linked from `contact.html`. Their nav still shows the old CTA button structure (now removed everywhere else). Verify their nav is updated to match the rest of the site and that their bottom CTA section (if any) follows the new standard pattern.

- **Continuity banner tone (svc1 vs svc2/3/4)** — svc1's banner explains the fee discount; svc2/3/4 reference prior engagement. Tone divergence is intentional. Review if you want a more unified voice.

- **svc4 section padding rhythm** — Philosophy and Control Tower sections use `72px` top/bottom vs standard `64px`. Flag for design review.

- **Hero CTA box punctuation** — Minor inconsistency across service pages. Worth aligning in a future copy pass.

- **"Contact us →" in-page links on service pages** — These currently point to `contact.html` (root). Consider whether specific anchor destinations (`contact.html#inquiry` for svc1, `contact.html#intake` for svc2/3/4) would improve user flow. Not urgent — root contact page is clear enough.

---

## Audit Notes (Decisions Made — No Action Required)

Carried forward from v0508A:

- **svc1 "Problem" section vs svc4 "Philosophy" section** — intentional structural difference.
- **svc2 repeated FAQ question** — valid UX choice, leave as-is.
- **FAQ section backgrounds on svc1/svc4** — white is correct for single-scroll pages.

New decisions made May 9:

- **"Book a call" removed from contact page** — The 3-card strip intentionally has no "Book a call" card. Calls are initiated by the team after reviewing an inquiry. This is a deliberate process decision, not an omission.
- **Nav CTA button removed** — Removing the top-right button was a deliberate simplification. The nav Contact link + bottom CTA on every page is sufficient. Do not re-add a nav CTA without a clear reason.
- **Bottom CTA reduced to one button** — Three-button bottom CTA (Submit inquiry / Fill intake / Book call) replaced with a single "Contact Us" button. Contact page handles the routing. Do not revert to multi-button without revisiting the contact page design.

---

## Tab System — Unchanged from v0508A

No changes to tab rules. See v0508A for full spec.

---

## Design System — Unchanged from v0508A

`:root` CSS variables unchanged. See v0508A for full canonical `:root`.

**New pattern added this session — in-page red text link CTA:**
```css
color: var(--red);
font-weight: 600;
font-size: 15px;
text-decoration: none;
/* on hover: text-decoration: underline */
```
Use this anywhere a btn-red is not appropriate (mid-page, within content sections). Never use this style in the bottom CTA section — use `btn-red` there.

---

## `style.md` — Planned, Not Yet Created

A `style.md` file is planned for the repo root. It will serve as the canonical design system reference for Claude Code. Until it exists, Claude Code must fetch live files from GitHub to understand current patterns.

**Planned contents of `style.md`:**
- Canonical `:root` variables (copy from v0508A)
- Button classes: `btn-red`, `btn-outline`, `btn-dark`, `.on-dark` modifier, red text link CTA
- Nav HTML structure (shared across all pages)
- Footer HTML structure (shared across all pages)
- Bottom CTA section HTML pattern
- Tab system patterns (contact page, svc2, svc3)
- Section background rhythm rules
- Mobile breakpoints and responsive rules
- Page title format: `[Page Name] — Three Flows Solutions`
- Breadcrumb rules per page type
- Critical rules checklist (from v0508A Critical Rules section)

**Priority:** Create before next major page build or any Claude Code session that touches shared layout.

---

## Git Hygiene — Unchanged from v0508A

Standard commit patterns unchanged. New pattern added:

**For contact page or CTA-only changes:**
```
git add contact.html [other affected pages] && git commit -m "[description]" && git push
```

**Note on PR workflow:** Claude Code opens PRs via GitHub REST API using a repo-scoped token. Merging is always a manual step — Claude Code cannot merge. After merge, GitHub Pages redeploys in ~1–2 minutes. CDN propagation can take up to 10 minutes for new files (e.g. first deploy of `contact.html`).
