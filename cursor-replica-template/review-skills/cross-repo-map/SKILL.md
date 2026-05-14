---
name: cross-repo-map
description: Map how the current repository fits into the surrounding repo ecosystem, including ownership, dependencies, shared contracts, and coordinated-change risks. Use when planning work, reviewing changes, or documenting how multiple repos interact.
---

# Cross Repo Map

Use this skill to understand and document how a repository fits into the broader system.

The goal is to answer questions like:

- What does this repo own?
- Which other repos depend on it?
- Which repos does it depend on?
- What contracts cross repo boundaries?
- What kinds of changes here usually require coordinated changes elsewhere?

## What To Look For

- explicit service-to-service calls
- shared APIs, schemas, events, tables, buckets, queues, or config
- infrastructure dependencies that connect one repo to another
- deployment or runtime configuration handoffs
- ownership boundaries and responsibility splits
- places where one repo can silently break another

## Expected Inputs

If available, read:

- `references/repo-map.md`

If no filled-in map exists yet, use:

- `references/repo-map-template.md`

You can also infer relationships from the codebase, deployment files, README files, CI config, Terraform, and data pipeline configuration.

## Output Format

Provide:

1. Current repo role
2. Upstream dependencies
3. Downstream consumers
4. Shared contracts and risky boundaries
5. Common coordinated-change flows
6. Missing mapping information
7. Suggested additions or corrections to the repo map

When reviewing a planned change or diff, also provide:

- likely affected repos
- interfaces or contracts to verify
- infrastructure or deployment dependencies to check
- breakage risks if only this repo changes

## Important Constraints

- Prefer concrete contracts over vague system diagrams.
- Call out unknowns explicitly.
- Distinguish confirmed links from inferred links.
- Optimize for planning and impact analysis, not architecture theater.
