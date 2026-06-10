# claude.md

claude_2026-06-10-001

## Purpose

These are the universal rules governing how Claude (Chat and Code) operates on
every project. They apply across all repos. Project-specific rules live in the
project's own files (process.md, scope.md, style.md, architecture.md) and refine
— never override — what is here.

## Source of truth and memory

- GitHub `main` is the single source of truth for "what is the latest." Never
  treat a chat, a Code session, or a local file as authoritative over `main`.
- There is no cross-chat or cross-session memory. No chat or Code session can
  read another. Never assume the state of another session; re-fetch the current
  state from the repo at the start of work.

## Session start: read order

At the start of every Code session, before making any change, read the project
files in this order:

1. claude.md (this file — the project's local copy)
2. process.md
3. handoff.md
4. style.md / scope.md / architecture.md, if present

Follow claude.md first, then process.md. If they conflict, or if a required file
is missing, STOP and ask the user. Do not assume and do not proceed.

## Don't assume — stop and ask

If anything is missing, ambiguous, or uncertain, stop and ask before doing any
work. Never guess at a file's contents, a convention, or the user's intent.

## Branching and merge

- Code always works on a branch. Never commit directly to `main`.
- When starting a task, Code suggests the branch name for the user to confirm.
  Branch names follow the format prefix/topic. Common prefixes: feature/ (new
  page or capability), fix/ (bug or content correction), chore/ (config,
  tooling, non-content changes), content/ (copy or asset updates only).
- Code never merges. Before merging, Code asks the user for review and launches
  the browser preview (the user may also review the pull request on GitHub).
- The user merges manually. Merge auto-triggers launch; there is no separate
  publish step. The PR preview is the last point of control.

## Visual mock before prompt

For significant UI/UX changes, Chat sends a visual mock after discussion and
before writing any prompt. For minor changes (e.g. typo corrections), this step
may be skipped.

## File and folder discipline

- Do not retro-create folders or rename files — it breaks the code.
- Never create files locally and reverse-sync them. Create on a branch via the
  normal flow.
- To read a shared file, take it from an upload in Chat or from a separate local
  folder. Never read project files from, or write them into, the clone folder
  outside the normal branch flow.
- A plain `topic.md` (no date) is always the live/current version. Archives are
  named `topic_yyyy-mm-dd-###.md` and kept in the same folder.

## Handoff

- On the user's request, Code generates handoff.md in the handoff folder, and
  creates an identical copy named `handoff_yyyy-mm-dd-###-[tag].md`.
- handoff.md is a running balance: it always reflects the full current state of
  `main`, not just the last PR.

## Archiving

- Whenever claude.md, scope.md, architecture.md, style.md, process.md, or
  template files are updated, create an archived copy in the same folder
  (`topic_yyyy-mm-dd-###.md`) alongside the updated live file.

## UAT protocol

- All writes to uat.xlsx are made by Code. The user never edits uat.xlsx; any
  manual edit will be overwritten. The user controls the CLOSED/REOPENED
  decision and instructs Code; Code performs the write.
- quick-log.xlsx is the user's private, gitignored scratch buffer. Code never
  reads from or writes to it.
- Logging a batch: after the user aligns with Chat on the issues, Code logs each
  issue into uat.xlsx — assigning an ID, setting status OPEN, and writing a
  robust issue description — then commits uat.xlsx so the batch is durably saved
  before any fixing begins.
- Amending a description: if an issue is described incorrectly, Code amends the
  description in uat.xlsx on a commit, on the user's instruction.
- Fixing an issue: Code works on a branch, applies the fix, flips that issue's
  status to FIXED in uat.xlsx within the same branch, and opens a PR. The
  uat.xlsx change rides in the PR; reviewing the PR is the review. There is no
  separate local-file step.
- After UAT on the PR preview: if it passes and the user merges and tags, Code
  (when instructed) writes the handoff and marks the issue CLOSED in uat.xlsx as
  a follow-up commit. If it fails, Code marks the issue REOPENED and re-enters
  the fix flow until it passes.
- Status lifecycle: OPEN → FIXED → CLOSED, with REOPENED on a failed UAT.
- uat.md is a living document; no archived version is created until the user
  asks for one.
- New feature or UI decisions that prove durable may be promoted into style.md.
