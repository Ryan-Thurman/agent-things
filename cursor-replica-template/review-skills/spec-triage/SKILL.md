---
name: spec-triage
description: Decide whether a requested change should use an OpenSpec change, a lightweight plan.md plan, or direct implementation, based on behavior, interfaces, workflows, data contracts, and cross-system impact.
---

# Spec Triage

Use this skill at the start of a task when it is not obvious whether the work needs full OpenSpec planning.

The goal is to prevent two failure modes:

- creating spec artifacts for changes that are too small to justify them
- skipping spec work for changes that alter behavior, contracts, workflows, or system boundaries

## What To Read

- the user request
- the relevant code area
- related files in `openspec/specs/` if they exist
- related `docs/sdd/` and `docs/srs/`
- `system-atlas.md` when dependencies or boundaries may be involved

## Decision Output

Classify the task into one of these paths:

1. `openspec-change`
2. `plan-md`
3. `direct-implementation`

## Use `openspec-change` When

- behavior changes
- interfaces or validation rules change
- workflow intent changes
- data contracts change
- infra boundaries or cross-repo connectivity change
- the work has enough product or operational risk that review should happen before coding

## Use `plan-md` When

- the work is internal and non-trivial
- implementation thinking is needed before editing
- behavior and contracts are not changing enough to justify OpenSpec artifacts

## Use `direct-implementation` When

- the change is tightly bounded
- the implementation is obvious
- behavior and contracts are unchanged
- creating planning artifacts would add more friction than clarity

## Output Format

Provide:

- chosen path
- why that path fits
- files or docs that should be read next
- whether SDD, SRS, or `system-atlas.md` are likely to need updates later

## Important Constraints

- prefer `openspec-change` when behavior or contracts are materially changing
- prefer `plan-md` over `direct-implementation` when the work is ambiguous but still internal
- do not use trivial size alone as the decision rule; a small interface change can still need OpenSpec
