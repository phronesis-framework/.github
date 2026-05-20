# Testing conventions

## Layout

```
tests/
├── conftest.py            # shared fixtures
├── unit/                  # fast, no I/O, no network
│   └── <package>/
│       └── test_<module>.py
└── integration/           # cross-component; may use containers
    └── test_<scenario>.py
```

- Tests live in `tests/`, **not** beside the source.
- One test module per source module: `src/pkg/foo.py` → `tests/unit/pkg/test_foo.py`.
- Integration tests are opt-in via the `integration` pytest marker.

## Naming

- File: `test_<module>.py`.
- Function: `test_<unit_under_test>_<scenario>_<expected_result>`.
  - Good: `test_agent_spec_rejects_missing_version`.
  - Bad: `test_agent_spec_1`.
- Async tests: `async def` — `pytest-asyncio` is in `auto` mode, no decorator required.

## Fixtures

- Shared fixtures in `tests/conftest.py`.
- Package-local fixtures in `tests/unit/<package>/conftest.py`.
- Prefer **fixture factories** over module-level constants for anything mutable.

## Coverage

- **Unit-test coverage target: 90%+ branch coverage** on the `core/` layer.
- Lower bars acceptable for `runtime/` (≥80%) and adapters (≥70%) where external systems make pure unit testing impractical.
- Coverage gates run in CI; PRs that lower coverage need an explicit waiver in the description.

## Async testing patterns

- Use `anyio.fail_after` rather than `asyncio.wait_for` when bounding test duration.
- For async generators, drain them with `async for` and explicit termination — never leak background tasks.
- Mock LLM providers with deterministic fakes; don't hit a real provider in unit tests.

## Placeholder tests

Every placeholder module gets a test that:

1. Imports the module without side effects.
2. Asserts the placeholder raises `NotImplementedError`.

```python
def test_placeholder_class_raises() -> None:
    from pkg.subpkg.module import PlaceholderClass

    with pytest.raises(NotImplementedError):
        PlaceholderClass()
```

## What not to test

- Pydantic's own validation — assume `pydantic` works.
- Standard-library behavior.
- Third-party library internals (mock them at your boundary).

## Markers

```python
import pytest

pytestmark = pytest.mark.integration  # whole module
```

Available markers (registered in `pyproject.toml`):

- `integration` — needs network/containers.
- `slow` — runtime >1 s; deselected by default in PR CI, run nightly.

## Running tests

```bash
uv run pytest                    # all tests
uv run pytest -m "not integration"  # unit only
uv run pytest --cov              # with coverage
uv run pytest tests/unit/core    # one subtree
uv run pytest -k "agent_spec"    # by keyword
```
