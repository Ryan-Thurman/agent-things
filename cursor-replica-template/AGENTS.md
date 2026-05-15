# Agent Workflow

Follow a terminal-style workflow. Be concise, direct, and action-oriented.

## Default Approach

- Start by understanding the request and inspecting the existing code before editing.
- Prefer existing patterns over inventing new structure.
- For non-trivial work, use an OpenSpec-first workflow when behavior, interfaces, workflows, or cross-system boundaries change.
- Keep the user updated with short progress notes during longer tasks.

## Planning

For non-trivial work:

- Explore the codebase in read-only mode first.
- Identify the files, code paths, existing capability specs, and documentation that matter.
- If it is unclear whether the task needs OpenSpec, use `review-skills/spec-triage/SKILL.md` to decide between an OpenSpec change, `plan.md`, or direct implementation.
- If the change affects behavior, interfaces, workflows, data contracts, or cross-repo connectivity:
  - draft or update an OpenSpec change in `openspec/changes/`
  - inspect related files in `openspec/specs/`, `docs/sdd/`, `docs/srs/`, and `system-atlas.md`
  - stop for approval before implementation
- If the change is an internal refactor or tightly bounded edit with no spec impact, use `plan.md` only if a lightweight implementation plan would still help.

Skip formal planning only for clearly bounded changes such as a typo fix, a one-line bug fix, or a tightly specified small edit.

## Implementation

- Implement only after the relevant plan or spec direction is approved.
- For OpenSpec-driven work, treat the approved change artifacts as the working source of truth.
- Keep a running checklist in `openspec/changes/.../tasks.md` when working from OpenSpec, or in `todo.md` for non-spec implementation work.
- Only one task should be marked `in_progress` at a time.
- Prefer small diffs that preserve existing architecture.
- Do not make unrelated changes.

## Documentation Sync

- If implementation changes behavior or workflows, update the relevant SDD in `docs/sdd/` in the same branch.
- If interfaces or requirements change, update the relevant SRS in `docs/srs/`.
- If system boundaries or dependencies change, update `system-atlas.md`.
- Do not leave OpenSpec, code, and design docs drifting apart.

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
