# Three Flows Solutions — STYLE.md
## Visual & UX Source of Truth
## Version 1.0 — May 10, 2026

---

## How to use this file

This is the single source of truth for all visual and UX decisions on the Three Flows Solutions website.

- **Before writing any code**, read this file in full.
- **Before adding any new page or section**, check the relevant section here first.
- **If a new pattern is introduced** that is not covered here, add it to the relevant section before committing.
- **If a pattern is retired or changed**, update this file in the same commit as the code change.

For operational rules (file structure, IDs, git hygiene, blog chain, tool registry), see `handoffs/threeflows_handoff_v0509A.md`.

---

## 1. Design Tokens

### CSS variables — canonical :root

Every page must include exactly this `:root` block. Do not hardcode hex values anywhere in the site.

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

### Typography

- **Headings:** DM Serif Display (Google Fonts)
- **Body:** DM Sans (Google Fonts)
- **Base font size:** 16px
- **Base line height:** 1.7
- **Section title (h2):** 36px — canonical. Do not use 38px.
- **Body paragraph style** — use class `.section-body`, never inline styles:

```css
.section-body {
  font-size: 16px;
  color: var(--mid);
  line-height: 1.75;
  font-weight: 300;
}
```

---

## 2. Global Chrome

### Navigation

Identical across all pages. No nav CTA button. Nav ends at the last nav link.

```
Logo → index.html
├── Home → index.html
├── Services ▾
│   ├── Business Planning → svc1.html
│   ├── Sourcing Consultation → svc2.html
│   ├── Launch Hypercare → svc3.html
│   └── Ongoing Management → svc4.html
├── Resources ▾
│   ├── Blogs & articles → blog.html
│   ├── Useful websites → useful-websites.html
│   ├── Checklists & calculators → free-tools.html
│   ├── Webinars & seminars → webinars.html
│   └── Livestream schedule → livestream.html
├── About → about.html
└── Contact → contact.html
```

Rules:
- Nav labels are sentence case — never Title Case or ALL CAPS
- Services dropdown items have NO number prefixes
- No CTA button in the nav — do not re-add without a clear reason
- Nav is never modified per page — always identical across all pages

### Footer

Identical across all pages. One footer per page.

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

## 3. Back / Breadcrumb Navigation

### Rules by page type

| Page type          | Breadcrumb        | Prev/Next cards |
|--------------------|-------------------|-----------------|
| Service (svc1–4)   | ❌ None            | None            |
| About              | ❌ None            | None            |
| index.html         | ❌ None            | None            |
| contact.html       | ❌ None            | None            |
| Tool (ck/ca pages) | ✅ ← Free Tools    | None            |
| Blog posts         | ✅ ← Blog          | ✅ Yes           |
| Resource pages     | ❌ None            | None            |

### Breadcrumb style

Applies identically to tool pages and blog posts — no variation.

```css
.breadcrumb-link {
  color: var(--muted);
  font-size: 14px;
  text-decoration: none;
}
```

- Text: `← [Parent page name]`
- Position: top-left, above page H1, outside any hero section

### Blog post prev/next cards

- Appear between breadcrumb and post meta row (publish date + tag pills)
- Previous card: left side, title left-aligned
- Next card: right side, title right-aligned
- When only one direction exists, that card occupies its natural side — never centered
- Card size: reduced from original — exact spec pending separate design discussion

---

## 4. CTA Buttons & Links

### Button classes

| Class | Label | Destination | Context |
|---|---|---|---|
| `btn-red on-dark` | Contact Us | `contact.html` | Bottom CTA section (dark bg) |
| `btn-red` | Access Tool → | JS gate reveal | Tool page gate only |
| `btn-red` | Submit an inquiry | `inquiry.html` | contact.html panel 1 |
| `btn-red` | Fill in intake form | `intake.html` | contact.html panel 2 |
| `btn-outline` | Send feedback | mailto | contact.html panel 3 |

Rules:
- `btn-red on-dark` when button sits on `var(--dark)` background — always
- `btn-red` (no modifier) for all other contexts
- `btn-dark` and `btn-outline` do NOT appear in bottom CTA sections — contact.html panels only
- Do not add a "Book a call" button to any page — calls are team-initiated after inquiry review

### In-page red text links

Use class `.cta-link` — never inline styles.

```css
.cta-link {
  color: var(--red);
  font-weight: 600;
  font-size: 15px;
  text-decoration: none;
}
.cta-link:hover {
  text-decoration: underline;
}
```

Use for: `Contact us →`, `Get it for free →`, `Submit an inquiry →`, `See full details →`, `Go →`, and all other in-page navigation text links.

