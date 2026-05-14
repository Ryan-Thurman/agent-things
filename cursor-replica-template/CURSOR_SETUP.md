# Cursor Setup

This directory is the repo-committable part of the workflow.

Assumption for this tailored version:

- most repos are standard TypeScript repos
- one repo is Terraform infrastructure
- one repo is Python for Databricks

What can live in the repo:

- `AGENTS.md`
- `.cursor/rules/*.mdc`
- `plan.md`
- `todo.md`
- `review-skills/*`

Optional stack overlays also live here:

- `variants/terraform/.cursor/rules/*.mdc`
- `variants/python-databricks/.cursor/rules/*.mdc`

What still needs to be configured manually in Cursor:

- Custom Modes
- keyboard shortcuts for mode switching
- Background Agent usage preferences

Official references:

- Rules: https://docs.cursor.com/en/context/rules
- Modes: https://docs.cursor.com/chat/custom-modes
- Background Agents: https://docs.cursor.com/en/background-agents

## Repo Types

### Standard TypeScript Repo

Use the base files directly:

- `AGENTS.md`
- `.cursor/rules/*.mdc`
- `plan.md`
- `todo.md`

The base rules are optimized for this case.

If you want a pre-tuned root agent file, use:

- `variants/typescript/AGENTS.md`

### Terraform Repo

Use the base files, then also copy:

- `variants/terraform/.cursor/rules/50-terraform-infra.mdc`

If you want a pre-tuned root agent file, use:

- `variants/terraform/AGENTS.md`

### Python Databricks Repo

Use the base files, then also copy:

- `variants/python-databricks/.cursor/rules/50-python-databricks.mdc`

If you want a pre-tuned root agent file, use:

- `variants/python-databricks/AGENTS.md`

## Recommended Modes

Cursor's docs describe:

- `Ask` as read-only exploration
- `Agent` as full implementation mode
- `Custom` modes as user-defined combinations of tools and instructions

If your Cursor build has Custom Modes enabled, create these three modes.

### 1. Plan

Suggested tool access:

- codebase search
- read file
- terminal

Suggested instructions:

```md
You are in planning mode.

Do not modify source files.
Explore the codebase first, identify the relevant files and patterns, and write a concrete implementation plan to `plan.md`.

The plan must include:
- goal
- relevant files
- approach
- risks or open questions
- verification steps

After writing `plan.md`, stop and ask for explicit approval before making any code changes.
```

### 2. Build

Suggested tool access:

- full agent tools
- terminal
- edit and apply tools

Suggested instructions:

```md
Implement only after `plan.md` has been approved.

Keep `todo.md` updated during execution.
Use minimal diffs, preserve existing patterns, and run focused verification before finishing.

Your final response must state:
- what changed
- what was verified
- remaining risks
```

### 3. Review

Suggested tool access:

- codebase search
- read file
- terminal

Suggested instructions:

```md
You are in review mode.

Do not edit code unless explicitly asked.
Review the current diff, changed files, and validation results for bugs, regressions, missing tests, and risky assumptions.

Lead with findings. Keep any summary brief and secondary.
```

## If Custom Modes Are Not Available

Use:

- `Ask` for planning and read-only exploration
- `Agent` for implementation

Then paste one of these short prompts at the start of the chat.

Planning prompt:

```md
Work in read-only planning mode. Explore first, write `plan.md`, and stop for approval before editing code.
```

Implementation prompt:

```md
Implement the approved `plan.md`, keep `todo.md` updated, and finish with focused verification plus a short risk summary.
```

## Background Agent Pattern

Use background agents as sidecar workers for tasks like:

- investigate a subsystem
- run a longer validation step
- produce a second opinion on a risky change

Keep the main chat as the coordinator.

Good example:

- main chat writes the plan
- background agent checks the affected test suite
- background agent inspects a separate subsystem for integration risk
- main chat synthesizes those results and decides what to implement

Bad example:

- multiple agents editing the same files at once
- asking a background agent to "just do everything"

## How To Drop This Into A Repo

1. Copy `AGENTS.md` to the repo root.
2. Copy `.cursor/rules` into the repo root.
3. For the infra repo, also copy `variants/terraform/.cursor/rules/50-terraform-infra.mdc` into that repo's `.cursor/rules`.
4. For the Databricks repo, also copy `variants/python-databricks/.cursor/rules/50-python-databricks.mdc` into that repo's `.cursor/rules`.
5. Copy `review-skills` into the repo if you want reusable PR review profiles.
6. Add `plan.md` and `todo.md` to the repo root.
7. In Cursor, create the `Plan`, `Build`, and `Review` modes from the prompts above.
8. Optionally create `Review: Standards` and `Review: Performance` from [REVIEW_MODE_PROMPTS.md](REVIEW_MODE_PROMPTS.md).
9. Optionally create `Review: Simplify` and `Review: Cross-Repo Impact` from [REVIEW_MODE_PROMPTS.md](REVIEW_MODE_PROMPTS.md).
10. Start using `Plan` for any non-trivial task before switching to `Build`.
