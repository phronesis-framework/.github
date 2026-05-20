# `.github` — Phronesis Framework org configuration

> *Phronesis* (φρόνησις): for Aristotle, **practical wisdom** — the capacity to deliberate well and act with judgment in concrete situations. An LLM has *episteme* (knowledge). An agent needs *phronesis*.

This repository is the **organization-level `.github` repo** for [`phronesis-framework`](https://github.com/phronesis-framework). It holds the shared community-health files, default policies, reusable CI/CD workflows, documentation skeleton, and **agent-development conventions** that every repo in the org inherits or copies.

It does **not** contain framework source code. The framework itself lives in [`phronesis-framework/phronesis-framework`](https://github.com/phronesis-framework/phronesis-framework).

## What's in here

| Path | Purpose |
|---|---|
| `profile/README.md` | Rendered as the public org landing page on github.com/phronesis-framework |
| `.github/workflows/` | Reusable workflows downstream repos call via `workflow_call` |
| `.github/ISSUE_TEMPLATE/` | Default issue forms for any org repo without its own |
| `PULL_REQUEST_TEMPLATE.md` | Default PR template |
| `CODEOWNERS` | Default code-ownership rules |
| `dependabot.yml` | Default Dependabot config |
| `.claude/commands/` | Slash-command prompts for Claude Code (shared across repos) |
| `.claude/agents/` | Sub-agent definitions for Claude Code |
| `pyproject.toml` | Canonical `[tool.ruff]`, `[tool.pyright]`, `[tool.pytest]`, `[tool.coverage]` config |
| `.pre-commit-config.yaml` | Canonical pre-commit hooks |
| `docs/conventions/` | Org-wide engineering conventions (Python, commits, testing, docs, CI) |
| `docs/guides/working-with-claude.md` | How to develop in this org with Claude Code |

## Why this exists

The point of this repo is to make every new repo in the org start from a **single, opinionated baseline** so that:

1. CI/CD, security scans, release flow, and dependency review are identical across repos.
2. Conventions for Python, commits, testing, and docs are codified — not folklore.
3. Claude Code (and other agents) have a **fixed reference frame** to work from. No re-deciding style, structure, or commit format on every task.

## How downstream repos use this

- **Issue/PR templates and CODEOWNERS** apply automatically to any repo in the org that doesn't define its own.
- **Reusable workflows** are invoked from a downstream repo with:
  ```yaml
  jobs:
    ci:
      uses: phronesis-framework/.github/.github/workflows/ci-python.yml@main
  ```
- **Tooling config** (`pyproject.toml`, `.pre-commit-config.yaml`) is copied into each repo and kept in sync via Dependabot or manual updates.
- **`.claude/` directory** is copied into each repo so Claude Code finds the same commands and sub-agents everywhere.

## Conventions index

See [`docs/conventions/`](docs/conventions/) for:

- `python.md` — Python style, type hints, async, error handling
- `commits.md` — Conventional Commits + commit-scope catalog
- `testing.md` — Test layout, naming, async tests, fixtures, coverage targets
- `docs.md` — Docstring style, mkdocs structure, ADRs
- `ci.md` — Workflow contracts and how to call reusable workflows
- `agents.md` — How agents (Claude Code, etc.) should operate in this org

## License

Apache-2.0. See [`LICENSE`](LICENSE).