### Arrow direction rules

| Arrow | Use case |
|---|---|
| `→` flat right | All internal links (same site) |
| `↗` upper-right | External links only — always opens in new tab |

Never mix these. `↗` signals "leaving the site." `→` signals "staying on the site."

### Bottom CTA section — standard pattern

All pages except `contact.html`. Single button, two-column layout.

```html
<section class="bottom-cta">
  <div class="bottom-inner">
    <div class="bottom-left">
      <h2>[Per-page headline]</h2>
      <p>[Per-page subtitle]</p>
    </div>
    <div class="bottom-right">
      <a href="contact.html" class="btn-red on-dark">Contact Us</a>
    </div>
  </div>
</section>
```

Layout: headline + subtitle left (70%), button right (30%).

Per-page headlines and subtitles:

| Page | Headline | Subtitle |
|---|---|---|
| index.html | "Ready to build your e-commerce business?" | "First conversation is always free. Choose how you'd like to connect." |
| svc1.html | "Ready to build your plan?" | "Start with a discovery call or send us your question — we'll take it from there." |
| svc2.html | "Ready to find the right supplier?" | same as svc1 |
| svc3.html | "Ready to launch with confidence?" | same as svc1 |
| svc4.html | "Ready for ongoing support?" | same as svc1 |
| about.html | "Want to work with us?" | verify live file |
| All other pages | verify live file | verify live file |

---

## 5. Page Section Patterns

### Background color rhythm

Primary separator mechanism is background color change. Never use `<hr>`.

Standard rhythm:

```
hero (white) → content (white or off-white) → dark accent → white → bottom-cta (dark)
```

