# Architecture

*Last updated 2026-07-02*

This document describes the **target architecture** for the Threeflows website — the intended design of the site. Some parts are already built and live; others are not yet implemented. Anything not yet in the repo is marked **(not yet built)**. As each piece ships, its tag is removed, so over time this document converges on the current state of the site.

For scope and boundaries, see SCOPE.md. For visual/styling decisions, see STYLE.md and STYLE.css.

---

## Pages

The primary pages are home, services, resources, about, and contact. There are also hidden pages, not reachable from the global nav (see Hidden pages).

**Home** — landing page leading to the rest of the site.

**Services** — four sub-pages, one per major service:
- svc1 — Business planning
- svc2 — Sourcing consultation
- svc3 — Launch hypercare
- svc4 — Ongoing management

**Resources** — free/paid education materials: blogs and articles, useful websites, checklists & calculators, webinars & seminars, and a livestream schedule. Each has its own section below.

**About** — introduction of principles, and introduction of clients (client cards are a styled component; see STYLE.md).

**Contact** — connect via a form (see Form-ish, and the Contact section below).

---

## Page layout (nav + footer) — *(not yet built)*

`partials.html` holds the shared nav and footer markup. Each page fetches it and injects it into placeholder containers via a small vanilla-JS snippet on load. Because every page pulls `partials.html` at load time, editing that one file updates the nav and footer across all pages — a single source, with no per-page copies and therefore no drift.

The nav renders as horizontal dropdown menus on desktop and collapses to a hamburger menu on mobile.

Note the tradeoff: the nav renders via JavaScript, so it depends on JS loading. This replaces the current failure mode (on mobile there is presently no nav at all — see Backlog/known issues) with a soft dependency on JS.

**Relationship to templates:** two independent mechanisms produce consistency and should not be confused. Content templates (see Blogs, Tools) govern the repeatable *content structure* of a page type and are applied once at page creation. `partials.html` governs *nav and footer* and is fetched at load time so edits propagate everywhere. Templates do not contain nav/footer; every page — including pages created from a template — gets its nav and footer from `partials.html`.

---

## Blogs

Blog index: https://threeflows.com/blog.html

**Blog behavior (how the blog works):** posts are sorted in descending date order; previous/next links are based on dates.

**When creating a post (workflow):** always ask the admin for the posting date, and ask for the primary and secondary tags.

New posts are created from `blog-000-template.html`, which defines the shared post content structure and styling. Nav and footer come from `partials.html` via the fetch snippet (not baked into the template). Post content styling is defined in STYLE.md (blog style). Contact/data-capture behavior, where relevant, follows the Form-ish pattern.

---

## Reference (useful websites)

https://threeflows.com/useful-websites.html

A tabbed page. Each tab shows relevant cards with an entity description, brief intro, logo, and hyperlink to the site. Tabs include Market insights & compliance, Business management, and Top e-commerce marketplaces.

Cards are a shared CSS component (styled via STYLE.css), **not** a template. A new card is added by copying an existing card's minimal HTML block and changing its content; removing a card is deleting its block; restyling all cards is a single CSS edit. See STYLE.md for the card component.

Note: useful-websites and free-tools use **distinct** card styles. Whether they share a common base is a styling decision deferred to STYLE.css.

---

## Tools

https://threeflows.com/free-tools.html

Offers free tools: checklists, calculators, and references.

Tool cards are a CSS component (see STYLE.md), not a template. Tool *pages* use the shared blocks in the gate pattern (email gate → tool body → CTA; the tool, not a submission, is the goal — see Form-ish). Contact (email) is captured; the user's tool entries are not.

**(Not yet built) — retire per-type tool templates.** The existing scaffolds `tool-ca000` (calculators) and `tool-ck000` (checklists) *(confirm exact names against repo)* are to be retired as the creation method. New tools use the shared blocks plus a per-tool body, rather than a separate template per tool type. Retiring the scaffolds does **not** remove or break the live tool pages already built from them; those pages migrate to the shared-blocks / partials model like every other page.

---

## Webinars

https://threeflows.com/webinars.html

Offers presentation materials and social media links. Uses the shared blocks in the gate pattern (contact captured to release materials — see Form-ish).

---

## Livestream

