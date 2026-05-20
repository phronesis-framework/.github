---
description: Generate tests for changed code following the org testing conventions.
allowed-tools: Bash(git diff:*), Bash(git status:*), Read, Glob, Grep, Write, Edit
---

# /test

Generate or update tests for the code described below, following [testing conventions](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/testing.md).

Target: $ARGUMENTS  (file path, module, or description; if omitted, infer from current `git diff`)

## Procedure

1. Identify the code under test:
   - If `$ARGUMENTS` is a file path, read it.
   - Otherwise read `git diff` (staged + unstaged) and infer the changed modules.
2. Locate or create the matching test file: `src/pkg/foo.py` → `tests/unit/pkg/test_foo.py`.
3. Read any existing tests to match the repo's style.

## Rules

- **One test module per source module.**
- **Naming**: `test_<unit>_<scenario>_<expected_result>`. No `test_thing_1` / `test_thing_2`.
- **Async tests** are plain `async def`. `pytest-asyncio` is in `auto` mode.
- **Use `anyio.fail_after`** for bounded async tests (not `asyncio.wait_for`).
- **Mock at boundaries.** Don't mock the code under test. Don't hit real LLM providers in unit tests.
- **One assertion concept per test.** Multiple `assert`s on the same concept are fine; chasing many concepts in one test is not.
- **Placeholder pattern**: for a `NotImplementedError` placeholder, add a single test that imports cleanly and asserts the error.
- **Fixtures** factor shared setup. Put repo-wide fixtures in `tests/conftest.py`; package-local in `tests/unit/<pkg>/conftest.py`.
- **Do not** lower coverage. If a branch can't be hit, add a `# pragma: no cover` with a one-line reason.

## Output

1. List the test file(s) you will create or modify.
2. Show the diff.
3. Stop before running tests. The human runs `uv run pytest` to verify.
