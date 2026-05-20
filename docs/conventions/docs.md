# Documentation conventions

## Docstrings

- **Google style.** Enforced via `ruff` (`pydocstyle`).
- **Every public module, class, and function** has a docstring.
- **Summary line in imperative mood**, ≤ 80 chars, no trailing period if a single fragment.
- **Sections**: `Args`, `Returns`, `Raises`, `Yields`, `Example` — only the ones that apply.

```python
def compact_context(messages: list[Message], max_tokens: int) -> list[Message]:
    """Compact a message list to fit a token budget.

    Drops or summarizes older messages until the total estimated token count
    is at or below ``max_tokens``. The system message (if any) is always kept.

    Args:
        messages: Ordered list of messages, oldest first.
        max_tokens: Token budget (must be positive).

    Returns:
        A new list of messages within the budget. Never mutates the input.

    Raises:
        ValueError: If ``max_tokens`` is not positive.
    """
```

## Repository docs

Each repo's `docs/` should follow this layout:

```
docs/
├── index.md
├── concepts/          # the "what" and "why" (no code)
├── guides/            # task-oriented tutorials
├── reference/         # auto-generated API reference via mkdocstrings
└── adr/               # Architecture Decision Records (optional)
```

## mkdocs

- `mkdocs-material` theme.
- `mkdocstrings[python]` plugin for API reference.
- Build with `uv run mkdocs build --strict` in CI — warnings fail the build.
- Deploy to GitHub Pages from `main` via `docs.yml` workflow.

## Architecture Decision Records (ADRs)

When a non-trivial design choice is made, record it as an ADR:

```
docs/adr/0001-pydantic-v2-frozen-specs.md
```

Template:

```markdown
# ADR 0001: Pydantic v2 frozen specs

## Status
Accepted — 2025-05-20

## Context
What problem are we solving? What constraints apply?

## Decision
What did we decide?

## Consequences
What follows from this — good, bad, and neutral?

## Alternatives considered
What did we reject, and why?
```

Number sequentially. Once an ADR is `Accepted`, edits append `## Update YYYY-MM-DD` sections rather than rewriting history.

## Code examples in docs

- All code examples must be syntactically valid Python.
- Prefer examples that import only from the documented module — no implicit setup.
- Long examples live in `examples/` and are referenced from docs, not pasted inline.
