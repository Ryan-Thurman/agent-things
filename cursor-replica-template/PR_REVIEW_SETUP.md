# PR Review Setup

This template keeps two reusable PR review skills:

- `review-skills/pr-style-standards`
- `review-skills/pr-performance`

Use them as the backing guidance for Cursor custom modes, saved prompts, or background agents.

## Recommended Review Passes

For meaningful PRs:

1. Run `Review` for general correctness and regressions.
2. Run `Review: Standards` for maintainability and repo conventions.
3. Run `Review: Performance` for scale and efficiency risks.

If the change also updates behavior or workflows, run `Update: SDD` before the final merge review.

## Background Agent Prompts

### Standards review prompt

```md
Review this PR using `review-skills/pr-style-standards/SKILL.md`.

Also read the stack-specific reference that matches this repo:
- TypeScript: `review-skills/pr-style-standards/references/typescript.md`
- Terraform: `review-skills/pr-style-standards/references/terraform.md`
- Python Databricks: `review-skills/pr-style-standards/references/python-databricks.md`

Lead with findings.
```

### Performance review prompt

```md
Review this PR using `review-skills/pr-performance/SKILL.md`.

Also read the stack-specific reference that matches this repo:
- TypeScript: `review-skills/pr-performance/references/typescript.md`
- Terraform: `review-skills/pr-performance/references/terraform.md`
- Python Databricks: `review-skills/pr-performance/references/python-databricks.md`

Lead with findings.
```

## Cursor Modes

Create these custom modes if you want the review passes permanently available:

- `Review: Standards`
- `Review: Performance`

Use the prompts in [REVIEW_MODE_PROMPTS.md](/Users/mac/workspaces/agent-things/cursor-replica-template/REVIEW_MODE_PROMPTS.md).
