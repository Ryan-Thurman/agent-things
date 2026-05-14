# Cross Repo Setup

This template includes a cross-repo mapping skill:

- `review-skills/cross-repo-map`

Use it to document and review how repositories interact, especially when changes may cross application, infrastructure, and data boundaries.

## Recommended Workflow

1. Create a filled-in repo map from `review-skills/cross-repo-map/references/repo-map-template.md`.
2. Save the filled-in version as:
   - `review-skills/cross-repo-map/references/repo-map.md`
3. Keep that file updated as boundaries and contracts change.

## Good Uses

- planning a feature that may touch multiple repos
- reviewing a change for cross-repo impact
- onboarding someone to repo ownership boundaries
- checking whether a schema, API, or infra change needs coordinated work elsewhere

## Cursor Usage

If you want this permanently available in Cursor, create:

- `Review: Cross-Repo Impact`

Use the prompt in [REVIEW_MODE_PROMPTS.md](REVIEW_MODE_PROMPTS.md).

## Background Agent Prompt

```md
Review this repository using the guidance in `review-skills/cross-repo-map/SKILL.md`.

Read:
- `review-skills/cross-repo-map/references/repo-map.md` if present
- otherwise `review-skills/cross-repo-map/references/repo-map-template.md`

Map:
- what this repo owns
- upstream dependencies
- downstream consumers
- shared contracts
- coordinated-change flows
- missing documentation

If a planned change or diff is in scope, also identify:
- which other repos may be affected
- what interfaces or contracts should be checked
- what could silently break if only this repo changes
```