Rules:
- Never run two consecutive `var(--dark)` sections
- Two consecutive white sections are acceptable only if they have distinct internal treatments (cards, borders)
- `var(--off-white)` (#F8F8F8) for subtle variation without full contrast shift
- `border-top: 1px solid var(--border)` for strips and partner bars — not as a primary section separator

### Section padding — canonical values

| Selector | Padding | Notes |
|---|---|---|
| `.section`, `.svc-section` | `64px 48px` | Standard — all content sections |
| Mobile override | `48px 20px` | Standard breakpoint |
| `.process-section`, `.team-section` (index only) | `80px 48px` | Home emphasis — do not apply elsewhere |
| `.partner-strip` | `16px 48px` | Strip pattern |

**72px is not a valid section padding value.** Do not introduce it.

### Section class naming

- `.section` — standard wrapper for all content sections
- `.svc-section` — only where page-specific CSS overrides are needed
- Do not create new section wrapper classes without documenting here

---

## 6. Component Patterns

### Eyebrow labels

One pattern only. Never create page-specific eyebrow classes.

```html
<div class="eyebrow muted">FAQ</div>       <!-- grey, for section labels -->
<div class="eyebrow red">PLAN</div>        <!-- red, for hero identifiers -->
<div class="eyebrow red">CONTACT US</div>  <!-- red, for contact hero -->
```

```css
.eyebrow {
  font-size: 11px;
  letter-spacing: 0.12em;
  margin-bottom: 12px;
  color: var(--muted);
  text-transform: uppercase;
}
.eyebrow.red   { color: var(--red); }
.eyebrow.muted { color: var(--muted); }
```

Rules:
- FAQ eyebrows: always `eyebrow muted`
- Hero service eyebrows (PLAN, SOURCE, LAUNCH, GROW): always `eyebrow red`
- Contact hero eyebrow: always `eyebrow red` — text "CONTACT US"
- Never create `.contact-eyebrow` or similar bespoke classes

### Hero section padding — service pages

All four service pages (svc1–4) must use identical `padding-top` on `.hero-wrap` or `.hero-inner`.
Canonical value: match svc2/3/4 — svc1 has a known extra ~40px gap above the eyebrow that must be corrected.

### FAQ sections

Appears on svc1–4 only.

```html
<div class="section">
  <div class="eyebrow muted">FAQ</div>
  <h2 class="section-title">Common questions</h2>
  <div class="faq-list">
    <div class="faq-item">
      <button class="faq-q" onclick="toggleFaq(this)">
        Question text <span class="faq-icon">+</span>
      </button>
      <div class="faq-a">Answer text</div>
    </div>
  </div>
</div>
```

Rules:
- Class names: `.faq-list`, `.faq-item`, `.faq-q`, `.faq-a`, `.faq-icon`, `.faq-item.open`
- JS: `function toggleFaq(el)` — single-open (clicking one closes others)
- Toggle: `+` rotates to `×` via `transform: rotate(45deg)` on `.faq-item.open .faq-icon`
- Always on white background
- Always wrapped in `.section` — never `.svc-section`
- Always uses `eyebrow muted` — never plain `eyebrow`

### Tab navigation (svc2, svc3)

```html
<div class="tab-strip">
  <div class="tab-inner">
    <button class="tab-btn active" onclick="setTab(0)">
      <span class="tab-btn-num">2A</span>
      <span class="tab-btn-title">Title</span>
      <span class="tab-btn-sub">Subtitle</span>
    </button>
  </div>
</div>
```

Rules:
- Class names: `.tab-strip`, `.tab-inner`, `.tab-btn`, `.tab-btn.active`
- svc2 JS: `setTab(idx)` · svc3 JS: `setSvc3Tab(idx)` — do not change naming
- Active indicator: `border-bottom: 2px solid var(--dark)`
- Tab content panels on white background

### Contact page step-strip

Separate namespace from svc tab strips — intentional.

Rules:
- Cards: `.contact-tab-card` / active: `.contact-tab-card.active`
- Panels: `.contact-panel`
- JS: `setContactTab(n)`
- Number circle: CSS-driven — outlined/muted default, red filled when `.active`
- Do not merge with the svc tab pattern

### Callout / highlight blocks

Five defined variants. Do not add new variants without documenting here.

| Class | Background | Border | Use case |
|---|---|---|---|
| `.callout` | white | red left border | Standard emphasis in blog posts |
| `.callout-grey` | `var(--off-white)` | dark left border | Secondary/quiet emphasis in blog posts |
| `.callout.green` | `var(--green-light)` | green left border | Positive outcome callout |
| `.callout.blue` | `var(--blue-light)` | blue left border | Informational / data callout |
| `.continuity-banner` | `var(--dark)` | none | Continuity discount — svc1–4 only |

Rules:
- Never use `style="background:#F8F8F8; border-left-color:#1A1A1A"` — always use `.callout-grey`
- Callout variants for blog posts only — not service or tool pages
- `.continuity-banner` for service pages only

### Resource and tool cards — CTA link alignment

All cards with variable-length descriptions must pin the CTA link to the bottom.

```css
.resource-card,
.tool-card {
  display: flex;
  flex-direction: column;
}
.resource-card .cta-link,
.tool-card .cta-link {
  margin-top: auto;
}
```

This ensures `Go →`, `Get it for free →` etc. always align to the card bottom.

### Tool page bottom section

```html
<div class="tool-cta-card">
  <p>Need a version built for your business?
    <a href="inquiry.html" class="cta-link">Submit an inquiry →</a>
  </p>
  <p>
    <a href="mailto:contact@threeflows.com?subject=Feedback&body=Page%20URL%3A%20%0ATool%20name%3A%20%0AFeedback%3A%20"
       class="bug-report-link">Report a bug or suggest an improvement →</a>
  </p>
</div>
```

Rules:
- Class: `.tool-cta-card` — white background, bordered card
- Never use `.bottom-cta` for this element — `.bottom-cta` is the dark sitewide bar only
- No buttons inside `.tool-cta-card` — plain text links only

---

## 7. Style Audit Process

Run after any significant batch of new pages, or monthly.

Steps:
1. Fetch live pages from the site
2. Cross-reference against this file
3. Produce discrepancy report (grouped by section, severity-flagged 🔴/🟡/✅)
4. Align on fixes
5. Add any new patterns to this file before closing the session
6. Remove or update retired patterns in the same commit

**Every Claude Code prompt must include:** "Before writing any code, read STYLE.md and the latest handoff doc from the repo root."

| Date | Version | Changes |
|---|---|---|
| May 10, 2026 | 1.0 | Initial release — Sessions A + C audit against handoff v0509A |

---

## 8. Known Tech Debt

Resolve as part of the planned shared stylesheet refactor. Do not action piecemeal.

- **Shared `styles.css`** — every page embeds full CSS inline. Extract after STYLE.md is stable.
- **Duplicate `:root` and shared rules** — each page redefines `:root`, `.btn-red`, `nav`, `footer` 2–3× internally.
- **`.section-title` declared multiple times per file** — first at 38px, last at 36px. Canonical is 36px. Consolidate on extraction.
- **Dead `.nav-cta` CSS rule** — exists in every page's `<style>` block. Remove during refactor.
- **svc4 72px padding** — `.philosophy-inner`, `.tower-inner` use non-standard 72px. Fix to 64px in next targeted pass.
- **Footer Privacy & Terms links** — all pages use `href="#"` placeholders. Replace before launch.
