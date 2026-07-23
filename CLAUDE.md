# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Prep materials for a conference talk: **"Agents Are Products, Not Prompts"**, a 60-minute
session at **CincyDeliver 2026** (Friday, July 24, 2026). Abstract:
https://www.cincydeliver.org/Sessions/Details/7586

This is not a software project — there is no build, lint, or test tooling. All work here is
editing Markdown planning docs, a `.pptx` deck, and one sample agent-definition file used as a
live demo artifact.

## Layout

Everything lives under `CincyDeliver Talk 2026/` (note the space in the directory name — quote
it in shell commands).

- **`outline.md`** — the living source of truth for the talk. Contains the full section-by-section
  outline (§1–§10) with timing budgets, a "Reusable assets" inventory, a **"Deck status"** log
  (dated changelog of what's been built/fixed in the deck), and a **"Decisions locked"** section
  (settled scope/design calls with rationale — read this before proposing a structural change,
  it likely re-litigates something already decided).
- **`punch-list.md`** — the pre-talk TODO list ("Must do" / "Should do" / "Optional polish"),
  checked off with `~~strikethrough~~` + a completion date as items land. Keep this in sync with
  `outline.md`'s "Deck status" when work is completed.
- **`agents-are-products.pptx`** — the actual slide deck (built with pptxgenjs per the outline's
  Deck status notes). Binary; edit via regeneration script or PowerPoint, not directly.
- **`demo/architecture-reviewer.agent.md`** — a local copy of a real production agent definition
  (imported from `ai-code-workshop`'s `.github/agents/architecture-reviewer.agent.md`), used as
  the live decomposition example in §6 of the talk. Its structure (frontmatter → Identity & Role →
  Responsibilities → Context → Constraints → Analysis Process → Output Format → Tone → Examples)
  **is** the "Agent Components model" the talk teaches — treat this file as a demo artifact to be
  walked through on stage, not a template to genericize. It was deliberately trimmed to .NET-only
  content (Spring Boot stripped out) to keep the live demo focused.
- **`AGENTS.md`** — a one-line imported note (session abstract link); not a rules file.

## Working in this repo

- Talk content changes belong in `outline.md`. When you make a substantive change to the deck or
  outline, add a dated entry under "Deck status" (matching the existing terse, factual style) and
  update `punch-list.md` if it closes an open item.
- `outline.md`'s "Decisions locked" section exists specifically to prevent re-deciding settled
  questions (e.g., which agent anchors §6, why Modernization was dropped from §7, why §6's live
  model call was cut). Check it before suggesting structural changes.
- Flags like **`[from workshop]`** and **`[from blog]`** in the outline mark source material
  provenance (the `ai-code-workshop` repo and Shawn's blog, shawnewallace.com) — preserve them
  when editing those lines.
- `demo/architecture-reviewer.agent.md` is presented live and referenced by section number in the
  outline (§6). If you edit it, keep changes consistent with what §6/§8 of `outline.md` claims
  happens on stage (e.g., which violation gets flagged, whether a live model call is made —
  currently it is not; §6 uses pre-captured output per the 2026-07-22 revision).
