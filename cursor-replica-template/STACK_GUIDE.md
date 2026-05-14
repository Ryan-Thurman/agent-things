# Stack Guide

Use one shared workflow across all repos, then add the smallest stack-specific rule layer.

## Default

For most repos, treat the base template as the standard:

- `AGENTS.md`
- `.cursor/rules/*.mdc`
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

Use the same three Cursor modes in every repo:

- `Plan`
- `Build`
- `Review`

Do not create separate modes per stack unless your team has materially different workflows. Keep the mode system stable and let the repo rules supply the stack-specific behavior.

## Repo-Specific AGENTS Files

If you want zero editing when bootstrapping a repo, use the ready-made variants:

- TypeScript: `variants/typescript/AGENTS.md`
- Terraform: `variants/terraform/AGENTS.md`
- Python Databricks: `variants/python-databricks/AGENTS.md`

Each variant is the same workflow with stack-specific defaults baked in.
