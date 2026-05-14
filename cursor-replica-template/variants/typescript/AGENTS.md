# Agent Workflow

This repository is a standard single-repo TypeScript codebase.

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

Skip planning only for tightly bounded edits with an obvious implementation.

## Implementation

- Implement only after the plan is approved.
- Keep a running checklist in `todo.md`.
- Only one task should be marked `in_progress` at a time.
- Prefer small diffs that preserve existing architecture.
- Reuse existing utility types, validation helpers, and package conventions.
- Avoid introducing `any` unless the surrounding code already relies on it and there is a clear reason.

## Verification

- Prefer the repo's existing `test`, `lint`, and `typecheck` scripts when present.
- Start with the narrowest useful validation for the changed area.
- Report what you changed, what you verified, and any remaining risk.

## Review Style

When asked to review:

- Lead with findings.
- Prioritize bugs, regressions, missing tests, risky assumptions, and type-safety regressions.
- Keep summaries brief and secondary.
