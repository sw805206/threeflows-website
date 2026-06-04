# Claude Code — Standing Instructions
## Three Flows Solutions / threeflows-website repo

These instructions apply to every Claude Code session in this repo,
regardless of the task. Read this file before doing anything else.

---

## Step 1 — Sync local with GitHub before every task

Run these commands before reading or editing any file:

1. cd /Users/swai/multipage
2. git fetch origin
3. git checkout main
4. git pull origin main
5. Create a new working branch from this clean state

GitHub main branch is the source of truth.
Never read from local files without completing steps 1–4 first.
Stale local files are the #1 cause of previously merged changes
being silently overwritten.

---

## Step 2 — Read these two files before writing any code

1. STYLE.md — visual and UX source of truth
2. The latest file in handoffs/ — files follow the naming format
   threeflows_handoff_vMMDD.md (or vMMDDa, vMMDDb for same-day
   versions). Sort by filename descending and read the first result
   (e.g. `ls handoffs/ | sort -r | head -1`) — operational rules

If the handoff filename has changed (newer version exists),
read the most recent version. Both files must be read in full
before any HTML, CSS, or JS is written or edited.

---

## Step 3 — After completing any task

- Open the affected pages in Chrome browser for visual confirmation
- Confirm no previously working elements have been broken
- Commit with a descriptive message referencing the task or issue number

---

## Tool ID conventions

- Two tool series: **CK** = Checklist, **CA** = Calculator (financial-model /
  unit-economics calculators live in the CA series). The short-lived "UE"
  prefix was retired and consolidated into CA on June 3, 2026.
- IDs are sequential per series. **Next available: CK005, CA003.**
- `TOOL_REGISTRY.md` (repo root) is the authoritative tool registry; the latest
  handoff in `handoffs/` carries the current operational state.

---

## Rules that never change

- Never read from /Users/swai/multipage without git pulling first
- Never skip reading STYLE.md
- Never skip reading the handoff doc
- Always open Chrome preview after changes
- Always create a new branch — never commit directly to main
