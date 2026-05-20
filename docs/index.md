# Phronesis Framework — Conventions

> *Phronesis* (φρόνησις): for Aristotle, **practical wisdom** — the capacity to deliberate well and act with judgment in concrete situations. An LLM has *episteme* (knowledge). An agent needs *phronesis*.

This site documents the engineering conventions, CI/CD contracts, and agent-development workflows used across every repository in the [`phronesis-framework`](https://github.com/phronesis-framework) GitHub organization.

It exists for two audiences:

1. **Humans** — contributors who want to know how we work before opening a PR.
2. **Agents** — Claude Code and other AI coding assistants that need a fixed reference frame so they don't re-decide structure, style, or commit format on every task.

## Start here

- [What is Phronesis](concepts/phronesis.md) — the philosophical framing and design principles.
- [Python conventions](conventions/python.md) — style, types, async, errors.
- [Commit conventions](conventions/commits.md) — Conventional Commits + the scope catalog.
- [Testing conventions](conventions/testing.md) — layout, naming, fixtures, coverage.
- [Documentation conventions](conventions/docs.md) — docstrings, mkdocs, ADRs.
- [CI/CD conventions](conventions/ci.md) — reusable workflows and how to call them.
- [Agent conventions](conventions/agents.md) — how agents operate in this org.

## Guides

- [Bootstrapping a new repo](guides/new-repo.md)
- [Working with Claude Code](guides/working-with-claude.md)
