# Decisions

## Purpose

This directory stores **durable technical decisions**.

A decision note explains:
- what was chosen
- why it was chosen
- what alternatives were considered
- what consequences follow from the choice

These files help future agents answer:
- why is the system designed this way?
- what tradeoff was accepted?
- what changed from a previous approach?

---

## When to Create a Decision Note

Create a decision note when one of these is true:

- a source of truth changes
- a module boundary changes
- an important technical approach is selected over alternatives
- a previous decision is reversed
- an integration strategy is chosen
- an important tradeoff is accepted
- future sessions are likely to ask “why was this done?”

Do **not** create a decision note for every small local choice.

---

## What Does Not Belong Here

Do not use this directory for:
- tiny refactors
- trivial bugfixes
- routine task progress
- raw brainstorming dumps
- duplicated architecture overviews
- ephemeral chat summaries

Those belong in:
- `.project-memory/`
- `docs/modules/`
- `docs/architecture/`
- `docs/raw/`

depending on the case.

---

## File Naming

Recommended pattern:

- `DEC-0001-short-title.md`
- `DEC-0002-short-title.md`

Use stable IDs if possible.

---

## Status Values

Common status values:
- proposed
- confirmed
- deprecated
- superseded

When a decision is reversed or replaced, mark the older file clearly.

---

## Recommended Template

Use:
- `docs/agent/templates/decision-note.md`

Each decision note should usually include:
- ID
- date
- status
- context
- decision
- alternatives considered
- why
- consequences
- follow-up
- supersession info if relevant

---

## Relationship to Other Docs

- `docs/architecture/` explains the current shape of the system
- `docs/modules/` explains module responsibilities and boundaries
- `docs/decisions/` explains why important long-lived choices were made
- `.project-memory/` tracks current working state and hot lessons

A decision may later influence:
- architecture docs
- module docs
- current focus
- lessons

---

## Maintenance Rule

Keep decision notes concise and durable.

When reviewing old decisions, ask:
- is this still active?
- has it been reversed?
- does it still match the codebase?
- should it be marked deprecated or superseded?

Do not keep stale decisions in an ambiguous state.