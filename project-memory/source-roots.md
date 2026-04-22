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

## Archetype

- Archetype: `auto`

Allowed values:
- `auto` — agent auto-detects on first session using `docs/agent/archetypes/detection.md` and writes the decided value back here. This is the default for new repositories.
- `code` — application / engineering project. Code and tests are primary source of truth.
- `docs-kb` — knowledge base / docs compilation project. Raw docs under `docs/raw/` are primary source of truth.

On first use the agent reads this line; if it is `auto` (or missing), it runs archetype detection, writes the result here, and logs one `archetype-detect` entry in `log.md`. After that, this field is sticky — re-detection only happens if the user sets it back to `auto` or explicitly asks.

If the detected value is `docs-kb`, also consult `docs/agent/archetypes/docs-kb.md` for archetype-specific behavior (curated layer shape, truth priority, lint checks).

---

## Code Roots

Applies to: `code` archetype (required). Under `docs-kb`, leave this section empty or note "not applicable".

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

Applies to: both archetypes. Under `docs-kb` this is the **primary** root.

- `docs/raw/`

> For `code` archetype, add additional raw locations if they exist (e.g. `notes/`, `specs/`, `research/`). For `docs-kb`, `docs/raw/` is typically the only raw root.

Role:
- raw human-authored material
- under `docs-kb`: primary source of truth
- under `code`: source material for interpretation and incremental compilation, subordinate to code/tests
- may include drafts, pitfall notes, legacy docs, meeting notes, research notes

Write policy:
- default is read-only unless the user explicitly asks to edit raw docs
- do not casually rewrite source material

---

## Curated Docs Roots

Under `code` archetype:
- `docs/architecture/`
- `docs/decisions/`
- `docs/modules/`
- `docs/agent/`

Under `docs-kb` archetype:
- `docs/topics/`
- `docs/concepts/`
- `docs/glossary.md`
- `docs/summaries/`
- `docs/decisions/` (editorial / structural decisions)
- `docs/agent/`

Role:
- structured, maintained, agent-readable repository docs
- under `code`: subordinate to code/tests
- under `docs-kb`: derived from and subordinate to raw docs
- used for navigation, understanding, and durable decisions

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

Under `code` archetype, when conflicts exist, prefer:

1. code and tests
2. runtime/config behavior
3. current user instruction
4. curated docs
5. old project memory / session notes

Under `docs-kb` archetype:

1. raw docs under `docs/raw/`
2. current user instruction
3. curated docs (`docs/topics/`, `docs/concepts/`, `docs/glossary.md`, `docs/summaries/`, `docs/decisions/`)
4. old project memory / session notes

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