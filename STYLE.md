# Style

*Target-state. Refer to STYLE.md and STYLE.css for specific values. All sections drafted; values are decided unless explicitly marked verify-from-live or deferred. STYLE.css implements these tokens (not yet built — see backlog).*

This document is the single source of truth for visual and UX decisions. STYLE.css (not yet built) implements these tokens; every page draws from it rather than defining styles inline. For structure and page mechanics, see ARCHITECTURE.md. For scope, see SCOPE.md.

---

## Assets

- Logo and images live in the asset folder (`assets/images/`).
- Logo: `logo_claude.svg` — a red rounded square with three white bars. The logo red is **#C2291B** (the brand anchor — see Colors).

---

## Design Tokens

### Color palette

This section is the **source of truth for colors**. Raw colors are identified by hex. Combos (background + text pairs) are identified by a 2-letter + 2-digit ID: the first letter is the background family, the second is the text family (R red, N neutral, G green, B blue, A amber; white and black fold into N), and the 2-digit serial runs per letter-pair. STYLE.css implements these as variables; a visual HTML view can be generated from this section on demand (via a Code prompt). **Governance: to add a new combo, add it here first, then implement it in STYLE.css.** Text weight/style (bold, italic) is typography — out of scope for the palette.

**Raw colors** (hex is the identifier), grouped by family:

- Reds: #C2291B (brand red), #EF4444 (interactive red), #FDF0F0 (red wash)
- Neutrals: #1A1A1A (black), #3A3A3A (charcoal), #5C5C5C (mid grey), #909090 (muted grey), #C8C8C8 (light grey), #E8E8E8 (border grey), #F8F8F8 (off-white), #FFFFFF (white)
- Ambers: #FACC15 (amber), #FEF3C7 (amber wash), #854F0B (amber text)
- Greens: #00B050 (green), #EAF3DE (green wash), #3B6D11 (green text)
- Blues: #185FA5 (blue), #E6F1FB (blue wash)

*Retired (do not reintroduce): #B82E2E (dark red — redundant with brand red), #534AB7 purple, pink #FDE8F0/#B5256A. Blog data-viz chart colors are per-chart, not part of the palette.*

*Accessibility (WCAG AA contrast, 4.5:1 for normal text): most combos pass comfortably. Three fall below AA for normal text and are large-text-only (3:1): **NN04** muted #909090 on white (3.19), **NR01** interactive-red #EF4444 link on white (3.76), and **RN01** button white-on-#EF4444 (3.76). Use these for large/bold text only, or darken toward #767676 (muted) / #C2291B (red, which passes at 5.79) if normal-text AA is required. New combos intended for body text should be checked against 4.5:1 before adding.*

