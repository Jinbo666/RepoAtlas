# Archetype Detection

## Purpose

Decide whether a repository's archetype is `code` or `docs-kb` **automatically**, without asking the user by default.

The user should not have to declare archetype manually. This page defines the heuristic the agent applies; the result is written back into `project-memory/source-roots.md` so detection runs at most once per repository.

---

## When to Run Detection

Run detection when **any** of these is true:

1. `project-memory/source-roots.md` does not exist yet (first run)
2. Its `Archetype:` field is missing, empty, or set to `auto`
3. The user explicitly asks for re-detection (e.g. "the project has changed shape, re-detect archetype")

Do **not** re-run detection if the field is already set to `code` or `docs-kb`. The stored value is authoritative. Respect user overrides.

---

## Signals

Agents should inspect the repository and gather these signals. No tooling is required — a directory listing plus a few targeted file checks is enough.

### Strong `code` signals

- Root-level package manifest of a programming ecosystem:
  `package.json`, `pyproject.toml`, `setup.py`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`, `Gemfile`, `composer.json`, `CMakeLists.txt`, `Makefile` (with code build targets), `*.csproj`, `*.sln`, `mix.exs`, `rebar.config`
- Populated code directories: `src/`, `app/`, `backend/`, `frontend/`, `lib/`, `pkg/`, `cmd/`, `internal/`, `api/` containing source files (not just readmes)
- Populated test directories: `tests/`, `test/`, `spec/`, `__tests__/`
- Presence of `docs/architecture/` or `docs/modules/` with content (means a previous `code`-archetype init happened)

### Strong `docs-kb` signals

- `docs/raw/` exists and contains substantive markdown (>= 3 files, or non-trivial size)
- Presence of `docs/topics/`, `docs/concepts/`, `docs/summaries/`, or `docs/glossary.md` with content (means a previous `docs-kb`-archetype init happened)
- Repo file tree is dominated by `.md` / `.mdx` / `.rst` / `.txt` documents; code-file count is near zero
- No root-level programming package manifest

### Weak / ambiguous signals

- A repo that has both `src/` and a large `docs/raw/`
- A repo with only a `README.md` and nothing else
- A repo whose `docs/raw/` exists but is empty

---

## Decision Rules (apply in order, first match wins)

1. **Previously-initialized repo**: If `docs/architecture/` or `docs/modules/` exist with content → `code`. If `docs/topics/` or `docs/concepts/` or `docs/summaries/` exist with content → `docs-kb`. This rule short-circuits everything else.

2. **Clear code signal**: If any strong `code` signal (package manifest or populated code/test directory) is present **and** `docs/raw/` is empty or missing → `code`.

3. **Clear docs-kb signal**: If `docs/raw/` has substantive content **and** no strong `code` signal is present → `docs-kb`.

4. **Code-dominated mixed**: If both code signals and `docs/raw/` content exist, and code files substantially outnumber raw docs, or a package manifest is present → `code`. Raw docs here are treated as source material for a code project, which is the default `code`-archetype behavior.

5. **Docs-dominated mixed**: If both exist but markdown files substantially outnumber code files **and** there is no package manifest → `docs-kb`.

6. **Fallback (ambiguous)**: Do **not** guess. Ask the user exactly once:
   > "I can't confidently auto-detect this repository's archetype. Is it a `code` project (application/engineering) or a `docs-kb` project (knowledge base / docs compilation)?"
   Then record the answer.

---

## After Detection: Write-back (self-healing)

Once a decision is made:

1. Update the top of `project-memory/source-roots.md` so the `Archetype:` field becomes `code` or `docs-kb` (replacing `auto` or the missing value).
2. Append a single entry to `project-memory/log.md` of type `archetype-detect`, noting the decided value and the one or two signals that were decisive.
3. Proceed with the task using the detected archetype.

This makes detection a one-time operation. Subsequent sessions read the stored value directly.

---

## What the User Sees

For a typical user dropping docs into `docs/raw/` and running the agent:

1. They do **nothing** — no config, no declaration.
2. First session: agent sees substantive `docs/raw/` with no code → decides `docs-kb`, writes it back, continues.
3. Later sessions: archetype is already set; detection is skipped.
4. Ambiguous cases only: agent asks once, then records.

For a `code` user: likewise, no declaration needed.

---

## Explicit Override

A user can always hard-set `Archetype:` in `source-roots.md` to any of the supported values. Manual values are respected and not re-detected.

If the user wants to trigger re-detection after a major shape change, they can either:
- set the field back to `auto`, or
- say "re-detect archetype" to the agent.

---

## Anti-patterns

- Do **not** ask the user upfront if the signals are clear. Asking is a fallback, not a default.
- Do **not** silently assume `code`. The default is `auto`, which means "decide by signals, ask only if ambiguous".
- Do **not** skip the write-back. Leaving `Archetype: auto` forces every future session to re-run detection.
- Do **not** re-detect once a concrete value is stored. Respect it.
