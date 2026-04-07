# Active Tasks

## Purpose

This file tracks the repository's **currently active engineering tasks**.

It should answer:

- what work is in progress now
- what is blocked
- what matters most next
- which modules/docs/decisions are involved

This file is for active work only.
Do not leave completed tasks here indefinitely.

---

## What Belongs Here

Keep a task here when it is:

- currently being worked on
- paused but still active
- blocked but still important
- likely to be resumed soon
- important enough that future sessions need to see it quickly

Move tasks out when they are:
- clearly backlog
- clearly done
- no longer relevant

---

## Task Entry Template

# <Task Title>

- Status: active / blocked / paused
- Priority:
- Owner area:
- Related modules:
- Related decisions:
- Related lessons:

## Goal
What outcome is this task trying to achieve?

## Current State
What is the current known status?

## Constraints
What boundaries, invariants, or external constraints matter?

## Next Action
What is the next concrete step?

## Blockers
What is currently blocking progress?

## Completion Signal
How will we know this task is done?

## Notes
Anything a future session should know before continuing.

---

## Example Tasks

# Unify configuration source across UI and backend

- Status: active
- Priority: P1
- Owner area: configuration/runtime
- Related modules: frontend, backend, config service
- Related decisions: DEC-0003
- Related lessons: L-0001

## Goal
Ensure configuration is resolved from a single source of truth and exposed consistently across UI and runtime.

## Current State
The UI and backend still contain partially duplicated config assumptions.

## Constraints
Must preserve current runtime behavior and avoid introducing a second control path.

## Next Action
Trace config read/write flow and identify every place where local UI state is treated as authoritative.

## Blockers
Need confirmation on whether legacy endpoints are still in use.

## Completion Signal
All config reads/writes flow through one authoritative path, and affected callers reflect that design.

## Notes
Check architecture invariants before making structural changes.

---

# Document module boundaries for the training pipeline

- Status: paused
- Priority: P2
- Owner area: training pipeline
- Related modules: training-pipeline, data-layer
- Related decisions: none
- Related lessons: none

## Goal
Create a reliable module note for the training pipeline so future refactors have a clearer boundary map.

## Current State
There is enough understanding to draft a note, but the current implementation still has some ambiguous edges.

## Constraints
Avoid over-documenting unstable details that are likely to move soon.

## Next Action
Inspect main entry points and runtime flow before drafting the module note.

## Blockers
Need confirmation on which orchestration path is canonical.

## Completion Signal
A compact `docs/modules/training-pipeline.md` exists and reflects current responsibilities and boundaries.

## Notes
Best done after the next round of pipeline cleanup.

---

# Investigate stale task/memory drift after recent refactor

- Status: blocked
- Priority: P2
- Owner area: repository health
- Related modules: none
- Related decisions: none
- Related lessons: none

## Goal
Bring tasks, current focus, and recent lessons back into sync after a recent refactor.

## Current State
Some memory pages may no longer reflect current code structure.

## Constraints
Do not rewrite memory broadly without checking actual code and recent changes.

## Next Action
Run a targeted lint pass across current focus, active tasks, recent lessons, and architecture overview.

## Blockers
Need to confirm what changed most recently in affected modules.

## Completion Signal
Memory health returns to good, with stale items corrected or retired.

## Notes
This is a maintenance task, not a feature task.

---

## Ordering Rule

Order tasks by practical importance:

1. highest-priority active tasks
2. blocked tasks that still matter
3. paused tasks likely to resume soon

Keep the most important tasks near the top.

---

## Maintenance Rule

Review this file after meaningful work.

For each task ask:

- Is it still active?
- Is the next action still accurate?
- Should it move to backlog or done?
- Did a new blocker appear?
- Did related modules/decisions/lessons change?

Keep this file concise and current.

---

## Relationship to Other Task Files

- `active.md` — tasks in current or near-current execution
- `backlog.md` — not active yet
- `done.md` — completed tasks worth retaining briefly or structurally

Do not duplicate the same task across all three without a reason.

---

## Last Reviewed

- Date:
- Notes: