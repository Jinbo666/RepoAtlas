# Agent Docs Index

## Purpose

This directory contains the repository's **agent operation docs**.

These files explain how to work with this repository as an agent-readable system:

- how to initialize the framework
- how to load context efficiently
- how to update project memory
- how to keep memory/docs healthy
- which templates to use when creating structured docs

Do not treat this directory as raw project knowledge.

Project facts live in:
- code and tests
- `docs/raw/`
- `docs/architecture/`
- `docs/decisions/`
- `docs/modules/`
- `project-memory/`

This directory contains **operational guidance for agents**, not the project facts themselves.

---

## Read by Scenario

### 1. First-time repository initialization
Read:

- `docs/agent/FIRST_RUN.md`

Use this only when the repository has not yet been initialized for the project-memory framework, or when a major re-bootstrap is explicitly requested.

Do not use `FIRST_RUN.md` as the default entrypoint for routine work.

---

### 2. Normal task / new session
Read in this order:

1. `project-memory/current-focus.md`
2. `project-memory/tasks/active.md`
3. `docs/architecture/system-overview.md`
4. relevant docs under:
   - `docs/architecture/`
   - `docs/decisions/`
   - `docs/modules/`
   - `project-memory/`

If deeper operational guidance is needed, then read:

- `docs/agent/context-loading.md`

---

### 3. After meaningful work
If the task produced durable engineering value, update as needed:

- `project-memory/log.md`
- `project-memory/current-focus.md` if priorities changed
- relevant task / decision / architecture / module docs

For detailed rules, read:

- `docs/agent/memory-update-policy.md`

---

### 4. Memory cleanup / repo drift / stale docs
Read:

- `docs/agent/lint-and-health.md`

Use this when:
- memory seems stale
- docs and code appear inconsistent
- tasks are outdated
- repeated mistakes are accumulating

---

### 5. Creating structured docs
Use templates under:

- `docs/agent/templates/`

Examples:
- module note
- decision note
- lesson note
- session note
- task note

---

## Directory Map

- `FIRST_RUN.md`  
  First-time initialization guide for bootstrapping the framework in a new repository.

- `context-loading.md`  
  Rules for loading only the minimum useful context for a task.

- `memory-update-policy.md`  
  Rules for tiny / medium / heavy updates to `project-memory/` and curated docs.

- `lint-and-health.md`  
  Rules for checking memory quality, stale claims, contradictions, and cleanup.

- `templates/`  
  Reusable templates for structured documentation.

---

## Source of Truth Reminder

When conflicts exist, prefer:

1. code and tests
2. runtime/config behavior
3. current user instruction
4. curated docs
5. old project memory

Do not preserve stale memory when code contradicts it.

---

## Working Style Reminder

- Prefer small targeted reads over broad reading
- Do not load all memory/docs by default
- Do not store raw chat transcripts
- Preserve durable engineering knowledge only
- Treat `project-memory/` as dynamic working memory, not as the only source of truth
- Treat `docs/raw/` as source material, not polished final truth

---

## Default Rule

For routine work:
- do not start from this file alone
- use this file as a navigation page
- start from current focus + active tasks + architecture overview

If `AGENTS.md` already directed you here, use this file for navigation and do not re-read `AGENTS.md` unless needed.