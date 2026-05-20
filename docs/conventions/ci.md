# CI/CD conventions

All reusable workflows live in this repo under [`.github/workflows/`](../../.github/workflows/) and are called from downstream repos via `workflow_call`.

## Contract for every workflow

- **Explicit `permissions:`** on every job — never rely on the default token scope.
- **Pinned actions.** Eventually by commit SHA with a `# vX.Y.Z` trailing comment. For now we pin by tag with a `TODO(pin-by-sha)` note (see `docs/conventions/agents.md`).
- **Concurrency** with `cancel-in-progress: true` on PR triggers.
- **No `pull_request_target`** unless strictly necessary for forks; document the reason in a YAML comment when used.
- **Secrets** are passed explicitly (`secrets: inherit` is acceptable for trusted callers; otherwise enumerate).

## Reusable workflows in this repo

| File | Purpose | Trigger contract |
|---|---|---|
| `ci-python.yml` | Lint, type-check, test, coverage, matrix on 3.11/3.12/3.13 | `workflow_call` from downstream `pull_request` + `push` |
| `security.yml` | CodeQL, `pip-audit`, gitleaks | `workflow_call` from downstream `push` + schedule |
| `docs.yml` | `mkdocs build --strict`; deploy to Pages on `main` | `workflow_call`; deploys when called from `main` |
| `release.yml` | Build wheels/sdist, OIDC publish to PyPI, sigstore-sign artifacts, GH Release | `workflow_call` on tag push `v*.*.*` |
| `dependency-review.yml` | Block PRs introducing vulnerable/banned deps | `workflow_call` from `pull_request` |
| `labeler.yml` | Path-based PR labels | `workflow_call` from `pull_request_target` |

## How to call from a downstream repo

```yaml
# .github/workflows/ci.yml in any downstream repo
name: ci
on:
  pull_request:
  push:
    branches: [main]

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

permissions:
  contents: read

jobs:
  ci:
    uses: phronesis-framework/.github/.github/workflows/ci-python.yml@main
    with:
      python-versions: '["3.11", "3.12", "3.13"]'
    secrets: inherit
```

## Versioning the workflows

- During alpha (org-wide), downstream repos pin to `@main`.
- Once stable, this repo will cut tags `workflows-vX.Y.Z` and downstreams pin to those.

## Adding a new reusable workflow

1. Add the workflow file under `.github/workflows/`.
2. Set `on: workflow_call:` with explicit `inputs:` and `secrets:`.
3. Document it in this file (the table above).
4. Update `CHANGELOG.md` under `[Unreleased]`.

## Local validation

```bash
# Optional: install actionlint to catch workflow errors before pushing.
actionlint .github/workflows/*.yml
```
