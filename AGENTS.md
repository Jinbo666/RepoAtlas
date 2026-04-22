# AGENTS.md

## Purpose

Give the agent a **map**, not a manual.

- code, tests, configs → source material
- `docs/` → curated long-lived docs
- `project-memory/` → dynamic working memory

---

## Archetype

Stored at the top of `project-memory/source-roots.md`.

- `auto` (default) — run detection per `docs/agent/archetypes/detection.md`, write result back, do not ask unless ambiguous
- `code` — application / engineering project
- `docs-kb` — knowledge base / docs compilation project (raw docs are primary truth; curated layer = topics / concepts / glossary / summaries)

If resolved to `docs-kb`, also read `docs/agent/archetypes/docs-kb.md` before acting.

---

## Init Gate

**Initialized** = both exist:
- `project-memory/source-roots.md`
- `project-memory/current-focus.md`

Missing either → read `docs/agent/FIRST_RUN.md`

---

## Normal Entry

Read in order, stop when enough context is available:

1. `project-memory/current-focus.md`
2. `project-memory/tasks/active.md`
3. main curated entry — `docs/architecture/system-overview.md` (`code`) or `docs/topics/README.md` (`docs-kb`)
4. relevant `docs/` and `project-memory/` files

Operational guidance → `docs/agent/index.md`

---

## Source of Truth

Default (`code` archetype):

1. code and tests
2. runtime / config behavior
3. current user instruction
4. curated docs
5. old project memory

Memory contradicts code → update the memory.

`docs-kb` archetype: raw docs → user instruction → curated docs → old memory. See `docs/agent/archetypes/docs-kb.md`.

---

## Updates

| scope | action |
|-------|--------|
| tiny | `log.md` only if useful |
| medium | update affected memory / docs |
| heavy | update architecture / decisions / memory |

Ingest raw docs → `docs/agent/memory-update-policy.md` § Raw Doc Ingestion Protocol

Details → `docs/agent/memory-update-policy.md`

Only preserve durable engineering knowledge.
No raw chat. No restating code.

---

## Working Style

- targeted reads, not broad reads
- compact, navigable docs
- mark uncertainty explicitly
- `docs/raw/` = source material
- `project-memory/` = working memory, not sole truth