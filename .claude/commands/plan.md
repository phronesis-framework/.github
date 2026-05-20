---
description: Produce a file-level implementation plan for a task. No code yet.
---

# /plan

You are producing an **implementation plan** for the task described below. You do **not** write code in this command.

## Output structure

Respond with the following sections — and only these:

### Goal
One sentence. What user-visible behavior changes when this is done?

### Non-goals
Bullet list. What this plan does *not* address. Bound the scope explicitly.

### Files
Table with three columns:

| File | Change | Approximate diff size |
|---|---|---|
| `src/...` | Modify / Create / Delete | small / medium / large |

### Steps
Numbered list of concrete actions in order. Each step references the files it touches. No step should exceed a single PR.

### Risks
Bullet list. What could go wrong? What conventions could this violate? What needs human review?

### Open questions
Bullet list. What do I need clarified before writing code?

## Rules

- **Reference conventions explicitly.** Cite `docs/conventions/python.md`, `docs/conventions/testing.md`, etc. by section when relevant.
- **No new dependencies** unless listed as an explicit step with justification.
- **Tests are part of the plan**, not an afterthought.
- **Docs updates are part of the plan** when the change touches public API or conventions.
- **Stop after the plan.** Do not start editing files. Wait for human approval.

## Task

$ARGUMENTS
