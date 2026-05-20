# `.claude/` — Claude Code shared toolkit

This directory is consumed by [Claude Code](https://docs.claude.com/en/docs/claude-code/overview). It defines the **shared slash commands** and **sub-agent definitions** every repo in the `phronesis-framework` org uses.

The point: agents work to a fixed reference frame. No re-deciding style, structure, or process per repo.

## Layout

```
.claude/
├── commands/        # slash-command prompts: /commit, /plan, /review-pr, /test, /new-feature
└── agents/          # sub-agent definitions: planner, reviewer, test-writer, doc-writer
```

## How downstream repos use this

Either:

1. **Copy** `.claude/` into the new repo (simple, drifts over time), or
2. **Sparse-checkout** this repo's `.claude/` as a vendored directory (stays in sync).

A future improvement: a `gh phronesis sync-claude` extension.

## Changing a command or sub-agent

Open a PR **here**. Per-repo forks of these prompts are not allowed — they erode the convention. If a repo needs different behavior, pass it as input to the existing prompt; don't fork the prompt.

See also:

- [`docs/conventions/agents.md`](../docs/conventions/agents.md)
- [`docs/guides/working-with-claude.md`](../docs/guides/working-with-claude.md)