**Combos with meaning** — tag pills, all wash, context-scoped (the same combo means different things on different page types; contexts don't co-occur, so no ambiguity):

| ID | bg / text | Context | Meaning |
|---|---|---|---|
| RR01 | #FDF0F0 / #C2291B | Blogs · Insights · Status | primary · startup · failure |
| NN01 | #E8E8E8 / #3A3A3A | Blogs · Insights | secondary · established |
| GG01 | #EAF3DE / #3B6D11 | Marketplaces · Status | open · success/eco |
| BB01 | #E6F1FB / #185FA5 | Marketplaces · Status | curated · to-start |
| AA01 | #FEF3C7 / #854F0B | Marketplaces · Status | vendor · at-risk |

**Combos commonly used** — text on backgrounds, buttons, links:

| ID | bg / text | Use |
|---|---|---|
| NN02 | #FFFFFF / #1A1A1A | primary text on white |
| NN03 | #FFFFFF / #5C5C5C | secondary text on white |
| NN04 | #FFFFFF / #909090 | muted / caption on white |
| NN05 | #F8F8F8 / #1A1A1A | primary text on off-white |
| NN06 | #1A1A1A / #F8F8F8 | light text on dark section |
| NN07 | #1A1A1A / #909090 | muted text on dark |
| NR01 | #FFFFFF / #EF4444 | interactive link on white |
| RN01 | #EF4444 / #FFFFFF | primary button |
| NR02 | #1A1A1A / #EF4444 | button / link on dark |

**Combos viable but unassigned** — legible, on-brand, kept in reserve (no meaning/use yet):

| ID | bg / text | Note |
|---|---|---|
| RN02 | #C2291B / #FFFFFF | brand-red solid fill |
| GN01 | #00B050 / #FFFFFF | loud green fill |
| BN01 | #185FA5 / #FFFFFF | loud blue fill |
| AN01 | #FACC15 / #1A1A1A | amber fill, dark text |
| NN08 | #909090 / #FFFFFF | disabled / inactive |

### Typography

- **Fonts:** DM Serif Display (h1, h2), DM Sans (h3, body, UI). Google Fonts.
- **Type ramp:**
  - h1 / hero — DM Serif Display, 44px
  - h2 / section title — DM Serif Display, 32px
  - h3 / subhead — DM Sans, 20px, weight 700
  - body — DM Sans, 16px, light (300)
- **Dense / UI tier** — DM Sans, for compact directory-style UI (cards, badges, in-card links) where the body ramp is too large. Governed sizes, not ad-hoc: **13px** (dense title / card name), **12px** (dense body / card description), **11px** (dense meta / in-card link). Do not introduce dense sizes outside this tier.
- **Body paragraphs:** the standard content paragraph is just the body ramp — 16px DM Sans, colour #5C5C5C (mid, NN03), weight 300. The old `.section-body` utility class is retired; body copy uses the ramp, not a bespoke class.
- **Line-height:** body 1.6 · headings 1.2 · dense/UI 1.3–1.45 · tight (buttons, badges, pills) 1.1

### Spacing scale

Steps (px): **4 / 8 / 12 / 16 / 24 / 32 / 48 / 64**. Every margin, gap, and padding snaps to a step.
- Section padding — 64×48 (desktop), 48×20 (mobile).
- Between-block spacing (card grids) — 16 or 24.
- Tag / pill row gaps — 8.
- Internal padding — per component (see Components): e.g. callouts 16×20, buttons 13×28, tag pills 3×10.
- **Governed exception:** card internal padding is **12×14** (the 14 is off-scale, kept deliberately for the dense card — see Components → Cards).

### Border-radius

- 6 — buttons, chips
- 10 — cards
- 20 — large cards, callouts
- 999 — pills (fully round)
- 50% — circles, avatars

(Retires the old `--radius` 12px token and the redundant `--border-radius-md`.)

---

## Global chrome (nav + footer)

Nav/footer **content and rules** live here; the **mechanism** (fetched from partials.html per page) is in ARCHITECTURE.md — do not re-describe it here.
- Link tree, sentence-case labels, no CTA button in nav, no number prefixes on Services items.
- Mobile: nav collapses to a hamburger menu.
- Footer: logo + copyright + Privacy/Terms links (currently placeholders — see backlog).

---

## Components

*All components drafted below: Cards, Callouts, Eyebrows, Tag pills, In-page links, Buttons, Bottom-CTA, Tool-CTA-card, FAQ, Tabs, Stepper, Form blocks.*

### Cards

**Scope:** this entry covers the directory-style **resource/tool card** only (the dense card used on useful-websites and free-tools). Other card types — client / case-study cards, stat cards, service-stage cards, principal / bio cards on index, svc1–4, and about — are distinct components, defined separately (see backlog).

Resource-card and tool-card are **one spec**, differing only in content, not styling.

- **Fill / placement:** white (#FFFFFF) fill, sitting on an off-white (#F8F8F8) section (per Section/layout → Card background). Border 1px #E8E8E8; radius 10.
- **Type (dense/UI tier):** name 13px / description 12px / in-card link 11px. Font DM Sans throughout (no serif on cards).
- **Padding:** 12×14 (governed exception — see Spacing scale). Internal gap 4.
- **Logo slot:** 16px, top-left before the name. Resource cards use each site's favicon; tool cards use the Threeflows logo (`logo_claude.svg`); the specific logo per tool is content, defined per tool.
- **Grid:** responsive auto-fill, **maximum 4 columns**, collapsing to 1 per row on mobile. Column count adjusts to page width up to the 4-column cap. (Min-width per column — verify-from-live.)
- **Height:** equal height across all cards on a page, derived from content (never a hardcoded value). Pages with longer content have taller cards than other pages; within a page, all cards match.
- **Bottom row:** in-card link (left) and tag pill(s) (right) pinned to the card bottom (`margin-top:auto` on a flex column) and horizontally aligned to each other.
- **Tag pills:** colours come from the Color palette combos (e.g. startup → RR01, established → NN01, open → GG01, curated → BB01, vendor → AA01). Not redefined here; the card cites the palette.
- **Arrows:** resource-card links are external (`↗`); tool-card links are internal (`→`) — see Arrow direction rule.

### Callouts

Three callouts, by function. All cite palette combos; no new colours. The two in-prose callouts share one anatomy: **attention text colour + a matching-colour left rim (3px) + tinted box** (radius 0 8px 8px 0, padding 16×20). The continuity callout is a different shape (dark band + pill), kept in this family by function, not form.

| Callout | Function | Style | Palette |
|---|---|---|---|
| **Continuity** | service / price-related | dark full-width band + pill badge; no rim; flex layout | band **NN06** (#1A1A1A) + pill **RN02** |
| **Content** | reminder, draw attention | red left-rim tinted box, in prose | **RR01** (#FDF0F0 / #C2291B rim) |
| **Remark** | additional comment / aside | grey left-rim tinted box, in prose | **NN05** (#F8F8F8) + neutral-dark rim, mid-grey text |

- Content and Remark: in-prose emphasis boxes; geometry as above.
- Continuity: standalone band (service pages), pill badge + light body text on the dark band.
- **All other prior highlight styles are removed** — green callout, blue callout, `.info-banner`, `.sourcing-banner`, the svc2 inline replica, and the non-callout highlights (`.highlight-row`, `.review-banner`, `.process-highlight`) are not part of this system. They are resolved in the page-by-page sweep: folded into one of the three above, or run through the component process if genuinely a new pattern (see backlog).

### Eyebrows

A small uppercase label above a section title or hero identifier. One pattern only — never page-specific eyebrow classes.

- **Type:** 11px (eyebrow's own governed size), weight 600, uppercase, letter-spacing 0.12em, margin-bottom 12px. DM Sans.
- **Variants:** muted (default) — colour #909090 (muted grey); red — colour **brand red #C2291B** (RR01 family; a label accent, not interactive). Never any other eyebrow colour.
- **Usage:** section labels (e.g. FAQ) use muted; hero identifiers (e.g. PLAN, SOURCE, CONTACT US) use red.

### Tag pills

A styled pill carrying a short status/category label. **Same height, content-driven width:** height is fixed (font-size + vertical padding + line-height, all constant); width flexes to the label text, with `white-space: nowrap`. So "startup" is narrower than "established"; all pills on a row share one height.

- **Shape:** radius 999 (fully round), padding 3×10, gap 8 between pills in a row, line-height 1.1 (tight). Font DM Sans, 11px (dense/UI tier), weight 600.
- **Colour:** from the Color palette combos only (RR01 / NN01 / GG01 / BB01 / AA01, meaning by context). The pill component defines shape; the palette defines colour. Not redefined here.
- **One canonical pill.** The historical `.badge` and `.resource-stage-badge` variants (differing font-size and radius) collapse into this single pill — see backlog for the live migration.

### In-page links (cta-link)

Inline red text links inside body content (e.g. `Contact us →`, `Get it for free →`, `See full details →`, `Go →`). Never inline styles — use the class.

- **Type / colour:** 16px (body ramp — snapped from the old off-scale 15px), weight 600, colour **interactive red #EF4444** (NR01 — these are interactive). Hover: underline.
- **Arrows:** internal links use `→`; external links use `↗` — see Arrow direction rule.

### Buttons

Filled action buttons. All buttons: padding **12×24**, radius **6**, DM Sans. (The live padding zoo — 13×28, 12×26, 11×24, 10×20 — collapses to 12×24; see backlog.)

- **btn-red** (primary) — **RN01** (#EF4444 / #FFFFFF). The ubiquitous button; used for all primary actions sitewide, including on dark bottom-CTA bands. Migrated from live #D63B3B (see backlog).
- **btn-dark** — #1A1A1A / #FFFFFF (NN06 family). Kept as-is; **index-only** ("See how we work →", "See full details →"). Not folded into btn-red — these stay dark by design.
- **btn-outline** (secondary) — **deferred.** In use on contact, forms (inquiry/intake), and tool pages, but its colour combo and border treatment are not yet finalized; to be settled when next encountered, via the component process (may involve adding a button combo to the palette). Do not rely on its current 1.5px-border rendering as canonical.

Rules:
- **No `on-dark` modifier.** btn-red is self-consistent on any background; the old `on-dark` class and its per-instance inline overrides are removed (see backlog). A red button on a dark band is just btn-red.
- **No CTA button in the nav** (the `.nav-cta` rule is dead CSS — remove; see backlog).
- **No "Book a call" button** on any page — calls are team-initiated after inquiry review.
- **Deferred elsewhere:** the multi-step form-wizard buttons (primary / secondary / next / back / restart / submit on inquiry, intake, blog-001) belong to the **form blocks** component, not here. The blog-007 chart-toggle buttons are a per-post data-viz exception, not a site button.

### Bottom-CTA

A standing dark band at the foot of every page except contact. Headline + subtitle on the left, a single btn-red on the right. Sits outside the background-rhythm system (see Section/layout).

- **Band:** **NN06** (#1A1A1A). Inner wrapper max-width 1100, padding **64×48** (snapped from live 60×48), flex space-between, gap 40, wraps on narrow; mobile 48×20, stacked.
- **Headline:** h2 ramp — DM Serif Display, **32px** (snapped from live 30px), white, line-height 1.25.
- **Subtitle:** **16px** (snapped from live 14px), colour **NN07** muted-on-dark #909090 (replaces the live translucent-white #FFF/0.5–0.55 — tokenized, not opacity).
- **Shared text width:** headline and subtitle share **one** max-width, sized so the longest headline (32px serif) and the longest subtitle (16px) each stay on one line. Exact px — **verify-from-live** (the current 460px on the headline, with no cap on the subtitle, wraps them at different widths — that mismatch is the bug being fixed).
- **Button:** one btn-red (primary, RN01). No `on-dark` modifier — it's a plain btn-red on the dark band.
- **De-alias:** `.svc-bottom-cta` / `.svc-bottom-inner` (useful-websites) and `.bottom-cta` / `.bottom-inner` (free-tools) are the same component under two names — collapse to one (`.bottom-cta`); see backlog.

### Tool-CTA-card

A white bordered card at the foot of tool pages: "need a version built for your business?" with an inquiry link and a bug-report link. **Not** the bottom-CTA (that dark band is sitewide; this is a quiet in-page card). No filled buttons inside — plain text links only.

- **Card:** white (#FFFFFF), border 1px #E8E8E8, radius 10, padding **24×24** (snapped from live 24×26 / 28×26), max-width **800** (from live 780 / 820), centred.
- **Body text:** **16px** (snapped from live 14px), colour #5C5C5C (mid).
- **Links:** inquiry → cta-link (16px, #EF4444 — see In-page links); bug-report → 12px muted #909090, `→` arrow. The live `--red-dark` #B82E2E on these links is a retired colour — remapped (see backlog).
- **One canonical form.** The elaborate tool-ck001 variant (adds an h2 heading + a `.cta-actions` button row) is dropped in favour of this simple form (matches oldSTYLE's "plain links, no buttons" intent and the majority live usage) — see backlog.
- **Templates:** per-type tool templates (`tool-ca000` / `tool-ck000`) are being retired (see ARCHITECTURE.md → Tools). Tool-cta-card is one shared component, not a per-template style — nothing template-specific is defined here.

### FAQ

A single-open accordion of questions, on service pages (svc1–4). **New compact design** — replaces the previous boxed-card FAQ (larger, bordered cards), which took too much vertical space; the old version migrates during the sweep (see backlog).

- **Container:** wrapped in `.section`, white background. Eyebrow muted "FAQ" + h2 "Common questions" (32px serif, ramp).
- **Rows, not cards:** each question is a row separated by a 1px hairline divider (#E8E8E8) — no per-item box, border, or fill. This is the space saving: the box chrome is removed.
- **Question:** 16px (body ramp), weight 600, DM Sans; `+` icon at the right.
- **Answer:** 16px, colour #5C5C5C (mid), revealed below the question on open.
- **Row padding:** 12px top/bottom (compact).
- **Behaviour:** single-open accordion — opening one closes the others. Icon `+` rotates 45° to `×` on the open row. Vanilla JS (`toggleFaq`), per the no-framework constraint.
- **Scope:** service pages (svc1–4) only.

### Tabs (underline text-tabs)

Horizontal tab bar that swaps content panels. Active tab marked by an underline — no fill, no badge. **One component** covering what were three separate implementations (svc2 `setTab`, svc3 `setSvc3Tab`, useful-websites `uwShowTab`); consolidated (see backlog).

- **Bar:** horizontal row of tab buttons over a 1px bottom border (#E8E8E8); scrolls horizontally on overflow. May be sticky under the nav (as on useful-websites) or static.
- **Button:** padding **12×24**, DM Sans. Idle: mid-grey #5C5C5C, weight 500. Active: dark #1A1A1A, weight 600, with a **2px dark (#1A1A1A) bottom-border** underline. No radius (flat tabs).
- **svc variant:** the button may carry a small num + title + sub label (e.g. "2A" / title / subtitle) — same bar, richer button content.
- **Mechanism:** panels toggled via an `.active` class (standardized — the useful-websites inline `style.display` version is retired). Vanilla JS, one function (survivor name `setTab`).
- **Panel:** revealed on white; only the active panel shown.

### Stepper (numbered steps)

A numbered step selector that reveals one panel at a time. Active step is a filled-dark card with a red circle badge. **One component** covering contact (`setContactTab`) and index "How we work" (`setFlow`) — the same structural pattern (see backlog). Distinct from Tabs (that's the other family: underline text-tabs, no fill/badge); the two families do not merge.

- **Step card:** padding **24×24**, radius 10. Idle: white (#FFFFFF), 1px border #E8E8E8. Active: filled dark **NN06** (#1A1A1A), white text.
- **Badge:** a **circle** (50% radius) numbered badge (canonical — the index style; the contact square badge is dropped). Idle: white with 1px border, dark text. Active: **RN01** (#EF4444) fill, white text.
- **Labels:** step title + sub-label; sub-label muted (#909090 idle / translucent-white on the active dark card).
- **Mechanism:** panels toggled via an `.active` class; only the selected step's panel is visible. Vanilla JS.
- **Layout:** steps may lay out horizontally (index, 4-across) or vertically (contact step cards) — layout varies by page; the component styling stays constant.
- **Note:** contact is slated for a redesign (see ARCHITECTURE.md), so the stepper there may change or not apply; the index "How we work" is the canonical reference.

### Form blocks

A set of reusable blocks that compose the site's forms and gates (see ARCHITECTURE.md → Form-ish for which pages use which). Two shapes: **form** (collect → submit → thank-you; the submission is the goal) and **gate** (capture email → unlock content; the email is a threshold). Both draw from the same field/label/button styling below.

**Container (gate / form card):** white (#FFFFFF), 1px border #E8E8E8, radius 10, padding 24×24. Heading: h3 (DM Sans 20px, weight 700) — a card heading, not a section title. Sub-text: 13px (dense/UI), colour #5C5C5C.

**Fields / labels:**
- **Label:** 12px, weight 500, colour #5C5C5C (mid); required marker `.req` asterisk in interactive red #EF4444. Margin-bottom 6.
- **Input** (text / email): DM Sans 14px, colour #1A1A1A, white bg, 1.5px border #border-dark, radius 6, padding 12×16, full width. **Focus:** border → #EF4444 + 3px red glow (rgba of #EF4444). Field margin-bottom 16.
- **Consent row:** checkbox + 13px text (#5C5C5C), aligned flex-start.
- **Error:** 13px, interactive red #EF4444 text on red-wash (#FDF0F0) bg, radius 6, padding 9×12; hidden until shown. (Live uses retired `--red-dark` — remapped; see backlog.)

**Buttons:** the form-wizard buttons (next / submit → **btn-red**, primary RN01; back → secondary; restart → text link) inherit the Buttons component — no separate button styling here.

**Thank-you block:** post-submit confirmation (form shape, and gate where applicable). Centred confirmation heading (h3 20px) + body (16px), on white or within the same card. Exact treatment — **verify-from-live** (no current sample in the tool pages; contact/intake/survey carry it).

**Migration:** live gate/field values use old red #D63B3B (focus, req, error via `--red-dark`), input radius 8, padding 11×14 / 28×26 — all remapped to the above; see backlog.

## Arrow direction rule

A link-behaviour convention (not a styled object): the arrow glyph signals whether a link keeps you on the site or takes you off it.

- **`→`** (flat right) — internal links, same-site navigation. Staying on the site.
- **`↗`** (upper-right) — external links only. Leaving the site; always opens in a new tab.

Never mix them. Applies everywhere links carry an arrow — cards, in-page links (cta-link), buttons with arrow labels.

## Breadcrumb / prev-next

**Breadcrumb** — a back-link above the page H1, outside any hero. Text `← [Parent page name]`. Style: 13px, DM Sans, colour muted #909090; hover → dark #1A1A1A; inline-flex, gap 6, no underline. Applies identically to the page types that use it — no per-page variation.

**Page-type rules** (which pages get a breadcrumb / prev-next):

| Page type | Breadcrumb | Prev/next |
|---|---|---|
| Service (svc1–4), About, index, contact | none | none |
| Tool pages (ck/ca/ref) | ✅ `← Free Tools` | none |
| Blog posts | ✅ `← Blog` | ✅ yes |
| Resource pages | none | none |

**Prev/next (blog posts only)** — previous/next post cards between the breadcrumb and the post meta row. Previous card left (title left-aligned); next card right (title right-aligned). When only one direction exists, that card holds its natural side — never centred. **Card size / exact styling — deferred** (pending a separate design decision; see backlog).

## Section / layout patterns

**Background rhythm.** The primary separator between sections is a background-color change — never `<hr>`. The default is white ↔ off-white (#F8F8F8) alternation for rhythm. Two things are exceptions, used deliberately:
- **Dark sections** (#1A1A1A) — exception, by design, for intentional highlight content (e.g. a featured case study). Never two dark sections in a row.
- **Consecutive white sections** — a true exception requiring case-by-case manual approval. Not a standard option and not self-justified by adding a card or border; the default is to break a white run with off-white.

Off-white (#F8F8F8) is the standard tool for gentle variation. A 1px border (#E8E8E8) suits strips and partner bars — not as a primary section separator.

Note: the bottom-CTA (a standing dark component at the foot of the page — see Components) sits outside this rhythm system and is not counted as a rhythm section.

*Per-page conformance to this rhythm is a backlog item, applied during the STYLE.css migration — not retrofitted page by page before then.*

**Section padding.** Two desktop steps, both on the spacing scale: standard `64px 48px` and emphasis `80px 48px` (for feature sections). Mobile: `48px 20px`. 72px is a one-off (a few page-specific inner wrappers), not a standard — do not treat it as canonical.

**Section-wrapper naming.** `.section` is the standard wrapper for content sections; `.svc-section` is used where page-specific overrides are needed (the name is historical — it applies beyond service pages; kept as-is to avoid a risky rename across all pages). Do not create new section-wrapper classes without documenting them here.

**Card background.** Cards use a white (#FFFFFF) fill regardless of the section background they sit on — so a card reads consistently on a white, off-white, or dark section. Both resource-card and tool-card share this white fill (they differ in size/content, not background).

**Hero padding (service pages).** All four service pages (svc1–4) use identical hero `padding-top`. Service-scoped — not a sitewide rule. Canonical value: verify-from-live (match svc2/3/4, then record here). The svc1 hero has a known ~40px extra gap above the eyebrow — see backlog.

---

## Style backlog / tech debt

Backlog tracked in BACKLOG.md.

---

## Governance TODO (post-STYLE.md)

- Write the **component-add process** — parallel to the palette's "add the combo here first, then implement in STYLE.css" rule. Likely: define in Components → cite existing palette IDs or add a new combo via the palette process → implement in STYLE.css → commit style-only. This is what the page-by-page sweep follows for any leftover that turns out to be a genuine new pattern. (Placement — Google Doc or a STYLE.md governance note — to be decided.)
