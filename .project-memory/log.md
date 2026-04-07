# Project Memory Log

## Purpose

This file is the chronological log of meaningful updates to project memory and curated docs.

It should help future agents answer:
- what changed recently
- when the memory/docs were updated
- why a change was recorded
- what kind of change it was

This is not a full changelog of every code edit.
It is a compact memory/doc evolution log.

---

## Entry Format

Use this heading format for each entry:

`## [YYYY-MM-DD HH:MM] <type> | <short title>`

Examples of `<type>`:
- bootstrap
- session
- bugfix
- refactor
- decision
- ingest
- lint
- task-update
- lesson-update
- architecture-update

---

## Example Entry

## [2026-04-07 15:20] bootstrap | initialize project memory framework

### Summary
Initialized `.project-memory/` and first-pass architecture docs.

### Touched
- `.project-memory/source-roots.md`
- `.project-memory/current-focus.md`
- `.project-memory/index.md`
- `docs/architecture/system-overview.md`

### Why
Repository was being initialized for agent-readable work.

### Follow-up
- confirm code roots
- refine module graph
- fill recent lessons after first real session

---

## Logging Rules

- Log meaningful memory/doc updates only
- Prefer concise entries
- Use log entries for visibility, not essay-writing
- Tiny changes may be omitted unless they matter later
- Medium/heavy changes should usually leave a log entry
- Lint passes should leave a log entry

---

## Current Entries

<!-- append new entries below -->