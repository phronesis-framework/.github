# Working with Claude Code

This guide is the operating manual for using Claude Code productively across `phronesis-framework` repos without drifting from conventions.

## The setup

Each repo that uses Claude Code should have:

- A copy of (or symlink to) `.claude/commands/` and `.claude/agents/` from this org repo.
- A green `pre-commit install`.
- The org [conventions](../conventions/python.md) read at least once.

## The loop

1. **State the goal.** One sentence. What's the user-visible change?
2. **Let Claude propose a plan** (use `/plan` if installed; otherwise just ask). Do not let it start writing code until you've read the plan.
3. **Constrain scope.** Reference the relevant convention page in your prompt. Example: "Stick to `docs/conventions/python.md`. No `Any`. No new deps."
4. **Edit, don't accept blindly.** Read the diff. If it touched something out of scope, push back.
5. **Run the checks locally** (`ruff`, `pyright`, `pytest`) before committing.
6. **Commit yourself** using `/commit` or by hand. Add `Co-Authored-By:` for substantial agent work.

## Slash commands

Shared commands live in [`.claude/commands/`](../../.claude/commands/). They're plain markdown prompts. Inspect them before running:

- `/commit` — analyze staged changes and write a Conventional Commit.
- `/plan` — produce an implementation plan with file-level granularity.
- `/review-pr` — review a PR against org conventions.
- `/test` — generate tests for changed code following [testing conventions](../conventions/testing.md).
- `/new-feature` — scaffold a new feature, including module + tests + docs.

To add or change a command, open a PR against this repo so the change is shared.

## Sub-agents

Defined in [`.claude/agents/`](../../.claude/agents/). They're prompts loaded as `Task` agents. Each has a single responsibility:

- `planner` — designs implementation, never writes code.
- `reviewer` — code review against org conventions.
- `test-writer` — writes pytest tests, including async + placeholder patterns.
- `doc-writer` — writes Google-style docstrings and mkdocs pages.

Same rule as for commands: change them in this repo, not per-repo.

## When to push back

You should override the agent (or stop and rewrite the prompt) when it:

- Adds a dependency you didn't approve.
- Invents a new abstraction not requested.
- Uses `Any`, swallows exceptions, or weakens types.
- Writes a commit message that's not Conventional Commits.
- Touches `LICENSE`, `CODEOWNERS`, `SECURITY.md`, or workflows in this repo without explicit instruction.
- Suggests a refactor outside the scope of the current task.

## Asking the agent good questions

Cheap, repeatable phrasing that gets you better output:

- "Reference [`docs/conventions/python.md`](../conventions/python.md) and stick to it."
- "Propose a plan first. Don't write code until I confirm."
- "List the files you intend to touch and the rough size of each diff."
- "Show me which conventions this could violate, then propose a way to avoid that."
- "Compare two approaches: A and B. Trade-offs in 5 bullets each. Recommend one."

## Common failure modes

| Symptom | Fix |
|---|---|
| Agent invents a library | Add "no new deps" to prompt; lock with `uv lock --check`. |
| Diff sprawls beyond the task | Stop. Reduce scope explicitly: "Only touch `src/pkg/foo.py` and its test." |
| Type errors after agent edits | Run pyright. Paste the errors back and ask for a fix that doesn't weaken types. |
| Commit message off-format | Re-run `/commit` or write it yourself. Don't argue with a misconfigured agent — replace it. |
| Conflicting conventions | Open an issue here to clarify the convention. Don't silently let the agent decide. |
