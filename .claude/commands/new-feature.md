---
description: Scaffold a new feature with module(s), tests, and docs in one pass.
---

# /new-feature

Scaffold a new feature inside the current Python package, following all org conventions.

Feature description: $ARGUMENTS

## Stages

You must complete these stages in order. **Stop after each and wait for confirmation.**

### Stage 1 — Plan

Produce a `/plan`-style output:

- Goal, non-goals, files, steps, risks, open questions.
- Identify which conventions apply (link them).
- Pause for human approval.

### Stage 2 — Spec / interface

Write the **public interface only**:

- Module docstring (Google style).
- Class / function signatures with full type hints.
- Docstrings on every public symbol.
- `raise NotImplementedError(...)` bodies — no logic yet.

Pause again. The human reviews the shape before any logic is written.

### Stage 3 — Implementation

Fill in the logic. Constraints:

- No new dependencies unless approved in Stage 1.
- No silent error handling — raise from the package's exception hierarchy.
- Async-first: public entrypoints are `async def`.
- Pydantic v2 for any spec types; `frozen=True, extra="forbid"`.

### Stage 4 — Tests

Generate tests per [`docs/conventions/testing.md`](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/testing.md):

- One test module per source module.
- Cover happy path + at least two edge cases.
- Async tests bounded with `anyio.fail_after`.

Run `uv run pytest` (or ask the human to) and ensure green.

### Stage 5 — Docs

- Add or update a concept page under `docs/concepts/` if the feature introduces a new mental model.
- Add or update a guide under `docs/guides/` if it changes user workflow.
- Update the API reference if applicable.

### Stage 6 — Commit(s)

Split into logical commits — typically: `feat(<scope>): add <feature> spec`, `feat(<scope>): implement <feature>`, `test(<scope>): cover <feature>`, `docs(<scope>): document <feature>`.

Use `/commit` for each.

## Rules

- Never silently skip a stage. If a stage is N/A for this feature, say so and continue.
- Conventions override agent instincts. If they conflict, **ask**.
