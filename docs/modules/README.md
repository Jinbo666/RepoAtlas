# Modules

## Purpose

This directory stores **module notes** for important parts of the repository.

A module note explains:
- what a module is responsible for
- what it is not responsible for
- where its entry points are
- what it depends on
- how it participates in runtime behavior
- what fragile seams or risks exist

These files help future agents navigate the codebase faster and more safely.

---

## What Counts as a Module

A module may be:
- a major package
- a service boundary
- a pipeline or subsystem
- a frontend area
- a backend area
- a data layer
- an integration layer

Do not create one file per tiny directory by default.
Prefer meaningful engineering boundaries.

---

## When to Create a Module Note

Create a module note when one of these is true:

- the module is important to understanding the system
- the module is a repeated work area
- the module has non-obvious boundaries
- the module has fragile seams or recurring bugs
- future work will likely revisit the area
- the area appears in tasks, decisions, or lessons repeatedly

Do not create many module notes on first run unless the structure is already very clear.

---

## What Does Not Belong Here

Do not use module notes for:
- raw brainstorming
- long history dumps
- routine progress logs
- generic architecture overviews
- repeated code restatements that add no durable value

Those belong elsewhere.

---

## Recommended Template

Use:
- `docs/agent/templates/module-note.md`

Each module note should usually include:
- status
- source of truth files
- related tasks
- related decisions
- related lessons
- responsibility
- non-responsibility
- entry points
- inputs/outputs
- dependencies
- runtime role
- known risks / fragile seams
- durable change notes

---

## Naming Guidance

Use names that match the engineering boundary, for example:
- `api.md`
- `frontend.md`
- `training-pipeline.md`
- `data-layer.md`
- `scheduler.md`

Prefer stable, human-readable names.

---

## Relationship to Other Docs

- `docs/architecture/` describes top-level system shape
- `docs/modules/` describes important local boundaries and responsibilities
- `docs/decisions/` explains why certain durable choices were made
- `.project-memory/` tracks current state, active tasks, and hot lessons

Module notes may reference:
- decisions
- tasks
- lessons
- architecture docs

---

## Maintenance Rule

Update a module note when:
- responsibilities change
- boundaries change
- important entry points move
- a recurring risk becomes clear
- durable understanding improves

Do not rewrite module notes for every tiny edit.
Prefer compact, durable updates.