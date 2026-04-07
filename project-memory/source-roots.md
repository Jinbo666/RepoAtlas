# Source Roots

## Purpose

This file defines the repository's main source roots and the role of each root.

It helps future agents answer:
- where code lives
- where raw docs live
- where curated docs live
- where dynamic memory lives
- which areas are source material vs. maintained summaries

This file is a navigation and classification file.
It is not a full project summary.

---

## Code Roots

- `src/`
- `app/`
- `backend/`
- `frontend/`
- `tests/`
- `configs/`

> Replace the list above with the actual repository roots.

Role:
- primary implementation source
- tests and runtime behavior are high-trust evidence
- code and tests outrank memory when conflicts exist

Write policy:
- agent may modify these when doing actual engineering work
- changes here may require updates to docs or memory

---

## Raw Source Roots

- `docs/raw/`
- `notes/`
- `specs/`
- `research/`

> Replace with actual raw or legacy source locations.

Role:
- raw human-authored material
- source material for interpretation and incremental compilation
- may include drafts, pitfall notes, legacy docs, meeting notes, research notes

Write policy:
- default is read-only unless the user explicitly asks to edit raw docs
- do not casually rewrite source material

---

## Curated Docs Roots

- `docs/architecture/`
- `docs/decisions/`
- `docs/modules/`
- `docs/agent/`

Role:
- structured, maintained, agent-readable repository docs
- higher quality than raw notes, but still subordinate to code/tests
- used for navigation, architecture understanding, and durable decisions

Write policy:
- agent may update these deliberately when durable understanding changes

---

## Dynamic Memory Roots

- `project-memory/`
- `project-memory/tasks/`
- `project-memory/sessions/`

Role:
- dynamic working memory
- current state, recent lessons, recent logs, active task tracking
- should stay compact and current

Write policy:
- agent may update these as part of normal work
- avoid noise and duplication
- do not treat these as the only source of truth

---

## Source of Truth Priority

When conflicts exist, prefer:

1. code and tests
2. runtime/config behavior
3. current user instruction
4. curated docs
5. old project memory / session notes

---

## Incremental Compilation Notes

Changes in these roots may trigger memory/doc updates:

- code changes
- raw doc additions/edits/deletions
- curated doc changes
- important conversation conclusions

Important:
- raw source roots are not the same as curated docs
- curated docs are not the same as dynamic memory
- dynamic memory is not a substitute for code truth

---

## Initialization Notes

- Initialized on:
- Last reviewed on:
- Needs confirmation: