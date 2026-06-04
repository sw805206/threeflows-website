# Three Flows Solutions — Website Reference & Handoff
## Version 0603 — Updated June 3, 2026

---

## How to use this file

This file covers **operational rules only** — file structure, page inventory, component IDs, git workflow, and content decisions.

**For all visual and UX rules, see `STYLE.md` in the repo root.** Do not add style-related content here.

This is the latest handoff and the operational source of truth. It supersedes `threeflows_handoff_v0529.md`.

---

## What Changed Since v0529

### Session June 3, 2026

Calculator tool naming was consolidated, and `TOOL_REGISTRY.md` was brought back in sync with reality.

#### Calculator series consolidated: UE → CA

v0529 briefly introduced a `UE` ("unit economics") prefix for the calculator tools. That has been **retired and consolidated under the `CA` ("Calculator") series** — the prefix already used by the calculator master template (`tool-ca000-template.html`) and the `TOOL_REGISTRY.md` ID convention.

**Renames (June 3, 2026):**
| Former | New |
|---|---|
| `tool-ue001.html` | `tool-ca001.html` |
| `tool-ue002.html` | `tool-ca002.html` |
| ID `UE001` | ID `CA001` |
| ID `UE002` | ID `CA002` |

IDs are numbered **sequentially per series** — the two shipped calculators take `CA001` and `CA002` regardless of any earlier sketched roadmap. (The old "pre-assigned" CA list — Landed Cost, Storage Fee, etc. — was never built and is not reserved; it now lives as a non-binding backlog note in `TOOL_REGISTRY.md`.)

**Cookie name change side effect:** the gate cookie key changed from `tf_tool_ue001` / `tf_tool_ue002` to `tf_tool_ca001` / `tf_tool_ca002`. Visitors who previously unlocked a tool will see the email gate once more. This is expected and acceptable.

#### Files touched
- `tool-ue001.html` → `tool-ca001.html` (renamed; internal `TOOL_ID` and cookie comments updated `ue001` → `ca001`)
- `tool-ue002.html` → `tool-ca002.html` (renamed; internal `TOOL_ID` and cookie comments updated `ue002` → `ca002`)
- `free-tools.html` — calculator card links updated to `tool-ca001.html` / `tool-ca002.html`
- `TOOL_REGISTRY.md` — Active Tools now lists CA001/CA002; UE001/UE002 recorded under Retired / Superseded; next available IDs CK005, CA003
- `handoffs/threeflows_handoff_v0529.md` — pointer banner added noting the UE naming is superseded

---

## Tool Series

The calculator and checklist series both follow the same standard tool-page pattern.

**Naming convention for tool IDs:**
- `CK` — Checklist tools
- `CA` — Calculator tools (unit-economics / financial-model calculators live here too)

`.tool-note`, `.tool-note.red`, and `.tool-note.green` remain the canonical callout classes for interactive tool pages (introduced in CA001). Do not use `.callout-*` on tool pages — those are blog-only. See STYLE.md section 6.

---

## Tool Pages — Component Reference

**Active tools:**
| ID    | Type       | File             | Title                           | Last revised |
|-------|------------|------------------|---------------------------------|--------------|
| CK001 | Checklist  | tool-ck001.html  | Pre-Launch Planning Checklist   | May 8, 2026  |
| CK002 | Checklist  | tool-ck002.html  | Sample Sourcing Checklist       | May 8, 2026  |
| CK003 | Checklist  | tool-ck003.html  | Voice of Customer Checklist     | May 8, 2026  |
| CK004 | Checklist  | tool-ck004.html  | Company and Brand Setup Checklist | May 8, 2026 |
| CA001 | Calculator | tool-ca001.html  | Unit Economics & Cashflow Model | May 29, 2026 |
| CA002 | Calculator | tool-ca002.html  | Last-Mile Rate Calculator       | June 3, 2026 |

**Next available IDs:** CK005, CA003

**Standard tool page pattern:**
- Breadcrumb: `← Free Tools` → `free-tools.html`
- Email gate: side-by-side 50/50 flex layout (First name + Email)
- Gate button: `btn-red` "Access Tool →" — JS gate reveal
- No info banner
- Bottom section: `.tool-cta-card` (white bordered card, NOT `.bottom-cta`)
- Callouts inside tool content: `.tool-note`, `.tool-note.red`, `.tool-note.green` — never `.callout-*`

**Cookie convention:** `tf_tool_<id>` — e.g. `tf_tool_ck001`, `tf_tool_ca001`.

**Bug report mailto:**
`contact@threeflows.com?subject=Feedback&body=Page%20URL%3A%20%0ATool%20name%3A%20%0AFeedback%3A%20`

---

## Carried Forward From v0529

All other operational content from `threeflows_handoff_v0529.md` remains in force, except the `UE` naming superseded above. This includes: page titles format (`[Page Name] — Three Flows Solutions`), contact.html step-strip reference, tab system reference (`setTab` / `setSvc3Tab` / `setContactTab`), the blog chain reference, and the To-Do list. Refer to v0529 for those sections.

Still open from the v0529 To-Do list:
- Footer Privacy & Terms links are `href="#"` placeholders sitewide — replace before launch.
- `inquiry.html` / `intake.html` still carry the old nav structure.
- `.tool-note` should be documented in STYLE.md section 6 at the next style audit.
- Shared stylesheet extraction (tech debt) — see STYLE.md section 8.

---

## Git Hygiene

**Standard workflow:**
- Always work on a branch — never commit directly to main
- Claude Code opens PRs via GitHub REST API — merging is always a manual step
- After merge, GitHub Pages redeploys in ~1–2 minutes. CDN propagation up to 10 minutes for new files.

**Commit message conventions:**
- Style fixes: `"Style audit fixes — [description] ([issue refs])"`
- New pages: `"Add [filename] — [one-line description]"`
- Content updates: `"[filename]: [what changed]"`
- Infrastructure: `"Add/Update [filename] — [purpose]"`
