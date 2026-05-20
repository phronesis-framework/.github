---
description: Review a PR against the org conventions.
allowed-tools: Bash(gh pr view:*), Bash(gh pr diff:*), Bash(gh pr checks:*), Bash(git log:*)
---

# /review-pr

You are reviewing a pull request against the [Phronesis Framework org conventions](https://github.com/phronesis-framework/.github/tree/main/docs/conventions).

PR identifier (number, URL, or branch): $ARGUMENTS

## Procedure

1. Fetch the PR:
   - `gh pr view $ARGUMENTS --json title,body,baseRefName,headRefName,labels,author,files`
   - `gh pr diff $ARGUMENTS`
   - `gh pr checks $ARGUMENTS` (skip if CI hasn't run yet)
2. Identify the PR's stated goal from the body.
3. Read the diff against the checklist below.

## Review checklist

For each item, mark ✓ / ✗ / N/A and add a one-line rationale.

### Scope
- [ ] PR touches only what its title and body claim.
- [ ] No unrelated refactors smuggled in.
- [ ] PR is small enough to review in one sitting (rough ceiling: 400 added lines, excluding tests and lockfiles).

### Conventions
- [ ] Commit messages follow [Conventional Commits](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/commits.md).
- [ ] Python style matches [python.md](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/python.md): type hints, `from __future__ import annotations`, no bare `Any`, Google docstrings.
- [ ] Tests follow [testing.md](https://github.com/phronesis-framework/.github/blob/main/docs/conventions/testing.md): named correctly, located under `tests/unit/...` or `tests/integration/...`, async tests use anyio bounds.
- [ ] Docs updated when public API or conventions changed.

### Correctness
- [ ] Logic is correct on the happy path.
- [ ] Edge cases identified in the diff are handled (empty input, None, concurrent access, large input).
- [ ] No swallowed exceptions. Errors come from the package's exception hierarchy.
- [ ] Async code does not leak background tasks; cancellation is propagated.

### Types & security
- [ ] Pyright strict passes (per CI).
- [ ] No secrets or tokens added.
- [ ] No dependencies added without explicit justification in the PR body.
- [ ] Workflows changes don't widen `permissions:` or use `pull_request_target` without a comment.

### CI
- [ ] All checks green. If not, explain which and why.

## Output

Produce a single review comment in markdown with:

1. A one-sentence verdict: **Approve**, **Request changes**, or **Comment**.
2. The checklist above with marks and rationale.
3. Inline observations grouped by file (use the form `path/to/file.py:LINE` for navigation).
4. Suggested follow-up issues (if any) — don't bury them inside this PR's scope.

Do **not** post the comment via `gh`. Return it as text for the human to post.
