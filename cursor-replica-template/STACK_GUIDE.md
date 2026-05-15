# Stack Guide

Use one shared workflow across all repos, then add the smallest stack-specific rule layer.

## Default

For most repos, treat the base template as the standard:

- `AGENTS.md`
- `.cursor/rules/*.mdc`
- `openspec/`
- `docs/sdd/`
- `docs/srs/`
- `system-atlas.md`

Optional fallback artifacts:

- `plan.md`
- `todo.md`

This is the TypeScript/default setup.

## Terraform Repo

Add:

- `variants/terraform/.cursor/rules/50-terraform-infra.mdc`

This adds a more conservative review and verification posture around state, module interfaces, and destroy/recreate risk.

## Python Databricks Repo

Add:

- `variants/python-databricks/.cursor/rules/50-python-databricks.mdc`

This keeps the workflow grounded in normal Python engineering while accounting for Databricks-specific runtime and deployment constraints.

## Practical Recommendation

Use the same core Cursor modes in every repo:

- `Plan: Spec`
- `Build: Spec Apply`
- `Review`
- `Review: Standards`
- `Review: Performance`
- `Update: SDD`
- `Update: SRS`

Optionally add:

- `Review: Spec Sync`

Keep the mode system stable and let the repo rules supply the stack-specific behavior.

## Repo-Specific AGENTS Files

If you want zero editing when bootstrapping a repo, use the ready-made variants:

- TypeScript: `variants/typescript/AGENTS.md`
- Terraform: `variants/terraform/AGENTS.md`
- Python Databricks: `variants/python-databricks/AGENTS.md`

Each variant is the same workflow with stack-specific defaults baked in.
