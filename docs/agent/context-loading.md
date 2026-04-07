# Context Loading

## Purpose

This file defines how to load **just enough context** for a task.

Context is limited.
Do not read the whole repository, the whole `docs/`, or the whole `project-memory/` by default.

The goal is:
- load the minimum useful context
- stop early when enough understanding is available
- prefer targeted reads over broad reads

---

## Default Loading Order

On a normal task or new session, load in this order and stop as soon as enough task-relevant context is available:

### Mandatory
1. `project-memory/current-focus.md`
2. `project-memory/tasks/active.md`
3. `docs/architecture/system-overview.md`

### Task-directed
4. relevant files under:
   - `docs/architecture/`
   - `docs/decisions/`
   - `docs/modules/`
   - `project-memory/`

### Operational guidance
5. only if needed:
   - `docs/agent/memory-update-policy.md`
   - `docs/agent/lint-and-health.md`
   - templates under `docs/agent/templates/`

### Raw source fallback
6. raw code, tests, configs, and `docs/raw/` as needed

---

## Stop Rule

Stop loading more context when all of the following are true:

- the task scope is clear
- the relevant modules are identified
- the likely source of truth is known
- the next action can be taken safely

Do not continue reading “just in case”.

---

## Task-Specific Loading Profiles

### A. Narrow bugfix
Prioritize:
1. `project-memory/current-focus.md`
2. `project-memory/tasks/active.md`
3. `docs/architecture/system-overview.md`
4. affected code/tests/configs
5. relevant module docs
6. `project-memory/recent-lessons.md`
7. recent `log.md` entries only if recent history matters

Do not read broad architecture or many decision files unless the bug crosses boundaries.

---

### B. Small feature or local refactor
Prioritize:
1. current focus
2. active tasks
3. system overview
4. relevant module docs
5. related code/tests/configs
6. related decision notes if the area already has decisions

---

### C. Architecture / cross-module change
Prioritize:
1. current focus
2. active tasks
3. system overview
4. `docs/architecture/module-graph.md`
5. `docs/architecture/invariants.md`
6. relevant decision files
7. relevant module docs
8. affected code/tests/configs

Load more broadly here, but still only around the affected area.

---

### D. Raw doc ingestion / legacy doc interpretation
Prioritize:
1. source roots
2. current focus
3. system overview
4. the raw docs being discussed
5. related architecture / decision / module docs
6. source registry if present

Do not rewrite raw docs unless explicitly asked.
Treat raw docs as source material.

---

### E. Memory cleanup / drift investigation
Prioritize:
1. current focus
2. recent `log.md`
3. active tasks
4. recent lessons
5. system overview
6. affected docs and code
7. `docs/agent/lint-and-health.md`

---

## Reading Budget Rules

### Prefer summaries before detail
Read:
- overview pages before module pages
- module pages before raw docs
- curated docs before broad codebase scans

### Prefer direct evidence near the task
If the user asks about a specific module, file, API, or behavior:
- inspect the relevant code/tests/config directly
- do not over-rely on memory summaries

### Prefer recency only when recency matters
Use recent `log.md` and recent lessons when:
- the task is about recent changes
- a regression may have been introduced recently
- a recent refactor likely changed assumptions

Otherwise, skip them.

### Prefer architecture only when boundaries matter
Use architecture and decisions when:
- changing module boundaries
- changing source of truth
- changing data/control flow
- changing integration behavior

---

## Source-of-Truth Reminder

When conflicts exist, prefer:

1. code and tests
2. runtime/config behavior
3. current user instruction
4. curated docs
5. old project memory

If memory contradicts code, update the memory.

---

## Must Not Do

- Do not read all memory files by default
- Do not read all raw docs by default
- Do not treat `project-memory/` as complete truth
- Do not keep reading after the next safe action is already clear
- Do not confuse navigation docs with project facts

---

## Output Behavior

After loading context, the agent should form a concise working model:

- task type
- relevant modules
- likely source of truth
- likely risks
- next step

This working model may stay implicit unless the user asks for it, but it should guide the work.