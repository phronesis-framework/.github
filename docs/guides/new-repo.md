# Bootstrapping a new repo in the org

Follow this when starting a fresh repository under the `phronesis-framework` org.

## 1. Create the repo

- Use the GitHub UI or `gh repo create phronesis-framework/<name>`.
- Initialize with `main` as the default branch.
- Apply standard branch protection: required PR review, required status checks (CI green), no force push to `main`.

## 2. Pull in the org defaults

The community-health files (issue/PR templates, `CODEOWNERS`, `dependabot.yml`, `SECURITY.md`, etc.) apply automatically from this `.github` repo. You do not need to copy them unless your repo needs a local override.

Copy explicitly into the new repo:

```bash
# from the new repo root
curl -L https://raw.githubusercontent.com/phronesis-framework/.github/main/pyproject.toml -o pyproject.toml
curl -L https://raw.githubusercontent.com/phronesis-framework/.github/main/.pre-commit-config.yaml -o .pre-commit-config.yaml
curl -L https://raw.githubusercontent.com/phronesis-framework/.github/main/.gitignore -o .gitignore
curl -L https://raw.githubusercontent.com/phronesis-framework/.github/main/.python-version -o .python-version
```

Then add the `[project]` block to `pyproject.toml` for your package metadata. The `[tool.*]` sections inherited from the org config are correct as-is.

Also copy `.claude/`:

```bash
mkdir -p .claude
curl -L https://raw.githubusercontent.com/phronesis-framework/.github/main/.claude/commands/ -o .claude/commands/  # or git sparse-checkout
```

(A future improvement: a `gh phronesis bootstrap <name>` extension that does all of this.)

## 3. Wire the reusable workflows

Create `.github/workflows/ci.yml` in the new repo:

```yaml
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
    secrets: inherit
```

Repeat for `security.yml`, `docs.yml`, `release.yml`, `dependency-review.yml` as needed.

## 4. Initial commits

Follow the [commit conventions](../conventions/commits.md). Suggested first commits:

1. `chore: pull in org-wide tooling configuration`
2. `chore: wire reusable CI/CD workflows from .github org repo`
3. `feat: initial package skeleton`

## 5. Branch protection checklist

- Require PR reviews (at least 1).
- Require status checks: `ci / lint`, `ci / type-check`, `ci / test`, `dependency-review`.
- Block force pushes to `main`.
- Restrict who can push to `main` (CODEOWNERS or the maintainers team).
- Require signed commits if your contributor base supports it.

## 6. Open the welcome issue

Open issue #1 with a roadmap or "What's in this repo" overview. This becomes the long-running pinned thread.
