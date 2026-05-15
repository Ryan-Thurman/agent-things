# Cursor Setup

This template is optimized for a Cursor + OpenSpec workflow.

For a multi-repo workspace rollout, see [WORKSPACE_CONTEXT_GUIDE.md](/Users/mac/workspaces/agent-things/cursor-replica-template/WORKSPACE_CONTEXT_GUIDE.md).
For shared cross-repo feature planning, use [workspace-docs-template](/Users/mac/workspaces/agent-things/cursor-replica-template/workspace-docs-template).

## Canonical Repo Artifacts

Keep these in the repo:

- `AGENTS.md`
- `.cursor/rules/*.mdc`
- `openspec/`
- `docs/sdd/`
- `docs/srs/`
- `system-atlas.md`

Optional fallback artifacts:

- `plan.md` for internal work that does not need OpenSpec
- `todo.md` for non-spec task tracking

Reusable skills kept in this template:

- `review-skills/spec-triage`
- `review-skills/pr-style-standards`
- `review-skills/pr-performance`
- `review-skills/sdd-update`
- `review-skills/srs-update`

## Workflow

For non-trivial work:

1. If scope is unclear, use `spec-triage` to decide the path.
2. Use `Plan: Spec` when the task needs OpenSpec planning.
3. Draft or update the OpenSpec change.
4. Implement from the approved spec in `Build: Spec Apply`.
5. Run `Review`, `Review: Standards`, and `Review: Performance` as needed.
6. Run `Update: SDD` when the change affects behavior or workflows.
7. Run `Update: SRS` when the change affects interfaces, validation, or requirements.
8. Run `Review: Spec Sync` when you want a final drift check.

Use `plan.md` only when the work is internal enough that creating an OpenSpec change would be noise.

## Recommended Cursor Modes

Create these custom modes in Cursor:

- `Plan: Spec`
- `Build: Spec Apply`
- `Review: Spec Sync`
- `Update: SDD`
- `Update: SRS`
- `Review: Standards`
- `Review: Performance`

Mode prompts live in:

- [SPEC_MODE_PROMPTS.md](/Users/mac/workspaces/agent-things/cursor-replica-template/SPEC_MODE_PROMPTS.md)
- [REVIEW_MODE_PROMPTS.md](/Users/mac/workspaces/agent-things/cursor-replica-template/REVIEW_MODE_PROMPTS.md)

## Repo Types

### Standard TypeScript Repo

Use the base files directly.

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

## OpenSpec Templates

Use `openspec-template/` as the single template source for:

- `system-atlas.md`
- `docs/sdd/`
- `docs/srs/`

Do not duplicate these templates elsewhere in the repo.

## How To Drop This Into A Repo

1. Copy `AGENTS.md` to the repo root.
2. Copy `.cursor/rules` into the repo root.
3. Copy `openspec-template/system-atlas.md` to `system-atlas.md`.
4. Copy `openspec-template/docs/sdd/sdd-template.md` into `docs/sdd/`.
5. Copy `openspec-template/docs/srs/srs-template.md` into `docs/srs/`.
6. Add or initialize `openspec/`.
7. Copy `review-skills/spec-triage`, `review-skills/pr-style-standards`, `review-skills/pr-performance`, `review-skills/sdd-update`, and `review-skills/srs-update` if you want reusable prompt-backed skills.
8. Optionally copy `plan.md` and `todo.md` for non-spec fallback work.
9. In Cursor, create the recommended custom modes from the prompt files above.
