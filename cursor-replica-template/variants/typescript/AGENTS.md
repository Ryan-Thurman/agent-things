# Agent Workflow

This repository is a standard single-repo TypeScript codebase.

Follow a terminal-style workflow. Be concise, direct, and action-oriented.

## Default Approach

- Start by understanding the request and inspecting the existing code before editing.
- Prefer existing patterns over inventing new structure.
- For non-trivial work, use an OpenSpec-first workflow when behavior, interfaces, workflows, or contracts change.
- Keep the user updated with short progress notes during longer tasks.

## Planning

For non-trivial tasks:

- Explore the codebase in read-only mode first.
- Identify the files, code paths, package boundaries, and existing specs that matter.
- If it is unclear whether the task needs OpenSpec, use `review-skills/spec-triage/SKILL.md`.
- If the change affects behavior, interfaces, workflows, or contracts:
  - draft or update an OpenSpec change
  - inspect related files in `openspec/specs/`, `docs/sdd/`, `docs/srs/`, and `system-atlas.md`
  - stop and wait for approval before editing source files
- Use `plan.md` only for internal changes that do not warrant OpenSpec artifacts.

Skip planning only for tightly bounded edits with an obvious implementation.

## Implementation

- Implement only after the relevant plan or spec is approved.
- Keep a running checklist in `openspec/changes/.../tasks.md` for OpenSpec work or `todo.md` for non-spec work.
- Only one task should be marked `in_progress` at a time.
- Prefer small diffs that preserve existing architecture.
- Reuse existing utility types, validation helpers, and package conventions.
- Avoid introducing `any` unless the surrounding code already relies on it and there is a clear reason.
- Update the relevant SDD when implementation changes behavior or workflow intent.
- Update the relevant SRS when implementation changes interfaces, validation rules, or requirements.

## Verification

- Prefer the repo's existing `test`, `lint`, and `typecheck` scripts when present.
- Start with the narrowest useful validation for the changed area.
- Report what you changed, what you verified, and any remaining risk.

## Review Style

When asked to review:

- Lead with findings.
- Prioritize bugs, regressions, missing tests, risky assumptions, and type-safety regressions.
- Keep summaries brief and secondary.
