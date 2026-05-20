# Commit conventions

Every commit in every org repo follows [Conventional Commits 1.0](https://www.conventionalcommits.org/).

## Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

- **Subject**: imperative mood, lowercase, no trailing period, ≤72 chars.
- **Body**: explain the *why*, not the *what*. Wrap at 100 chars. Optional but recommended for non-trivial changes.
- **Footer**: `BREAKING CHANGE:` notes, `Refs: #N`, `Co-Authored-By:` lines.

## Types

| Type | When |
|---|---|
| `feat` | New user-facing capability. |
| `fix` | Bug fix. |
| `refactor` | Internal restructuring; no behavior change. |
| `perf` | Performance improvement; no behavior change. |
| `docs` | Documentation only. |
| `test` | Tests only. |
| `build` | Build system, packaging, dependencies. |
| `ci` | CI workflows or supporting scripts. |
| `chore` | Maintenance that doesn't fit elsewhere (tooling config, gitignore, etc.). |
| `revert` | Reverts a prior commit. Include the hash in the body. |

`feat!` / `fix!` (or `BREAKING CHANGE:` footer) signal breaking changes for SemVer.

## Scopes

Pick the smallest scope that's still informative. Use what already exists in the repo's history; only introduce a new scope when one is clearly missing.

Common scopes in framework repos:

- `core`, `runtime`, `providers`, `tools`, `mcp`, `memory`, `context`, `comm`, `pipelines`, `policies`, `obs`, `api`
- `tests`, `docs`, `ci`, `deps`

Scope is optional for repo-wide changes (e.g. `chore: bump pre-commit hooks`).

## Examples

```
feat(core): add AgentSpec with frozen pydantic model

AgentSpec composes ToolSpec and MemorySpec references by ID. Frozen to
guarantee the spec is hashable and JSON-roundtrippable.

Refs: #12
```

```
fix(runtime): cancel in-flight tool invocations on agent shutdown

Previously the AgentRunner returned before tool tasks completed, leaving
HTTP connections open. Wraps tool execution in an anyio task group so
cancellation propagates.

Fixes: #34
```

```
ci: pin actions/checkout to commit SHA

Closes a supply-chain audit finding flagged by security.yml.
```

## Pre-commit enforcement

`commitizen`-style enforcement is provided by the `conventional-pre-commit` hook configured in [`.pre-commit-config.yaml`](../../.pre-commit-config.yaml). Install with `pre-commit install --hook-type commit-msg`.

## Why this matters

Conventional Commits drive:

- Automated CHANGELOG generation.
- SemVer bump detection in `release.yml`.
- Issue/PR labeling.
- Searchable history when bisecting.

Sloppy commit messages cost more downstream than they save upstream.
