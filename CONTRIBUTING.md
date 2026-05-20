# Contributing to Phronesis Framework

Thanks for considering a contribution. This document applies to **every repository** in the `phronesis-framework` organization. Repo-specific addenda live in each repo's own `CONTRIBUTING.md` when they exist.

## Ground rules

1. **Read the conventions first.** See [`docs/conventions/`](docs/conventions/). They are not suggestions.
2. **Open an issue before non-trivial work.** A 10-line bug fix doesn't need one. A new feature or API change does.
3. **Conventional Commits.** Every commit message must follow the [Conventional Commits 1.0](https://www.conventionalcommits.org/) format. See [`docs/conventions/commits.md`](docs/conventions/commits.md).
4. **No code without tests.** New behavior gets new tests. Bug fixes get a regression test.
5. **CI must be green before review.** Don't ask for review on a red PR unless you explicitly want help getting it green.

## Workflow

1. **Fork** the repo and create a branch from `main`. Branch naming: `<type>/<short-description>` (e.g. `feat/agent-spec-validation`, `fix/pipeline-stage-id-collision`).
2. **Install dev dependencies.** Most repos use `uv`:
   ```bash
   uv sync --all-extras
   pre-commit install
   ```
3. **Make your change.** Keep PRs small and focused. One PR per concern.
4. **Run checks locally** before pushing:
   ```bash
   uv run ruff check
   uv run ruff format --check
   uv run pyright
   uv run pytest --cov
   ```
5. **Open a PR** against `main`. Fill out the PR template completely.
6. **Address review comments** by pushing additional commits — don't force-push during review. Squash on merge happens automatically.

## Working with Claude Code (or other AI agents)

This org treats AI-assisted development as a first-class workflow. See [`docs/guides/working-with-claude.md`](docs/guides/working-with-claude.md) and [`docs/conventions/agents.md`](docs/conventions/agents.md).

Key rules when committing agent-assisted code:

- **You** are responsible for every line you commit, regardless of who or what wrote it.
- Use the shared `.claude/commands/` and `.claude/agents/` — don't invent ad-hoc prompts that bypass the conventions.
- Sign commits with `Co-Authored-By:` when significant content was produced by an agent.

## Reporting bugs and requesting features

Use the issue forms in any repo. If the form doesn't fit, open a blank issue and explain why.

## Security

**Do not report security issues in public issues.** See [`SECURITY.md`](SECURITY.md).

## Code of conduct

Participation in this org is governed by [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).

## License

By contributing, you agree your contribution is licensed under the project's [Apache-2.0](LICENSE) license.
