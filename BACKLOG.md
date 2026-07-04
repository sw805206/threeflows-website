# Threeflows — Backlog

Single source of truth for the project's tracked work. CLAUDE.md points here for the full process detail.

## What this is

A **project-based tracker** for important-but-not-urgent items — process, feature, page, bug, or governance changes. This file is the **source of truth**. Every item is tagged with a **category** and a **status**. Closing an item **requires evidence**: the `PR##` if it was code, or a human description otherwise.

## Process

1. During chat, the user says **"log to backlog."**
2. Chat maintains a **running cumulative block**, reprinted in full every time it changes (the latest printing is always the complete, authoritative list). On request it is **flushed to BACKLOG.md** as a word-for-word copy, **verified by count** (N pending in = N rows out). Temporary IDs (P##) are scoped to the current unflushed batch only; after a flush, the pending block empties and P## recycle from P01. Permanent BL-### IDs carry the cumulative sequence.
3. A flush **writes to the working tree only** — never committed until the user says so.
4. **Tags / status / comments** are assigned at flush, or edited later via Code.
5. An **xlsx view** may be generated on demand from BACKLOG.md; edits made there return through Code.

## Categories

- **Governance types:** `claude` · `scope` · `architecture` · `style` · `process`
- **Change types:** `bug` · `feature` · `content` · `page`
- **Fallback:** `other`

## Status

`open → review → close` — plus `park` or `discard` at any time.

- **open** — active/pending work.
- **review** — Code believes it is done and needs human verification. **Code never self-closes** — it moves an item to `review`, never to `close`.
- **close** — **human-only.** The user ratifies, and the closed row must carry evidence in **Closed-by**: the `PR##` for code, or the user's stated reason otherwise.
- **park** — deferred, intentionally not being worked now.
- **discard** — dropped / moved out of this tracker's scope.

## Schema

`| ID | Status | Category | Item | Raised | Closed-by |`

- **ID** — `BL-001`, `BL-002`, … sequential, never reused.
- **Closed-by** — **empty** unless Status = `close`, then the `PR##` or the human reason.

---

## Items

| ID | Status | Category | Item | Raised | Closed-by |
|---|---|---|---|---|---|
| BL-001 | close | style | Design tokens — colours, typography (incl. dense/UI tier 13/12/11), spacing scale, border-radius scale — defined in STYLE.md | 2026-07-03 | PR#33 |
| BL-002 | close | style | Global chrome (nav/footer content + rules) defined in STYLE.md; mechanism (partials fetch) lives in ARCHITECTURE.md | 2026-07-03 | PR#33 |
| BL-003 | close | style | Section/layout patterns — background rhythm, section padding, wrapper naming, card background, hero padding | 2026-07-03 | PR#33 |
| BL-004 | close | style | Arrow-direction rule — `→` internal, `↗` external | 2026-07-03 | PR#33 |
| BL-005 | close | style | Components — all 12 drafted in STYLE.md: cards, callouts, eyebrows, tag pills, in-page links, buttons, bottom-cta, tool-cta-card, FAQ, tabs, stepper, form blocks | 2026-07-03 | PR#33 |
| BL-006 | close | style | Breadcrumb / prev-next component defined (prev/next card size still deferred — see BL-012) | 2026-07-03 | PR#33 |
| BL-007 | open | style | Verify-from-live: card grid column min-width (auto-fill, max 4 cols) — record value, remove flag | 2026-07-03 | |
| BL-008 | open | style | Verify-from-live: service hero `padding-top` — match svc2/3/4, then record | 2026-07-03 | |
| BL-009 | open | style | Verify-from-live: bottom-cta shared headline/subtitle max-width (longest 32px headline + longest 16px subtitle each on one line) | 2026-07-03 | |
| BL-010 | open | style | Verify-from-live: thank-you block treatment (no live sample in tool pages; contact/intake/survey carry it) | 2026-07-03 | |
| BL-011 | open | style | Verify-from-live: breadcrumb `.breadcrumb-wrap` max-width drift (780 on some tool pages, 1100 on others) — pick one | 2026-07-03 | |
| BL-012 | park | style | Prev/next card size — deferred pending a separate design decision | 2026-07-03 | |
| BL-013 | open | style | svc1 hero — remove the ~40px extra gap above the eyebrow (match svc2/3/4) | 2026-07-03 | |
| BL-014 | open | style | Live→token colour migrations: callout red #D63B3B→#C2291B; continuity pill #D63B3B→RN02; callout green text #174A17/#1A4A1A→#3B6D11; callout blue bg #EEF4FB→#E6F1FB (BB01); eyebrow red #D63B3B→#C2291B; cta-link red #D63B3B→#EF4444 and 15px→16px | 2026-07-03 | |
| BL-015 | open | style | Tag pill consolidation: collapse `.badge` (10.5px, radius 20) and `.resource-stage-badge` (10px, radius 20) into one canonical pill (11px, radius 999, pad 3×10) | 2026-07-03 | |
| BL-016 | open | style | Button cleanup: btn-red #D63B3B→RN01 #EF4444; standardize padding→12×24 (drift 13×28/12×26/11×24/10×20 + 9 inline on-dark); radius→6 (3 files drift to 8); remove `on-dark` class + 9 inline "Contact Us" overrides; remove dead `.nav-cta` CSS (51 pages); blog-007 chart toggles #D63B3B/#5C5C5C→per-post data-viz | 2026-07-03 | |
| BL-017 | park | style | btn-outline — finalize combo + border treatment when next encountered (currently 1.5px/1px border drift, radius 8) | 2026-07-03 | |
| BL-018 | open | style | Bottom-cta de-alias + snaps: collapse `.svc-bottom-cta`/`.svc-bottom-inner`→`.bottom-cta`/`.bottom-inner`; pad 60×48→64×48; headline 30→32; subtitle 14→16 + translucent-white #FFF/0.5–0.55→NN07 #909090; resolve conflicting `var(--white)` def | 2026-07-03 | |
| BL-019 | open | style | Tool-cta-card consolidation: 3 drifted forms (ca001/ref001 max-w 780/820, ck001 rich w/ h2+`.cta-actions`)→one simple card (max-w 800, pad 24×24); body 14→16; drop ck001 h2+button row; remap retired `--red-dark` #B82E2E→#EF4444/muted | 2026-07-03 | |
| BL-020 | open | style | Form blocks remaps: red #D63B3B→#EF4444 (focus/`.req`/error); error `--red-dark`→#EF4444; input radius 8→6; input pad 11×14→12×16; container radius 12→10, pad 28×26→24×24; gate heading 22px serif→h3 20px sans | 2026-07-03 | |
| BL-021 | open | style | Retire `.section-body` utility — body copy uses the ramp (16px DM Sans, #5C5C5C/NN03); confirm and remove the standalone class | 2026-07-03 | |
| BL-022 | open | style | FAQ redesign (design change, not a remap): svc1–4 boxed-card FAQ→compact hairline-row accordion (drop per-item box; question 18→16; row pad 20×24→12 vertical; #E8E8E8 dividers) | 2026-07-03 | |
| BL-023 | open | style | Tabs consolidation (Family A, underline text-tabs): collapse svc2 `setTab`, svc3 `setSvc3Tab`, useful-websites `uwShowTab`→one component (`.tab-strip`/`setTab`); standardize panel mechanism to `.active`; snap pad 20×16/16×20→12×24 | 2026-07-03 | |
| BL-024 | open | style | Stepper consolidation (Family B, numbered steps): collapse contact `setContactTab` + index `setFlow`→one component; canonical circle badge (drop contact square); badge red #D63B3B→RN01 #EF4444; pad 20×18/28×24→24×24; reconcile 0- vs 1-based indexing | 2026-07-03 | |
| BL-025 | open | style | Page-by-page sweep — callout leftovers: `.info-banner`, `.sourcing-banner`, svc2 inline replica→fold into Content/Remark callout; green/blue callout content→remap per post; `.highlight-row`, `.review-banner`, `.process-highlight`→handle as own non-callout patterns | 2026-07-03 | |
| BL-026 | open | style | Page-by-page sweep — inventory + define remaining card types (index, svc1–4, about); decide whether a shared card base is warranted after inventory | 2026-07-03 | |
| BL-027 | open | style | Per-page background-rhythm conformance — applied during the STYLE.css migration, not retrofitted page-by-page before then | 2026-07-03 | |
| BL-028 | open | architecture | partials.html (shared nav/footer) — fixes: About link missing on blog pages (stale nav), no nav on surveys/svy001/inquiry/intake/mtl001, no mobile nav sitewide. NOTE: Pilot merged (PR#36) and verified live on index/svc1/blog-003 — sticky nav, dropdowns, footer, blog-003 stale-nav fix all confirmed on live domain. The 47-page sweep remains the open work. | 2026-07-03 | |
| BL-029 | open | architecture | `.nojekyll` file — disable the unused Jekyll build path; reversible (delete to re-enable) | 2026-07-03 | |
| BL-030 | open | architecture | Free-tools tabbing (checklists/calculators) — structural; intersects "retire per-type tool templates" (BL-031) | 2026-07-03 | |
| BL-031 | open | architecture | Retire per-type tool templates (`tool-ca000`/`tool-ck000`)→shared blocks; live tool pages migrate to shared-blocks/partials model | 2026-07-03 | |
| BL-032 | open | architecture | intake.html form shell — 174 inputs, 0 `<form>` tags, JS submit to endpoint; fragile, inconsistent with the other 3 flows | 2026-07-03 | |
| BL-033 | park | architecture | Contact page redesign — deferred until after STYLE.css; promote Contact Us, consolidate inquiry+feedback | 2026-07-03 | |
| BL-034 | open | architecture | Shared stylesheet (STYLE.css) — the migration itself: extract inline CSS sitewide into token-based STYLE.css | 2026-07-03 | |
| BL-035 | open | content | SEO / metadata — not yet implemented | 2026-07-03 | |
| BL-036 | open | content | Footer Privacy / Terms links — currently `href="#"` placeholders; replace before launch | 2026-07-03 | |
| BL-037 | open | content | Terms & conditions / privacy pages — "add hidden page?"; confirm approach | 2026-07-03 | |
| BL-038 | open | content | Survey 1 activation / deactivation — only one survey active at a time | 2026-07-03 | |
| BL-039 | open | content | Paywall (livestream) — not built | 2026-07-03 | |
| BL-040 | open | content | Livestream calendar — placeholder / coming soon | 2026-07-03 | |
| BL-041 | open | process | Component-add process — write the rule parallel to the palette's "add the combo here first, then implement in STYLE.css"; placement (Google Doc vs STYLE.md note) to be decided | 2026-07-03 | |
| BL-042 | open | process | Repo branch reconciliation — earlier audits flagged STYLE.md/oldSTYLE.md removed on a working branch, CLAUDE.md modified, ARCHITECTURE.md untracked. Revisit: parts likely resolved by PR#33 + current governance commits — reconfirm authoritative state | 2026-07-03 | |
| BL-043 | discard | process | Style Audit process — moved off STYLE.md to a Google Doc per an earlier decision (out of this tracker's scope) | 2026-07-03 | |
| BL-044 | discard | process | Handoffs — documented in a Google Doc, not the repo (off the table for this tracker) | 2026-07-03 | |
| BL-045 | open | page | "Orphaned blog pages" — term never defined; clarify what it refers to before any disposition | 2026-07-03 | |
| BL-046 | open | other | Accessibility (WCAG 2.1 AA) — palette-contrast angle is style-relevant (AA on combos); broader a11y tracked separately; decide its home | 2026-07-03 | |
| BL-047 | close | architecture | Lean-deps / data-viz exception — d3/Chart.js/topojson on 3 blog pages accepted by exception, not a framework violation | 2026-07-03 | Human-confirmed: accepted data-viz exception, not a framework violation |
| BL-048 | close | claude | Update CLAUDE.md with two rules: (a) "When a decision is pending user input, stop at the recommendation and wait — do not draft the runnable prompt until user explicitly says go, even if discussion seems complete"; and (b) adopt the backlog process — Part A (Chat maintains running block, reprints in full, flushes on request) + Part B (flush/tag/status/close mechanics, PR## evidence, Code never self-closes). [Note: implemented via commit 4b7dea2 on branch docs/claude-md-backlog, PR pending — leave OPEN until that PR merges, then close with its PR##.] | 2026-07-04 | PR#34 |
| BL-049 | open | style | Type-ramp 13↔16 gap: live uses 14px (nav links, logo-name) and 15px (retired cta-link) to fill it. Decide as a PATTERN (add a governed ramp step, or snap) during a dedicated size-drift audit — not piecemeal. | 2026-07-04 | |
| BL-050 | open | process | Establish a periodic style-drift audit as a standing governance item — the venue to settle the 13↔16 gap and similar off-ramp values across the whole site at once, from complete evidence. | 2026-07-04 | |
| BL-051 | open | style | Dead .nav-cta / .logo-icon CSS: full ~50-page removal deferred to the STYLE.css sweep. (partials pilot only clears it on the 3 pilot pages.) | 2026-07-04 | |
| BL-052 | open | style | Partials.html self-contained inline style slice (nav/footer/hamburger) → lift into STYLE.css during the migration, then delete from partials. | 2026-07-04 | |
| BL-053 | open | page | Blog body-structure divergence: blog-002 through blog-005 carry an extra `<article class="post" id="postNNN">` wrapper that blog-000-template.html and the other 21 posts lack (meta row nested one level deeper). Normalize these 4 posts against the template — sequence AFTER partials + STYLE.css. Other 21 posts already match template. | 2026-07-04 | |
| BL-054 | open | process | Sweep retrofit must guard line endings: the pilot's CSS-strip script silently converted CRLF→LF on index.html/svc1.html, causing ~2,400 lines of false diff churn (caught and corrected in pilot). The 50-page sweep must preserve original line endings per file. | 2026-07-04 | |
| BL-055 | open | claude | Add post-merge cleanup to CLAUDE.md Part B as a standard step: after a PR merges, run `git checkout main && git pull origin main && git branch -d <branch> && git remote prune origin` (sync main, delete local branch, prune stale remote refs). Make it part of the branch-discipline flow so it's automatic, not manually remembered. | 2026-07-04 | |
