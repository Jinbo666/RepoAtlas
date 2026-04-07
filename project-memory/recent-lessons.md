# Recent Lessons

## Purpose

This file stores the repository's **hot-layer lessons**:
recent pitfalls, debugging conclusions, and implementation rules that are still likely to matter in near-future work.

This is not the permanent archive of every past mistake.
It is the active reminder layer.

Use this file to help future sessions avoid repeating known mistakes.

---

## What Belongs Here

Keep lessons here when they are:

- still likely to recur
- recently discovered
- not yet fully absorbed into architecture/docs/code habits
- useful as short-term warnings for active work

Examples:
- a recurring config mistake
- a root cause discovered during debugging
- a recently clarified implementation boundary
- a fragile integration behavior that is easy to forget

---

## What Does Not Belong Here

Do not use this file for:

- raw debugging transcripts
- every tiny bugfix
- generic advice with no project-specific value
- stale lessons that no longer match the codebase
- long architecture essays
- decisions that belong in `docs/decisions/`

If a lesson becomes stable and long-lived, promote it into:
- `docs/architecture/invariants.md`
- `docs/decisions/`
- `docs/modules/`

If a lesson is no longer useful, retire or remove it.

---

## Status Values

Use one of these:

- `active` — still important and likely to recur
- `cooling` — less urgent now, but still worth remembering
- `retired` — no longer relevant in the current codebase
- `graduated` — promoted into a more durable doc such as architecture, decisions, or module notes

---

## Lesson Entry Template

## L-<ID> <Short Title>

- Status:
- Date:
- Scope:
- Related modules:
- Related tasks:
- Related decisions:

### Trigger / Symptom
What went wrong, or what symptom appeared?

### Root Cause
What was the actual underlying cause?

### Correct Handling
What should be done correctly next time?

### Prevention Rule
What reusable rule should future work follow?

### Evidence
How was this confirmed? Code, tests, runtime behavior, or debugging outcome.

### Graduation Target
Should this eventually move into:
- architecture invariant
- decision note
- module doc
- none

### Notes
Anything else future sessions should know.

---

## Example Entries

## L-0001 Config source split between UI and backend

- Status: active
- Date: 2026-04-07
- Scope: configuration flow
- Related modules: frontend, backend, config service
- Related tasks: unify configuration handling
- Related decisions: DEC-0003

### Trigger / Symptom
The UI appeared updated, but runtime behavior still used a different configuration source.

### Root Cause
Configuration truth was split across UI-local state and backend/runtime config resolution.

### Correct Handling
Treat backend/runtime config resolution as the single source of truth and ensure the UI reflects it instead of inventing a second source.

### Prevention Rule
Do not introduce a second config source for convenience.

### Evidence
Confirmed through runtime behavior and code inspection.

### Graduation Target
architecture invariant

### Notes
Check this whenever config-related work touches both frontend and backend.

---

## L-0002 Bugfix changed local behavior but not module contract

- Status: cooling
- Date: 2026-04-08
- Scope: API contract updates
- Related modules: api, frontend
- Related tasks: align API and callers
- Related decisions: none

### Trigger / Symptom
A local fix solved one path but other callers still assumed the old contract.

### Root Cause
The fix was applied at one usage point instead of updating the contract understanding across the module boundary.

### Correct Handling
When behavior crosses a module boundary, inspect the contract and affected callers, not only the first failing path.

### Prevention Rule
Do not patch symptoms at one call site if the real issue is a shared contract.

### Evidence
Confirmed through failing tests and multiple call sites inspection.

### Graduation Target
module doc

### Notes
Most useful when fixing behavior that spans frontend/backend or service/client boundaries.

---

## Maintenance Rule

Review this file during lint or after medium/heavy work.

For each lesson ask:

- Is this still an active risk?
- Was the root cause actually confirmed?
- Has the codebase changed enough to retire this?
- Should this lesson graduate into architecture, decisions, or module docs?

Keep this file short and current.

---

## Ordering Rule

Prefer ordering lessons from most recent / most active to less active.

Put the hottest lessons first.

---

## Last Reviewed

- Date:
- Notes: