---
description: Analyze staged changes and write a Conventional Commit in the org style.
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git add:*), Bash(git commit:*)
---

# /commit

You are creating a single commit that follows the Phronesis Framework org [commit conventions](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/commits.md).

## Rules

1. **Conventional Commits 1.0.** Format: `<type>(<scope>): <subject>`.
2. **Allowed types**: `feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `build`, `ci`, `chore`, `revert`.
3. **Subject**: imperative, lowercase, no trailing period, ≤72 chars.
4. **Body**: explain the *why*, wrap at 100 chars. Required for any change beyond a one-line fix.
5. **No emojis** unless the diff itself adds emojis.
6. **Footer**: include `Refs: #N` / `Fixes: #N` if applicable and `Co-Authored-By:` for agent-assisted content.
7. **Never** use `--no-verify`, `--amend` (unless explicitly asked), or `--force` push.
8. **Never** stage files in `.gitignore` or anything that looks like a secret (`.env`, credentials, keys).

## Procedure

1. Run `git status` and `git diff --staged` (plus `git diff` if anything is unstaged that should be staged).
2. Run `git log --oneline -10` to match the repo's existing style.
3. Decide the type and scope. Pick the smallest scope that's still informative — see the scope catalog in `docs/conventions/commits.md`.
4. Draft the message in a HEREDOC commit:

   ```bash
   git commit -m "$(cat <<'EOF'
   <type>(<scope>): <subject>

   <body>

   Co-Authored-By: Claude (claude-opus-4-7) <noreply@anthropic.com>
   EOF
   )"
   ```

5. After commit, run `git status` to confirm a clean tree.

If pre-commit hooks fail, fix the issues and create a **new** commit. Never `--amend` after a hook failure (the original commit didn't happen).

If there's nothing to commit, say so and stop. Do not create an empty commit.
