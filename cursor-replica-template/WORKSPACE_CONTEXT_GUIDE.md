# Workspace Context Guide

This guide is for a multi-repo workspace using Cursor + OpenSpec across these repos:

- `infra`
- `etl`
- `factory`
- `service`
- `learning`
- `privacy`
- `public_pages`
- `tco`
- `pwd`
- `hcp`

The goal is to give Cursor enough context to reason well without flooding it with stale or low-signal documentation.

## Core Principle

Do not optimize for "more context." Optimize for:

- current context
- local context
- contract context
- failure context

The best context is the smallest set of artifacts that let the agent answer:

1. what this repo owns
2. what behavior is intended
3. what contracts matter
4. what other repos can break
5. what failure modes already taught the team something

## What Context Is Useful

Keep these close to the code and indexed in Cursor.

### Per Repo

- `AGENTS.md`
- `.cursor/rules/*.mdc`
- `openspec/specs/`
- `openspec/changes/`
- `docs/sdd/`
- `docs/srs/`
- `system-atlas.md`

### High-Signal Content

- current capability specs
- current workflow and behavior docs
- API, event, table, queue, bucket, and job contracts
- deployment and environment boundaries
- validation rules and operational constraints
- known risky boundaries between repos
- recent incidents that changed design understanding

### Best Uses By Doc Type

- `system-atlas.md`
  - repo ownership
  - upstream/downstream dependencies
  - shared contracts
  - coordinated change flows
  - risky boundaries

- `docs/sdd/`
  - what the feature or workflow does
  - major flows
  - dependencies that shape behavior
  - failure modes worth remembering

- `docs/srs/`
  - requirements
  - validation rules
  - inputs and outputs
  - interface constraints

- `openspec/specs/`
  - accepted capability behavior

- `openspec/changes/`
  - active and recent non-trivial work

## What Context Is Not Worth Keeping

Do not make Cursor ingest large low-signal archives just because they exist.

Usually avoid:

- old Jira tickets with no durable insight
- duplicate docs that restate the same behavior in different words
- outdated architecture decks
- long prose docs with no owner and no update habit
- meeting notes
- slack transcripts
- one-off migration notes after the migration is complete
- giant requirement dumps that no longer match the code

If a document does not change decisions, reviews, or implementation, it is probably noise.

## How To Handle Bug Tickets And RCAs

Your instinct is right, but only if you curate them.

Do not dump raw bug tickets into the indexed context.

Instead, create a small incident knowledge layer:

- `docs/incidents/incident-index.md`
- `docs/incidents/YYYY-MM-short-name.md`

Only preserve incidents that contain reusable engineering knowledge:

- contract misunderstanding
- hidden cross-repo dependency
- recurring validation gap
- bad rollout sequence
- monitoring gap
- privacy or compliance edge case
- data quality failure pattern
- cache, queue, or retry failure mode

For each incident, keep it short:

- summary
- affected repos
- trigger
- root cause
- fix
- prevention
- which SDD, SRS, atlas, or OpenSpec spec should now reflect the lesson

Use RCAs to improve the durable docs:

- add validation rules to SRS
- add failure modes to SDD
- add risky boundaries to `system-atlas.md`
- add coordinated change guidance to the atlas

That gives you future RCA help without forcing Cursor to wade through ticket sludge.

## Recommended Multi-Repo Context Model

You have 10 repos, so use two layers.

### Layer 1: Repo-Local Truth

Each repo should own:

- its own `system-atlas.md`
- its own SDDs
- its own SRS docs
- its own OpenSpec specs and changes

This is where implementation-facing truth lives.

### Layer 2: Workspace-Level Map

Add one lightweight workspace doc outside the repos, or in a small coordination repo:

- `workspace-system-map.md`

This should not duplicate the repo atlases. It should only answer:

- what each repo owns
- main upstream/downstream relationships
- shared contracts across repos
- which repos are most tightly coupled
- normal coordinated change paths

For your repos, start with rows like:

- `infra`: environments, provisioning, deploy boundaries, secrets handoff
- `etl`: pipelines, sources, sinks, schedules, downstream consumers
- `factory`: shared generation/orchestration layer if that is its role
- `service`: core application or backend service contracts
- `learning`: model or learning workflow boundaries
- `privacy`: consent, deletion, compliance, policy enforcement
- `public_pages`: public web surface, SEO, analytics, content release path
- `tco`: domain-specific contracts and consumers
- `pwd`: domain-specific contracts and consumers
- `hcp`: domain-specific contracts and consumers

Keep the workspace map short enough to read in under five minutes.
Prefer `confidence` and `evidence` fields so Cursor can separate confirmed links from inferred links.

## How To Avoid Context Bloat In Cursor

Do not ask Cursor to read all 10 repos for every task.

Use this sequence:

1. Start with the repo you are changing.
2. Read that repo's `system-atlas.md`, relevant SDD, relevant SRS, and relevant OpenSpec artifacts.
3. Only pull in another repo when the atlas or spec says the contract crosses boundaries.
4. Use the workspace map only to identify which adjacent repo matters next.

