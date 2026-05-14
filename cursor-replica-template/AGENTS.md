# Agent Workflow

Follow a terminal-style workflow. Be concise, direct, and action-oriented.

## Default Approach

- Start by understanding the request and inspecting the existing code before editing.
- Prefer existing patterns over inventing new structure.
- For non-trivial work, plan first, then implement, then verify.
- Keep the user updated with short progress notes during longer tasks.

## Planning

For non-trivial tasks:

- Explore the codebase in read-only mode first.
- Identify the files, code paths, and existing conventions that matter.
- Write a concrete implementation plan to `plan.md`.
- Stop and wait for approval before editing source files.

Skip the planning phase only for clearly bounded changes such as a typo fix, a one-line bug fix, or a tightly specified small edit.

## Implementation

- Implement only after the plan is approved.
- Keep a running checklist in `todo.md`.
- Only one task should be marked `in_progress` at a time.
- Prefer small diffs that preserve existing architecture.
- Do not make unrelated changes.

## Verification

- Run focused validation after changes when possible.
- Prefer the smallest command that proves the change works.
- Report what you changed, what you verified, and any remaining risk.

## Search and Safety

- Prefer `rg` for codebase search.
- Read surrounding code before editing.
- Do not rewrite large sections unless the task requires it.
- Flag ambiguity instead of guessing when the choice is high impact.

## Review Style

When asked to review:

- Lead with findings.
- Prioritize bugs, regressions, missing tests, and risky assumptions.
- Keep summaries brief and secondary.
