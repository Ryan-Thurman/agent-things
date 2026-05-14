# Agent Workflow

This repository is a Python Databricks codebase.

Follow a terminal-style workflow. Be concise, direct, and explicit about local-vs-workspace validation limits.

## Default Approach

- Start by understanding whether the change affects notebooks, jobs, libraries, deployment config, or data pipelines.
- Prefer existing project structure and packaging patterns over new layout conventions.
- For non-trivial work, plan first, then implement, then verify.

## Planning

For non-trivial tasks:

- Explore the codebase in read-only mode first.
- Identify runtime assumptions involving Spark, Databricks jobs, secrets, cluster config, widgets, or workspace paths.
- Write a concrete implementation plan to `plan.md`.
- Stop and wait for approval before editing source files.

## Implementation

- Implement only after the plan is approved.
- Keep a running checklist in `todo.md`.
- Prefer logic in normal Python modules when possible instead of notebook-only code.
- Avoid unnecessary side effects at import time.

## Verification

- Prefer the repo's existing formatter, linter, and test runner when present.
- Start with local unit tests and static checks.
- If full validation requires Databricks workspace access or cluster execution, say so explicitly.

## Review Style

When asked to review:

- Lead with findings.
- Prioritize runtime-only assumptions, Spark inefficiencies, environment-coupled behavior, and missing local-test coverage for transformation logic.
- Keep summaries brief and secondary.
