---
name: pr-style-standards
description: Review a pull request for coding standards, maintainability, consistency with repository patterns, and general engineering quality. Use when a PR needs a standards-oriented review pass, especially before merge or after a large refactor.
---

# PR Style And Standards Review

Use this skill for a review pass focused on code quality and repository standards rather than feature correctness alone.

## What To Look For

- Inconsistency with established repository patterns
- Unclear naming, structure, or control flow
- Unnecessary abstraction or indirection
- Type-safety regressions
- Missing validation or error handling
- Fragile tests or missing tests for changed behavior
- Dead code, duplicated logic, or hidden coupling

## Review Output

Lead with findings.

For each finding, state:

- severity
- file or area
- what is wrong
- why it matters
- what a better direction would be

If there are no material findings, say so explicitly and note any residual risks or test gaps.

## Stack References

- For TypeScript repos, read `references/typescript.md`.
- For Terraform repos, read `references/terraform.md`.
- For Python Databricks repos, read `references/python-databricks.md`.

## Important Constraints

- Do not nitpick formatting if the formatter would handle it automatically.
- Prefer maintainability, clarity, and correctness over personal taste.
- Focus on issues that would matter in a real code review.
