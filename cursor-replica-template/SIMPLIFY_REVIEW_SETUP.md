# Simplify Review Setup

This template includes a simplification review skill:

- `review-skills/repo-simplify`

Use it when you want suggestions similar to a Cursor-style simplify pass: not bug-finding, not benchmarking, but identifying where the codebase can be made easier to understand and maintain.

## Recommended Usage

Run simplify review as a separate pass from:

- correctness review
- standards review
- performance review

That separation keeps the simplify pass focused on leverage instead of mixing it with normal PR triage.

## Background Agent Prompt

```md
Review the entire repository using the guidance in `review-skills/repo-simplify/SKILL.md`.

Also read the stack-specific reference that matches this repo:
- TypeScript: `review-skills/repo-simplify/references/typescript.md`
- Terraform: `review-skills/repo-simplify/references/terraform.md`
- Python Databricks: `review-skills/repo-simplify/references/python-databricks.md`

Start by identifying the highest-leverage areas in the codebase, then propose refactor and simplification opportunities.
Do not propose style-only cleanup or large rewrites without clear payoff.

Group suggestions by:
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
```

## Extra Custom Mode

If you want this permanently available in Cursor, create:

- `Review: Simplify`

Use the prompt in [REVIEW_MODE_PROMPTS.md](REVIEW_MODE_PROMPTS.md).