This keeps the context graph narrow.

## Suggested Rules For OpenSpec In Your Workflow

Use OpenSpec changes when:

- behavior changes
- contracts change
- validation rules change
- cross-repo behavior changes
- rollout sequence matters
- the work touches privacy, public behavior, or data movement

Use `plan.md` only when:

- the change is internal
- the implementation is non-trivial
- no durable contract or behavior is changing

Implement directly only when:

- the change is tightly bounded
- behavior and contracts are unchanged

## What To Do With Jira

Replacing Jira feature planning with OpenSpec is the right move if you actually keep the repo docs current.

Recommended split:

- OpenSpec
  - active feature/change planning
  - spec deltas
  - task execution
  - approved capability behavior

- Jira
  - backlog triage
  - assignment
  - business tracking if the organization still requires it

Do not try to make Jira and OpenSpec equally authoritative for behavior. Pick OpenSpec as the engineering source of truth.

## Practical Setup On Your Work Laptop

### 1. Keep The 10 Repos In One Workspace

Use one Cursor workspace containing:

- `infra`
- `etl`
- `factory`
- `service`
- `learning`
- `privacy`
- `public_pages`
- `tco`
- `pwd`
- `hcp`

Optional:

- `workspace-docs` for cross-repo docs that do not belong to any single repo

### 2. Add A Small Shared Workspace Layer

Inside `workspace-docs`, create:

- `workspace-system-map.md`
- `incident-index.md`
- `repo-index.md`

Keep these manually curated and short.

Use the templates in [workspace-docs-template](/Users/mac/workspaces/agent-things/cursor-replica-template/workspace-docs-template).
For Cursor-assisted discovery, use [workspace-map-prompts.md](/Users/mac/workspaces/agent-things/cursor-replica-template/workspace-docs-template/workspace-map-prompts.md).

### 3. Add Repo-Local OpenSpec Docs

In each repo, add:

- `AGENTS.md`
- `.cursor/rules/`
- `openspec/`
- `docs/sdd/`
- `docs/srs/`
- `system-atlas.md`

Do not try to fully document all 10 repos at once.

Start with the 3 highest-change or highest-risk repos first:

- likely `service`
- `infra`
- one of `etl`, `privacy`, or the repo with the highest operational pain

### 4. Create Cursor Modes

Create these modes once on the laptop:

- `Plan: Spec`
- `Build: Spec Apply`
- `Review`
- `Review: Standards`
- `Review: Performance`
- `Update: SDD`
- `Update: SRS`
- `Review: Spec Sync`

### 5. Build The First Atlases

For each initial repo, fill in:

- purpose
- what it owns
- what it does not own
- upstream dependencies
- downstream consumers
- shared contracts
- risky boundaries

This is the highest-value document to write first.

### 6. Migrate Only The Durable Jira Knowledge

For active or recent feature work:

- create OpenSpec specs or changes

For old tickets:

- migrate only the ones that reveal a real invariant, contract, or failure mode
- convert the lesson into SDD, SRS, atlas, or incident docs

Do not bulk-import ticket history.

### 6a. Use One Cross-Repo Change Folder Per Feature

For a feature that touches multiple repos, create one shared OpenSpec change in `workspace-docs/openspec/changes/`.

Use these templates:

- [proposal.md](/Users/mac/workspaces/agent-things/cursor-replica-template/workspace-docs-template/openspec/changes/example-cross-repo-change/proposal.md)
- [design.md](/Users/mac/workspaces/agent-things/cursor-replica-template/workspace-docs-template/openspec/changes/example-cross-repo-change/design.md)
- [tasks.md](/Users/mac/workspaces/agent-things/cursor-replica-template/workspace-docs-template/openspec/changes/example-cross-repo-change/tasks.md)
- [validation.md](/Users/mac/workspaces/agent-things/cursor-replica-template/workspace-docs-template/openspec/changes/example-cross-repo-change/validation.md)

That shared change record should describe the coordinated feature once.
Repo-local SDD, SRS, and atlas docs should only hold the durable truth each repo owns.

### 7. Curate RCA Knowledge

When an RCA matters long-term:

1. write the short incident note
2. update the relevant atlas, SDD, or SRS
3. if behavior changed, update OpenSpec too

The incident note is memory.
The doc updates are the real value.

## Recommended Rollout Order

1. Create `workspace-docs/workspace-system-map.md`
2. Add `system-atlas.md` to `service`
3. Add `system-atlas.md` to `infra`
4. Add one SDD and one SRS to the most active repo
5. Start using OpenSpec changes for new non-trivial work
6. Add incident notes for the 5-10 most instructive RCAs
7. Expand to the next repos only after the first set is actually being maintained

## Good Operating Habits

- keep atlases short
- keep SDDs behavioral
- keep SRS docs contract-focused
- let OpenSpec hold active change intent
- update docs in the same branch as code
- use incidents to sharpen docs, not replace them
- prefer current truth over archival completeness

## Quick Heuristic

When deciding whether context is worth keeping, ask:

Would a future engineer or agent make a worse decision without this?

If the answer is no, drop it.