https://threeflows.com/livestream.html

Intends to link to a calendar for the livestream. Placeholder / coming soon. Paywall not built.

---

## Contact

https://threeflows.com/contact.html

The contact page surfaces two forms:

- **Contact Us (primary)** — a unified, email-style contact form. This consolidates what were previously separate "inquiry" and "send feedback" mechanisms into one.
- **Intake (secondary, subdued)** — the longer form for serious clients / CS-assisted use, kept but de-emphasized.

Both use the shared blocks (form / gate pattern — see Form-ish), and both capture contact to a Google endpoint.

**(Not yet built) — redesign the page.** The redesign promotes Contact Us to the primary display and consolidates inquiry + send feedback into it. This redesign depends on `partials.html`, STYLE.css, and the shared form blocks all existing first, and is therefore sequenced after those.

---

## Hidden pages

Hidden pages may be various HTML pages. They are intentionally hidden and **must not be added to the nav**. They are available only via link/invitation, and the admin dictates when (or whether) to show any of them. Any hidden page can be unhidden at the admin's request.

There are currently two types: surveys and materials.

**Surveys**
- The survey URL is sent directly to a target audience; surveys are not in the nav.
- Only one survey is active at a time; past and future surveys stay hidden.
- No survey template — each survey differs.
- Results go to a Google Sheet.
- `surveys.html` serves as the cover page; `svy###.html` is each individual survey (active or inactive).

**Materials**
- `mtl###.html` — no fixed format.
- Materials can appear in multiple places, gated by various CTAs.
- A material is currently gated behind a survey, so it collects no contact of its own (the survey already captured it). If a material is later unhidden to the public, it may need its own contact-capture block, since the survey gate no longer applies.

---

## Inventory (dependencies)

- **Google Fonts** — DM Serif Display + DM Sans, sitewide via CDN.
- **Chart.js 4.4.1** — confined to specific blog posts.
- **D3.js 7.8.5** — blog posts only.
- **TopoJSON 3.0.2** — blog posts only (companion to D3).
- **us-atlas@3** — blog posts only (map data for the D3 charts).
- **api.mailcheck.ai** — disposable-email screening on the tool gate forms.
- **Google favicon service** — favicon images on the useful-websites and free-tools resource cards.
- **Explicitly absent:** no analytics/trackers, no ad pixels, no JS/CSS UI frameworks (no React/Vue/jQuery).

---

## Deploy config

- `CNAME` present.
- **(Not yet built)** Add `.nojekyll` to disable the unused Jekyll build path (the site is hand-authored static and does not use Jekyll features). Reversible — delete the file to re-enable Jekyll.
- No CI/CD workflows.

---

## Soft constraints

- No JS/CSS frameworks (hard constraint, per SCOPE.md). Data-visualization libraries (D3, Chart.js, TopoJSON) are accepted **by exception** on the individual blog posts that need them — loaded per-page via CDN, not sitewide.
- mailcheck.ai for disposable-email screening; no analytics.

---

## Form-ish — *(target state)*

Several page types share a set of reusable blocks: partials (nav/footer), a contact-info capture block, a thank-you block, a Google endpoint, and a CTA button. A page composes the blocks it needs; its body varies. Two shapes recur: the **form** shape (collect info → submit → thank-you → endpoint; the submission is the goal) and the **gate** shape (capture an email to unlock → deliver the tool/content → CTA; the email is a threshold, not the payload).

The matrix below is target-state. "Contact info = yes" means the client's contact is captured to a Google endpoint. "User entry in Google endpoint = yes" means the client's body input (not just their contact) is captured.

| Page | Partials | Contact info | Thank you | User entry captured | CTA button |
|---|---|---|---|---|---|
| blog | yes | no | no | no | no |
| contact | yes | yes | yes | yes | no |
| intake | yes | yes | yes | yes | no |
| survey### | yes | yes | yes | yes | no |
| checklist | yes | yes | no | no | yes |
| calculator | yes | yes | no | no | yes |
| materials | yes | yes | no | no | yes |

CTA button actions vary by page (unlock a tool, reveal content, route elsewhere) — the same styled component, different actions.

Note: the *materials* row reflects the future public state (its own contact capture). While a material is gated behind a survey, it captures no contact of its own.
