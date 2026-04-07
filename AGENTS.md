# AGENTS.md

## Purpose

Give the agent a **map**, not a manual.

- code, tests, configs → source material
- `docs/` → curated long-lived docs
- `.project-memory/` → dynamic working memory

---

## Init Gate

**Initialized** = both exist:
- `.project-memory/source-roots.md`
- `.project-memory/current-focus.md`

Missing either → read `docs/agent/FIRST_RUN.md`

---

## Normal Entry

Read in order, stop when enough context is available:

1. `.project-memory/current-focus.md`
2. `.project-memory/tasks/active.md`
3. `docs/architecture/system-overview.md`
4. relevant `docs/` and `.project-memory/` files

Operational guidance → `docs/agent/index.md`

---

## Source of Truth

1. code and tests
2. runtime / config behavior
3. current user instruction
4. curated docs
5. old project memory

Memory contradicts code → update the memory.

---

## Updates

| scope | action |
|-------|--------|
| tiny | `log.md` only if useful |
| medium | update affected memory / docs |
| heavy | update architecture / decisions / memory |

Details → `docs/agent/memory-update-policy.md`

Only preserve durable engineering knowledge.
No raw chat. No restating code.

---

## Working Style

- targeted reads, not broad reads
- compact, navigable docs
- mark uncertainty explicitly
- `docs/raw/` = source material
- `.project-memory/` = working memory, not sole truth