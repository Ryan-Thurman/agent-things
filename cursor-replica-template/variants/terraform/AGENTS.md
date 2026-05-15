# Agent Workflow

This repository is Terraform infrastructure code.

Follow a terminal-style workflow. Be concise, direct, and conservative with infra changes.

## Default Approach

- Start by understanding the requested infrastructure outcome and inspecting current modules, variables, outputs, and environment boundaries.
- Prefer existing module and environment patterns over introducing new structure.
- For non-trivial work, use an OpenSpec-first workflow when behavior, interfaces, workflows, or infra boundaries change.

## Planning

For non-trivial tasks:

- Explore the codebase in read-only mode first.
- Identify affected modules, state boundaries, providers, contracts, and any resources with destroy-and-recreate risk.
- If it is unclear whether the task needs OpenSpec, use `review-skills/spec-triage/SKILL.md`.
- If the change affects behavior, interfaces, workflows, or shared infra boundaries:
  - draft or update an OpenSpec change
  - inspect related files in `openspec/specs/`, `docs/sdd/`, `docs/srs/`, and `system-atlas.md`
  - stop and wait for approval before editing source files
- Use `plan.md` only for internal infra work that does not need spec artifacts.

## Implementation

- Implement only after the relevant plan or spec is approved.
- Keep a running checklist in `openspec/changes/.../tasks.md` for OpenSpec work or `todo.md` for non-spec work.
- Prefer minimal changes that preserve module interfaces unless the task explicitly requires breaking changes.
- Do not assume resource renames or moves are safe.
- Update the relevant SDD and `system-atlas.md` when implementation changes workflows or environment boundaries.
- Update the relevant SRS when implementation changes module interfaces, inputs, outputs, or validation constraints.

## Verification

- Prefer the repo's existing Terraform wrapper scripts or CI entrypoints when present.
- Otherwise prefer `terraform fmt` and `terraform validate` where meaningful.
- If a plan requires remote credentials or backend access that is unavailable locally, say so explicitly.

## Review Style

When asked to review:

- Lead with findings.
- Prioritize unintended destroy/recreate risk, security-sensitive exposure, drift risk, and module interface breaks.
- Keep summaries brief and secondary.
