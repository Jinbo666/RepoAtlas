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
   Structured long-lived docs under `docs/`. Exact shape depends on archetype (see below).

3. **Dynamic Project Memory**  
   Working memory under `project-memory/` for current focus, logs, tasks, recent lessons, and session history.

---

## Archetype

Before generating scaffolding, determine the **project archetype**. Two values are supported:

- `code` — application / engineering project. Code and tests are primary source of truth. Curated layer = architecture / modules / decisions.
- `docs-kb` — knowledge base / docs compilation project. Raw docs in `docs/raw/` are primary source of truth. Curated layer = topics / concepts / glossary / summaries.

### How to determine archetype

Do **not** ask the user upfront. Follow the automated rubric:

1. Apply the decision rules in [`docs/agent/archetypes/detection.md`](archetypes/detection.md) — signal scan + first-match wins.
2. If the rubric returns a clear answer, use it.
3. Only if the rubric explicitly falls through to "ambiguous", ask the user once.

Then record the chosen archetype in the "Archetype" section of `project-memory/source-roots.md` during step 3 (replacing `auto` with the concrete value), and append one `archetype-detect` entry in `project-memory/log.md` noting which signals were decisive. The rest of this file then branches by archetype where indicated.

If the result is `docs-kb`, also read `docs/agent/archetypes/docs-kb.md` before continuing — it is authoritative for archetype-specific shape.

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
These are working-memory files under `project-memory/`.

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
- `project-memory/`
- `project-memory/tasks/`
- `project-memory/sessions/`

Do not create unnecessary files beyond what is useful for initialization.

### 3. Initialize source roots
Create or update:

- `project-memory/source-roots.md`

This file must record:
- code roots
- raw source roots
- curated docs roots
- dynamic memory roots
- the role of each root

This becomes the repository's root map for future incremental compilation.

### 4. Initialize a thin project map
Create or update these files with concise first-pass content:

- `project-memory/index.md`
- `project-memory/current-focus.md`
- `project-memory/log.md`
- `project-memory/tasks/active.md`
- `project-memory/tasks/backlog.md`
- `project-memory/tasks/done.md`
- `project-memory/source-registry.md`
- `project-memory/recent-lessons.md`

Rules:
- keep them thin
- prefer clarity over completeness
- do not invent details
- mark uncertainty explicitly

### 5. Initialize curated core docs

Branches by archetype.

#### 5a. `code` archetype
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

#### 5b. `docs-kb` archetype
Do **not** create `docs/architecture/` or `docs/modules/`. Instead create:

- `docs/topics/README.md` — topic map; list the major topics the corpus covers and how they relate
- `docs/concepts/README.md` — index of key concept cards (cards themselves are created lazily during ingestion)
- `docs/glossary.md` — term → one-line definition
- `docs/summaries/README.md` — index of per-raw-doc compressed summaries (individual summaries created during §7 ingestion)

The first pass should identify:
- what the knowledge base is about
- major topics / strands
- obvious key terms
- unknowns that need confirmation

Keep each page thin. Do not pre-fill concept cards or per-doc summaries — those are produced in §7.

### 6. Initialize doc scaffolding

Both archetypes:
- `docs/decisions/README.md`
- `docs/agent/index.md`
- `docs/agent/context-loading.md`
- `docs/agent/memory-update-policy.md`
- `docs/agent/lint-and-health.md`

`code` archetype only:
- `docs/modules/README.md`

`docs-kb` archetype only:
- `docs/agent/archetypes/docs-kb.md` (ensure present; this repo ships it)
- reuse of `docs/decisions/README.md` but framed for editorial / structural decisions

Keep these lightweight.
Do not overfill them on first run.

### 7. Register and compile existing raw documents

Under `code` archetype this step is a side workflow (only run when raw/legacy docs exist).

Under `docs-kb` archetype this step is **the main work of initialization** — most of the first-run effort goes here.

#### 7a. Register
- leave them in place
- classify them as raw source material
- add them to `source-roots.md` or `source-registry.md` as appropriate

#### 7b. First-pass compilation

##### `code` archetype
For each registered raw document that contains durable engineering value:

1. read the document
2. extract key knowledge: architecture insights, constraints, decisions, pitfalls, module boundaries
3. compile findings into the appropriate targets:
   - architecture docs if the doc reveals system shape or invariants
   - decision notes if the doc records a durable choice
   - module notes if the doc clarifies responsibilities or boundaries
   - `recent-lessons.md` if the doc contains pitfall/debugging knowledge
   - `current-focus.md` if the doc changes priorities or risks
4. update `source-registry.md` with status `ingested` and a brief note
5. append a log entry of type `ingest`

##### `docs-kb` archetype
For each registered raw document:

1. read the document
2. write a compressed summary at `docs/summaries/<slug>.md` — what the doc is, key takeaways, what it contradicts or supersedes, pointers to the concepts / topics it feeds. Every ingested raw doc must have a summary, even if short.
3. extract durable concepts:
   - add or update `docs/concepts/<concept>.md` cards
   - add non-obvious terms to `docs/glossary.md`
   - update `docs/topics/README.md` if a new topic emerged or structure shifted
4. update `source-registry.md` with status `ingested` (or `skipped` / `partial` / `pending` as appropriate) and a brief note of what was extracted
5. append a log entry of type `ingest`
6. if two raw docs conflict, create a decision note in `docs/decisions/` recording which is treated as authoritative

Rules (both archetypes):
- do not rewrite the raw document itself
- under `code`: do not create a curated page per raw document by default — extract knowledge into existing structure
- under `docs-kb`: do create a summary per ingested raw doc (that is the traceable landing point); concept cards, on the other hand, are created only for durable reusable concepts, not per-doc
- if a raw doc has no durable value, mark it `skipped` in the registry
- prefer thin first-pass extraction; depth can be added in later sessions
- if the number of raw docs is large, prioritize the most relevant ones and mark the rest `pending`

If existing docs are already structured and current, they may remain where they are or be referenced from curated docs.

### 8. Write a bootstrap log entry
Append one entry to:

- `project-memory/log.md`

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
- a clear `source-roots.md` (with archetype declared at the top)
- archetype-appropriate curated entry:
  - `code`: a usable `system-overview.md` + first-pass `module-graph.md`
  - `docs-kb`: a usable `docs/topics/README.md` + seeded `docs/glossary.md` + per-raw-doc summaries in `docs/summaries/`
- a thin `current-focus.md`
- a minimal task scaffold
- a `source-registry.md` with every raw doc accounted for (especially under `docs-kb`)
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
- read `project-memory/current-focus.md`
- read relevant architecture / decision / module docs
- update memory incrementally after meaningful work

This file should not be the default read for every session.
It is primarily for initialization or major re-bootstrap of a repository.