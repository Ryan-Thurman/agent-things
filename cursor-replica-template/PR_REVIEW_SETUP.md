# PR Review Setup

This template includes two reusable review skills:

- `review-skills/pr-style-standards`
- `review-skills/pr-performance`
- `review-skills/repo-simplify`
- `review-skills/cross-repo-map`

Cursor does not natively execute `SKILL.md` files the way Codex can, so use them as review profiles for custom modes, saved prompts, or background agents.

## Recommended Usage

For meaningful PRs, run two review passes in parallel:

1. standards review
2. performance review

For larger or older areas of the codebase, add:

3. simplify review

For changes that may cross service, data, or infrastructure boundaries, add:

4. cross-repo impact review

Keep the main chat as the coordinator and synthesize the findings.

## Option A: Background Agent Prompts

### Standards review prompt

```md
Review this PR using the guidance in `review-skills/pr-style-standards/SKILL.md`.

Also read the stack-specific reference that matches this repo:
- TypeScript: `review-skills/pr-style-standards/references/typescript.md`
- Terraform: `review-skills/pr-style-standards/references/terraform.md`
- Python Databricks: `review-skills/pr-style-standards/references/python-databricks.md`

Lead with findings. Focus on maintainability, repository conventions, clarity, type safety, missing tests, and engineering quality. Skip formatter-only nits.
```

### Performance review prompt

```md
Review this PR using the guidance in `review-skills/pr-performance/SKILL.md`.

Also read the stack-specific reference that matches this repo:
- TypeScript: `review-skills/pr-performance/references/typescript.md`
- Terraform: `review-skills/pr-performance/references/terraform.md`
- Python Databricks: `review-skills/pr-performance/references/python-databricks.md`

Assume the code must hold up for roughly 500k users. Lead with findings. Focus on scale risks, hot paths, query counts, payload growth, batching, caching, indexing, rendering cost, memory growth, and synchronous work on latency-sensitive paths.
```

### Simplify review prompt

```md
Review the entire repository using the guidance in `review-skills/repo-simplify/SKILL.md`.

Also read the stack-specific reference that matches this repo:
- TypeScript: `review-skills/repo-simplify/references/typescript.md`
- Terraform: `review-skills/repo-simplify/references/terraform.md`
- Python Databricks: `review-skills/repo-simplify/references/python-databricks.md`

Focus on high-leverage simplification and refactor opportunities across the codebase. Group suggestions by high, medium, and low leverage. Avoid style-only cleanup and rewrite-heavy advice without clear payoff.
```

### Cross-repo impact prompt

```md
Review this repository and the planned or changed area using the guidance in `review-skills/cross-repo-map/SKILL.md`.

Read:
- `review-skills/cross-repo-map/references/repo-map.md` if present
- otherwise `review-skills/cross-repo-map/references/repo-map-template.md`

Focus on repo ownership, upstream and downstream dependencies, shared contracts, coordinated-change flows, and what could break if only this repo changes.
```

## Option B: Extra Custom Review Modes

If you want stronger separation, create extra Cursor custom modes:

- `Review: Standards`
- `Review: Performance`
- `Review: Simplify`
- `Review: Cross-Repo Impact`

Use the prompts above as the mode instructions.

## Practical Recommendation

Do not replace your normal `Review` mode.

Use:

- `Review` for general correctness and regressions
- `Review: Standards` for maintainability and conventions
- `Review: Performance` for scale-readiness
- `Review: Simplify` for codebase-wide refactor and complexity-reduction opportunities
- `Review: Cross-Repo Impact` for contract and dependency boundary analysis

That gives you the closest equivalent to specialized review subagents.
