# Lint and Health

## Purpose

This file defines how to check whether the repository's documentation and memory layers are still healthy.

The goal is to control drift across:

- code and tests
- curated docs under `docs/`
- dynamic memory under `project-memory/`

Lint is not about style only.
It is about **truth maintenance**.

---

## When to Run Lint

Run or suggest a lint pass when one of these is true:

- after a heavy change
- after a medium change that touched architecture, decisions, or lessons
- when the user explicitly asks
- when memory and code seem inconsistent
- when tasks appear stale
- when repeated mistakes accumulate
- when recent lessons seem outdated
- when doc structure feels bloated or contradictory

Do not run full lint after every tiny change.

---

## Lint Scope

A lint pass may check some or all of the following:

### A. Task health
- Are active tasks still active?
- Are done tasks still sitting in `active.md`?
- Are backlog items duplicated elsewhere?
- Does current focus still match current work?

### B. Architecture health
- Does `system-overview.md` still match actual code structure?
- Does `module-graph.md` reflect current dependency directions?
- Do invariants still make sense?
- Was a source-of-truth change made without updating architecture docs?

### C. Decision health
- Are there important changes with no decision note?
- Do old decision notes conflict with current architecture?
- Are deprecated decisions marked clearly?
- Are follow-ups still unresolved without being tracked?

### D. Lesson health
- Are recent lessons still relevant?
- Has a lesson been fixed and should now cool down or retire?
- Should a hot lesson graduate into an invariant, decision, or module doc?
- Are lessons duplicated across files?

### E. Module doc health
- Are important modules undocumented?
- Are module responsibilities outdated?
- Do module docs claim behavior the code no longer has?
- Are boundaries or dependencies wrong?

### F. Memory/log health
- Is `current-focus.md` stale?
- Is `log.md` capturing meaningful changes?
- Are session notes useful, or just noise?
- Are there too many stale scratch notes?

### G. Raw-doc integration health
- Are important raw docs unregistered?
- Are curated docs missing key conclusions from raw docs?
- Are raw docs being mistaken for polished final truth?

---

## Lint Severity

### 1. Info
Minor inconsistency or cleanup suggestion.
Example:
- a missing cross-link
- a task that should probably move to done

### 2. Warning
Likely drift or outdated documentation.
Example:
- current focus no longer reflects actual work
- a lesson remains active but the code no longer has the same risk

### 3. Critical
Documentation/memory now materially misleads future work.
Example:
- system overview contradicts actual architecture
- source of truth is wrong in docs
- stale decision notes actively point work in the wrong direction

---

## Lint Output

A lint pass should produce:

### 1. A log entry
Append one entry to:
- `project-memory/log.md`

Type:
- `lint`

### 2. A concise findings summary
Include:
- what was checked
- what was healthy
- what drift was found
- what was fixed immediately
- what still needs follow-up

### 3. Direct fixes when safe
Safe fixes may include:
- moving tasks between active/backlog/done
- correcting small stale references
- updating a status field
- removing obvious duplication
- cooling down or retiring an outdated lesson

### 4. Follow-up notes when not safe
If a fix requires interpretation or code inspection beyond confidence, record follow-up work in:
- `project-memory/current-focus.md`
- `project-memory/tasks/active.md`

---

## Suggested Lint Procedure

### Step 1: Read state
Read:
- `project-memory/current-focus.md`
- `project-memory/tasks/active.md`
- `project-memory/recent-lessons.md`
- recent `log.md` entries
- relevant architecture/decision/module docs

### Step 2: Compare with current reality
Inspect:
- affected code
- tests
- configs
- recently changed files

### Step 3: Detect drift
Look for:
- stale claims
- contradictions
- orphan docs
- missing docs
- duplicated knowledge
- hot lessons that should graduate or retire

### Step 4: Repair safely
Fix what is obvious and low-risk.

### Step 5: Record unresolved issues
If uncertainty remains, record:
- what is wrong
- what likely needs attention
- what evidence is missing

---

## Specific Checks

### Task checks
- Is every active task still active?
- Does every active task have a next action?
- Are completed tasks removed from active?
- Does current focus reflect the same priorities as active tasks?

### Lesson checks
For each recent lesson ask:
- Is this still an active risk?
- Was the root cause actually confirmed?
- Was the codebase changed to prevent recurrence?
- Should this lesson be cooled, retired, or graduated?

### Decision checks
For each relevant recent heavy change ask:
- Was a long-term choice made?
- If yes, is there a decision note?
- If a prior choice was reversed, is that recorded?

### Architecture checks
- Does system overview still describe the current shape?
- Do module relationships still hold?
- Did any integration point move or change?
- Are invariants still consistent with the codebase?

### Module checks
- Are important modules missing notes?
- Do module docs still describe real responsibilities?
- Are non-responsibilities still correct?

---

## What “Healthy” Looks Like

A healthy repository has:

- current focus that matches actual work
- active tasks that are actually active
- lessons that are hot only while needed
- architecture docs that still reflect current code
- decisions for durable choices
- no large contradictions between memory and code

Perfect completeness is not required.
Low drift and clear navigation are the target.

---

## Must Not Do

- Do not lint the entire repository for every tiny change
- Do not create work just to satisfy documentation formalism
- Do not preserve stale notes for nostalgia
- Do not keep a lesson active just because it once mattered
- Do not let docs become more authoritative than code

---

## Result

Lint should reduce entropy.

It should make future sessions:
- faster
- safer
- less repetitive
- less likely to repeat known mistakes