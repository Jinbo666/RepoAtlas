# FIRST_RUN.md

## Purpose

This file is only for the **first-time initialization** of this repository's agent-readable knowledge framework.

On first run, use this file as the main instruction entrypoint.

Your job is to inspect the repository, identify its major source roots, and initialize a minimal but useful documentation + memory structure so future sessions can work from a project map instead of starting from zero.

Do not treat this as a request to summarize every file.
Do not create a giant manual.
Create a thin, navigable first version.

---

## High-Level Goal

Initialize three layers:

1. **Raw Source Layer**  
   Existing code, configs, tests, logs, and raw human-authored docs.

2. **Curated Repository Docs**  
   Structured long-lived docs under `docs/`, such as architecture, decisions, modules, and agent operation docs.

3. **Dynamic Project Memory**  
   Working memory under `.project-memory/` for current focus, logs, tasks, recent lessons, and session history.

---

## Repository Roles

During first run, classify repository content into these buckets:

### A. Raw source roots
These are source-of-truth inputs and should usually remain in place.

Examples:
- `src/`, `app/`, `backend/`, `frontend/`
- `tests/`, `configs/`
- `docs/raw/`
- existing design drafts, pitfall notes, legacy notes, research notes

### B. Curated docs
These are structured, current, agent-readable docs under `docs/`.

Examples:
- `docs/architecture/`
- `docs/decisions/`
- `docs/modules/`
- `docs/agent/`

### C. Dynamic project memory
These are working-memory files under `.project-memory/`.

---

## First-Run Tasks

Complete the following in order.

### 1. Discover the repository shape
Inspect the repository and identify:

- main code roots
- test/config roots
- existing docs roots
- raw/legacy note locations
- major subsystems/modules
- major entry points

### 2. Create missing framework directories if needed
Create these only if they do not already exist:

- `docs/raw/`
- `docs/agent/`
- `docs/architecture/`
- `docs/decisions/`
- `docs/modules/`
- `.project-memory/`
- `.project-memory/tasks/`
- `.project-memory/sessions/`

Do not create unnecessary files beyond what is useful for initialization.

### 3. Initialize source roots
Create or update:

- `.project-memory/source-roots.md`

This file must record:
- code roots
- raw source roots
- curated docs roots
- dynamic memory roots
- the role of each root

This becomes the repository's root map for future incremental compilation.

### 4. Initialize a thin project map
Create or update these files with concise first-pass content:

- `.project-memory/index.md`
- `.project-memory/current-focus.md`
- `.project-memory/log.md`
- `.project-memory/tasks/active.md`
- `.project-memory/tasks/backlog.md`
- `.project-memory/tasks/done.md`
- `.project-memory/source-registry.md`
- `.project-memory/recent-lessons.md`

Rules:
- keep them thin
- prefer clarity over completeness
- do not invent details
- mark uncertainty explicitly

### 5. Initialize curated architecture docs
Create or update:

- `docs/architecture/system-overview.md`
- `docs/architecture/module-graph.md`
- `docs/architecture/invariants.md`

The first pass should identify:
- what the project does
- main execution/runtime flow
- major modules
- major entry points
- important dependency directions
- likely invariants / constraints
- unknowns that need confirmation

Do not try to describe every file.
Capture the top-level map only.

### 6. Initialize doc scaffolding
Create or update:

- `docs/decisions/README.md`
- `docs/modules/README.md`
- `docs/agent/index.md`
- `docs/agent/context-loading.md`
- `docs/agent/memory-update-policy.md`
- `docs/agent/lint-and-health.md`

Keep these lightweight.
Do not overfill them on first run.

### 7. Register existing raw documents
If raw or legacy project docs exist, do not rewrite them.
Instead:

- leave them in place
- classify them as raw source material
- add them to `source-roots.md` or `source-registry.md` as appropriate

If existing docs are already structured and current, they may remain where they are or be referenced from curated docs.

### 8. Write a bootstrap log entry
Append one entry to:

- `.project-memory/log.md`

Type:
- `bootstrap`

Record:
- what was initialized
- which roots were discovered
- which files were created
- which files were only partially filled
- what still needs human confirmation

---

## Important Constraints

### Do not do a giant repo dump
Do not summarize every directory or every file.
Do not create a 1000-line encyclopedia.

### Prefer top-down mapping
Start with:
- repository purpose
- major subsystems
- entry points
- cross-module boundaries
- active/raw docs roots

Then stop.

### Respect source of truth
When conflicts exist, trust in this order:

1. code and tests
2. current configs/runtime behavior
3. explicit current user instructions
4. curated docs
5. old memory/session notes

### Treat raw docs as source material
`docs/raw/` and similar legacy note folders are source material.
Do not casually overwrite them.

### Mark unknowns explicitly
If something is unclear, write:
- `unknown`
- `needs confirmation`
- `inferred from code structure`

rather than pretending certainty.

### Do not over-generate on first run
Do not create many module pages or decision files on first run unless the structure is already very clear and the user explicitly asked for it.

Prefer a small number of high-value files first.

---

## What Good First Run Looks Like

A good first run produces:
- a clear `source-roots.md`
- a usable `system-overview.md`
- a first-pass `module-graph.md`
- a thin `current-focus.md`
- a minimal task scaffold
- a bootstrap log entry
- no giant wall of prose

The goal is not completeness.
The goal is to make future sessions faster and safer.

---

## Output Summary Required

After finishing, provide a concise summary including:

1. discovered repository roots
2. files created
3. files updated
4. inferred major modules
5. unknowns / risks / areas needing confirmation

---

## After First Run

After initialization, future work should usually follow the normal workflow:

- read `AGENTS.md`
- read `.project-memory/current-focus.md`
- read relevant architecture / decision / module docs
- update memory incrementally after meaningful work

This file should not be the default read for every session.
It is primarily for initialization or major re-bootstrap of a repository.