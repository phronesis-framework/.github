# Python conventions

These rules apply to every Python repository in the org.

## Versions

- **Runtime support**: 3.11, 3.12, 3.13.
- **Local default**: 3.12 (see `.python-version`).
- **No 3.10-or-earlier compatibility code.**

## Style

- **Formatter + linter**: `ruff` (config in [`pyproject.toml`](../../pyproject.toml)).
- **Line length**: 100.
- **Import order**: ruff isort, `phronesis*` is first-party.
- **Quotes**: double quotes.
- **Docstrings**: Google convention.

Run before committing:

```bash
uv run ruff check --fix
uv run ruff format
```

## Type hints

- **Type hints everywhere**, including return types on `__init__`.
- `from __future__ import annotations` at the top of every module.
- **Pyright strict mode** is the type-checker contract.
- **No `Any` without a one-line justification comment.** `# noqa: ANN401  reason: …` if necessary.
- **Identifiers are typed.** Use `NewType` or branded types for IDs, not bare `str`.
- **Generics are concrete.** No bare `list` / `dict` in annotations; use `list[X]` / `dict[K, V]`.

## Async

- **Async-first.** Public runtime entrypoints are `async def`.
- **No hidden sync facades** that secretly block.
- Use `anyio` primitives where possible; avoid mixing `asyncio` and `trio`-specific APIs.

## Errors

- One exception hierarchy per package, rooted at `<package>.errors.<Package>Error`.
- Specific subclasses per failure mode. No raising bare `Exception`.
- Errors are part of the public contract — document what each function can raise.

## Pydantic

- **Pydantic v2** only. `BaseModel`, not `dataclass`, for anything that crosses a boundary.
- **Specs are frozen.** `model_config = ConfigDict(frozen=True, extra="forbid", validate_assignment=True)`.
- **Every spec carries `version: str`** for forward compatibility.
- **JSON roundtrip is mandatory** for core spec types: serialize → deserialize must equal the original.

## Module conventions

- **Every public module, class, and function has a docstring.** Google style.
- **Module docstring explains *purpose*,** not contents. The contents are self-evident from the code.
- **`__all__`** in modules that are imported with `from … import *` (rare; usually avoid).
- **One concept per module.** Splitting a 200-line module is cheap; untangling a 2,000-line one is not.

## Placeholder pattern

For modules that are scaffolded but not implemented yet:

```python
"""Module purpose in one sentence."""

from __future__ import annotations

# TODO(phronesis): Implementation pending. See ROADMAP.md or issue #N.


class PlaceholderClass:
    """Brief description of what this will be.

    This is a scaffolding placeholder; implementation tracked in issue #N.
    """

    def __init__(self) -> None:
        raise NotImplementedError(
            "PlaceholderClass is not yet implemented. "
            "See https://github.com/phronesis-framework/<repo>/issues/N",
        )
```

Every placeholder gets a test that imports it cleanly and asserts the `NotImplementedError`.
