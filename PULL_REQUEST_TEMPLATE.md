<!-- Default PR template for the phronesis-framework org. -->

## Summary

<!-- One paragraph. What does this PR do and why? Link issues with "Fixes #N" / "Refs #N". -->

## Changes

<!-- Bullet list of the concrete changes. -->

- ...

## Test plan

<!-- How did you verify this? Check off as you go. -->

- [ ] `uv run ruff check` — clean.
- [ ] `uv run ruff format --check` — clean.
- [ ] `uv run pyright` — strict mode passes.
- [ ] `uv run pytest --cov` — green, coverage not lowered.
- [ ] `uv run mkdocs build --strict` (if docs changed) — clean.

## Conventions checklist

<!-- See https://github.com/phronesis-framework/.github/tree/main/docs/conventions -->

- [ ] Commits follow [Conventional Commits](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/commits.md).
- [ ] Python style matches [python.md](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/python.md).
- [ ] Tests follow [testing.md](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/testing.md).
- [ ] Docs updated if public API or conventions changed.
- [ ] No new dependencies (or: justified in the description).

## Breaking changes

<!-- If yes, describe migration. Mark the PR / commit with `!` per Conventional Commits. -->

- [ ] None.

## Agent attribution

<!-- If significant content was produced by an AI agent, include a Co-Authored-By footer in your commits. -->

- [ ] Not applicable.
- [ ] Co-authored with: `Claude (claude-opus-4-7)` / other (specify).
