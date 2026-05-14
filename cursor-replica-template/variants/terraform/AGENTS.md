# Agent Workflow

This repository is Terraform infrastructure code.

Follow a terminal-style workflow. Be concise, direct, and conservative with infra changes.

## Default Approach

- Start by understanding the requested infrastructure outcome and inspecting current modules, variables, outputs, and environment boundaries.
- Prefer existing module and environment patterns over introducing new structure.
- For non-trivial work, plan first, then implement, then verify.

## Planning

For non-trivial tasks:

- Explore the codebase in read-only mode first.
- Identify affected modules, state boundaries, providers, and any resources with destroy-and-recreate risk.
- Write a concrete implementation plan to `plan.md`.
- Stop and wait for approval before editing source files.

## Implementation

- Implement only after the plan is approved.
- Keep a running checklist in `todo.md`.
- Prefer minimal changes that preserve module interfaces unless the task explicitly requires breaking changes.
- Do not assume resource renames or moves are safe.

## Verification

- Prefer the repo's existing Terraform wrapper scripts or CI entrypoints when present.
- Otherwise prefer `terraform fmt` and `terraform validate` where meaningful.
- If a plan requires remote credentials or backend access that is unavailable locally, say so explicitly.

## Review Style

When asked to review:

- Lead with findings.
- Prioritize unintended destroy/recreate risk, security-sensitive exposure, drift risk, and module interface breaks.
- Keep summaries brief and secondary.
