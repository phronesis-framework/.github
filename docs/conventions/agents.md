# Agent conventions

How AI coding agents (Claude Code, Cursor, Copilot, etc.) operate in this org. These rules apply to anyone using an agent to produce code, docs, or workflows.

## Operating principles

1. **The human commits, the human owns.** Whoever runs `git commit` is responsible for the content regardless of who or what authored it.
2. **Use the shared toolkit.** Slash commands in [`.claude/commands/`](../../.claude/commands/) and sub-agents in [`.claude/agents/`](../../.claude/agents/) are the canonical entry points. Don't invent ad-hoc prompts that bypass them.
3. **Conventions over preferences.** When the agent's instinct conflicts with [`docs/conventions/`](.), conventions win.
4. **Ask before deciding.** Library choices, architectural pivots, new abstractions — the agent must propose, not act. See the BOOTSTRAP-style "what to ask before doing" pattern.
5. **No silent deviation.** If the agent finds a contradiction in the conventions, it asks.

## Required attribution

When a significant portion of a commit was produced by an agent, include a `Co-Authored-By:` footer:

```
Co-Authored-By: Claude (claude-opus-4-7) <noreply@anthropic.com>
```

"Significant" is judgment. Trivial completions (single-line refactors, format-only diffs) don't need it. Whole new functions or files do.

## Forbidden actions

Agents must **not**:

- Run destructive git commands (`push --force`, `reset --hard`, `clean -f`, `branch -D`) without explicit human direction.
- Skip git hooks (`--no-verify`, `--no-gpg-sign`) without explicit human direction.
- Commit secrets or files in `.gitignore`.
- Add dependencies without proposing them first.
- Edit `.github/workflows/` in this org-level repo without an issue tracking the reason.
- Touch `CODEOWNERS`, `SECURITY.md`, `LICENSE` without explicit human direction.

## Action SHA pinning — current status

Workflows in this repo are currently pinned by **tag** (e.g. `actions/checkout@v4`), with a `TODO(pin-by-sha)` note. The org-wide migration to SHA pinning will:

1. Resolve the current SHA for every `uses:` entry.
2. Rewrite each line as `actions/checkout@<sha>  # v4.1.7`.
3. Track future updates via Dependabot's `package-ecosystem: github-actions`.

Until that migration completes, agents should preserve the tag pin and the TODO comment.

## Working with sub-agents

The `.claude/agents/` directory defines named sub-agents (e.g. `planner`, `reviewer`, `test-writer`). To stay within conventions:

- **Don't fork these definitions per repo.** If a repo needs different behavior, change the *prompt input*, not the agent definition.
- **Propose changes to a shared agent via PR to this repo.** Same review bar as code.

## Debugging an agent

When an agent goes off the rails:

1. Stop the run.
2. Capture the prompt and the off-conventions output.
3. Open an issue in this repo with the `area:agents` label.
4. If a convention was ambiguous, the fix is a docs PR — not a one-off prompt patch.
