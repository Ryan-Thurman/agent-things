---
name: repo-simplify
description: Review the current repository for opportunities to simplify, refactor, reduce duplication, and remove unnecessary complexity. Use when you want recommendations similar to a codebase-wide "simplify" pass rather than a correctness or performance review.
---

# Repo Simplify Review

Use this skill for a refactor-and-simplify review pass across the codebase. The goal is not cosmetic cleanup. The goal is to identify complexity that is making the repository harder to change, understand, or operate.

This skill should produce suggestions, not automatic rewrites, unless the user explicitly asks for implementation.

## What To Look For

- duplicated logic that should be centralized
- abstractions that add indirection without real payoff
- large functions, classes, or components with mixed responsibilities
- repeated condition trees or mapping code
- inconsistent patterns solving the same problem in different ways
- dead code, stale helpers, or compatibility layers that no longer justify themselves
- state shape or data flow that is more complicated than the use case requires
- unnecessary configuration surface or over-generalized APIs

## Good Simplification Targets

Prioritize suggestions that:

- remove code rather than add more code
- unify multiple patterns into one established pattern
- reduce cognitive load for future changes
- make testing easier
- shrink public surface area
- reduce coupling between modules

Avoid suggestions that are only stylistic or that create risky churn without meaningful payoff.

## Output Format

Group suggestions by impact:

- high leverage
- medium leverage
- low leverage

For each suggestion, state:

- file or area
- current complexity
- why it is harder than it needs to be
- the simplification direction
- expected payoff
- migration risk

Start by identifying the highest-leverage areas in the repository before drilling into specific files.

If there are no worthwhile simplifications, say so explicitly.

## Stack References

- For TypeScript repos, read `references/typescript.md`.
- For Terraform repos, read `references/terraform.md`.
- For Python Databricks repos, read `references/python-databricks.md`.

## Important Constraints

- Prefer simplification that preserves behavior.
- Do not recommend large rewrites unless the current design is actively harmful.
- Prefer suggestions that can be implemented incrementally.
- Be skeptical of "helper" layers, wrappers, or generic frameworks that exist only to abstract simple code.
- Default to codebase-wide recommendations unless the user narrows the scope to a subdirectory or feature area.
