# Changelog

All notable changes to the **org-level `.github`** repository are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html) for any tagged releases of shared workflows.

## [Unreleased]

### Added
- `pyproject.toml` with shared ruff, pyright, pytest, and coverage configuration.
- `.pre-commit-config.yaml` with ruff, pyright, gitleaks, and conventional-commits hooks.
- `.gitignore`, `.python-version` defaults.
- `LICENSE` (Apache-2.0).
- Org `profile/README.md` rendered on the org landing page.
- Root `README.md` describing the purpose of this repo.
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `SUPPORT.md`.
- `docs/` skeleton with `conventions/`, `guides/`, `concepts/`.
- `mkdocs.yml` for the conventions site.
- Reusable workflows: `ci-python`, `security`, `docs`, `release`, `dependency-review`, `labeler`.
- `dependabot.yml`, `labeler.yml`, `release.yml` (release-notes config).
- `CODEOWNERS`, `PULL_REQUEST_TEMPLATE.md`, `ISSUE_TEMPLATE/`.
- `.claude/commands/` slash-command prompts.
- `.claude/agents/` sub-agent definitions.

[Unreleased]: https://github.com/phronesis-framework/.github/commits/main
