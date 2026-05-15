# Agent Workflow

This repository is a Python Databricks codebase.

Follow a terminal-style workflow. Be concise, direct, and explicit about local-vs-workspace validation limits.

## Default Approach

- Start by understanding whether the change affects notebooks, jobs, libraries, deployment config, or data pipelines.
- Prefer existing project structure and packaging patterns over new layout conventions.
- For non-trivial work, use an OpenSpec-first workflow when behavior, interfaces, workflows, or data contracts change.

## Planning

For non-trivial tasks:

- Explore the codebase in read-only mode first.
- Identify runtime assumptions involving Spark, Databricks jobs, secrets, cluster config, widgets, workspace paths, and downstream consumers.
- If it is unclear whether the task needs OpenSpec, use `review-skills/spec-triage/SKILL.md`.
- If the change affects behavior, interfaces, workflows, jobs, or data contracts:
  - draft or update an OpenSpec change
  - inspect related files in `openspec/specs/`, `docs/sdd/`, `docs/srs/`, and `system-atlas.md`
  - stop and wait for approval before editing source files
- Use `plan.md` only for internal changes that do not need spec artifacts.

## Implementation

- Implement only after the relevant plan or spec is approved.
- Keep a running checklist in `openspec/changes/.../tasks.md` for OpenSpec work or `todo.md` for non-spec work.
- Prefer logic in normal Python modules when possible instead of notebook-only code.
- Avoid unnecessary side effects at import time.
- Update the relevant SDD when implementation changes pipeline behavior or workflow intent.
- Update the relevant SRS when implementation changes interfaces, data contracts, validation rules, or job inputs and outputs.

## Verification

- Prefer the repo's existing formatter, linter, and test runner when present.
- Start with local unit tests and static checks.
- If full validation requires Databricks workspace access or cluster execution, say so explicitly.

## Review Style

When asked to review:

- Lead with findings.
- Prioritize runtime-only assumptions, Spark inefficiencies, environment-coupled behavior, and missing local-test coverage for transformation logic.
- Keep summaries brief and secondary.
