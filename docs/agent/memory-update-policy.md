# Memory Update Policy

## Purpose

This file defines how durable engineering knowledge should be compiled into:

- `project-memory/`
- `docs/architecture/`
- `docs/decisions/`
- `docs/modules/`

The goal is to preserve **high-value engineering knowledge** without turning the repository into a giant diary.

Do not store raw chat transcripts.
Do not rewrite large areas for small changes.
Update memory proportionally.

---

## What Counts as an Update Source

Durable knowledge may come from:

### A. Conversation increment
Examples:
- choosing one technical approach over another
- identifying a non-obvious constraint
- discovering a root cause
- clarifying a module boundary
- rejecting a prior assumption
- agreeing that “from now on we should do X”

### B. Document increment
Examples:
- new design docs
- edited specs
- deleted or superseded notes
- reorganized architecture docs

### C. Code/runtime increment
Examples:
- a bugfix with durable lessons
- an API contract change
- a refactor that changes module behavior
- tests that reveal actual behavior
- runtime incidents or debugging outcomes

---

## Change Levels

### 1. Tiny change
Examples:
- typo fix
- formatting cleanup
- trivial rename
- one-line config correction with no lasting consequence
- tiny local fix with no reusable lesson

Required:
- append to `project-memory/log.md` only if useful

Optional:
- update active task status if it truly changed

Do not create session notes or decisions for tiny changes.

---

### 2. Medium change
Examples:
- meaningful bugfix
- local feature change
- small refactor
- new lesson from debugging
- raw doc update that changes understanding of one module
- clarified task state that matters beyond this session

Required:
- append to `project-memory/log.md`
- update relevant files in `project-memory/`
- create or update one session note if the change has future value
- update one or more affected module / task / lesson pages as needed

Typical targets:
- `project-memory/log.md`
- `project-memory/tasks/active.md`
- `project-memory/recent-lessons.md`
- `project-memory/current-focus.md` if priorities changed
- `docs/modules/<module>.md` if module behavior understanding changed

---

### 3. Heavy change
Examples:
- architecture change
- source-of-truth change
- cross-module refactor
- important technical decision
- significant new invariant
- large raw-doc compilation that changes project understanding
- decision reversal with long-term consequences

Required:
- append to `project-memory/log.md`
- create or update one session note
- update `project-memory/current-focus.md` if priorities or risks changed
- update relevant architecture / decision / module docs
- update lessons if a durable lesson emerged

Typical targets:
- `project-memory/log.md`
- `project-memory/current-focus.md`
- `project-memory/tasks/active.md`
- `docs/architecture/system-overview.md`
- `docs/architecture/module-graph.md`
- `docs/architecture/invariants.md`
- `docs/decisions/*.md`
- `docs/modules/*.md`
- `project-memory/recent-lessons.md`

---

## Conversation → Memory Triggers

Do not wait until the very end if durable knowledge becomes clear mid-session.

When conversation reveals any of the following, consider compiling immediately or at least before session close:

- a non-obvious constraint
- a root cause
- a rejected hypothesis
- a chosen approach among alternatives
- a new invariant or boundary
- a reusable debugging pattern
- a clarified module responsibility
- a task dependency that will matter later
- a decision likely to be forgotten if left only in chat

If the insight is narrow and local, a `recent-lessons.md` or module update may be enough.
If it changes how the system should be built, record a decision or architecture update.

---

## Decision Recording Rule

Create a decision note when one of these is true:

- a source of truth changed
- module boundaries changed
- an important approach was selected over alternatives
- a previous decision was reversed
- an integration strategy was chosen
- a long-lived tradeoff was accepted
- future sessions may ask “why is it designed this way?”

Do not create a decision file for every small choice.

Decision notes belong under:
- `docs/decisions/`

Use the decision template under:
- `docs/agent/templates/decision-note.md`

---

## Lesson Recording Rule

Use lessons for pitfalls, debugging conclusions, and recurring mistakes.

A lesson should be recorded when:
- the mistake is likely to recur
- the fix reflects a broader rule, not just a one-off patch
- the root cause teaches something durable
- the lesson affects future implementation choices

Record lessons in:
- `project-memory/recent-lessons.md`

If a lesson becomes stable and long-lived, “graduate” it into:
- `docs/architecture/invariants.md`, or
- a decision note, or
- a module note

Use the lesson template under:
- `docs/agent/templates/lesson-note.md`

---

## Recent Lessons Lifecycle

`recent-lessons.md` is the **hot layer**, not the permanent archive of all history.

Each lesson should have a status such as:
- active
- cooling
- retired
- graduated

### Graduation rule
Promote a lesson when it becomes:
- an architecture invariant
- a decision rationale
- a stable module constraint

### Retirement rule
Retire or remove a lesson when:
- the codebase no longer has the relevant risk
- the lesson is obsolete
- the relevant structure was removed
- the lesson has already been promoted elsewhere and no longer needs to stay hot

Lint should help identify stale lessons.

---

## Session Notes Rule

Create a session note only when it adds future value.

Create or update a session note when:
- the work was medium or heavy
- the work crossed files/modules
- decisions were made
- lessons emerged
- there are unresolved follow-ups
- a future agent would benefit from a compact summary

Do not create a session note for trivial changes.

Session notes belong under:
- `project-memory/sessions/`

Use the session template under:
- `docs/agent/templates/session-note.md`

---

## Document Increment Rule

When raw or curated docs change:

### Added docs
- extract durable knowledge
- update affected memory/docs
- log the ingest/update

### Modified docs
- identify what changed in understanding
- keep valid conclusions
- deprecate outdated conclusions
- update affected targets only

### Deleted docs
- do not assume all related memory should be deleted
- determine whether the deleted doc was:
  - temporary and discardable, or
  - historically meaningful and should remain reflected in decisions/history
- remove stale references if needed

### Renamed docs
- preserve continuity
- do not treat a rename as unrelated delete + add unless the content truly changed

---

## Minimal Update Targets by Situation

### Bugfix with reusable lesson
Update:
- `log.md`
- `recent-lessons.md`
- related module doc if needed
- session note if medium+

### API contract change
Update:
- `log.md`
- related module docs
- possibly system overview / module graph
- decision note if the contract change reflects a lasting choice

### Architecture adjustment
Update:
- `log.md`
- current focus if priorities changed
- architecture docs
- decision note
- relevant module docs
- lessons if a new stable rule emerged

### New raw design doc
Update:
- source registry if useful
- log
- relevant architecture/module/decision docs
- current focus only if it changes actual priorities

---

## Must Not Do

- Do not preserve raw chat
- Do not over-update for tiny changes
- Do not create decisions for every local choice
- Do not create many module pages on first run
- Do not let `recent-lessons.md` become a permanent junk drawer
- Do not keep stale conclusions when code disproves them

---

## Expected Result

The repository should gradually accumulate:

- a clear project map
- a reliable current state
- a usable hot-layer lesson system
- an understandable decision history
- compact but durable session summaries

That is the meaning of continuous compilation in this repository.