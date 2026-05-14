# Repo Map Template

Fill this in once per organization or product area and keep it updated.

## Repo Summary

### repo-name

- Purpose:
- Primary stack:
- Owns:
- Does not own:
- Main deploy/runtime environment:

## Dependencies

### repo-name

- Upstream repos:
  - repo:
  - dependency type:
  - contract or interface:
  - failure mode if contract changes:

- Downstream repos:
  - repo:
  - dependency type:
  - contract or interface:
  - failure mode if this repo changes:

## Shared Contracts

Document concrete boundaries:

- HTTP or RPC APIs
- events or queues
- database tables or views
- storage buckets or paths
- IaC-managed infrastructure
- secrets, env vars, or config handoffs
- Databricks jobs, outputs, or data products

For each contract:

- Producer repo:
- Consumer repo:
- Interface name:
- Change sensitivity:
- How to verify a change safely:

## Coordinated Change Flows

Examples:

- app feature requiring backend and infra changes
- schema change requiring pipeline and app changes
- new Databricks output requiring app or analytics changes

For each flow:

- Trigger:
- Repos commonly touched:
- Order of operations:
- Verification checklist:

## Known Risky Boundaries

- Boundary:
- Why it is risky:
- Typical failure mode:
- How to check it:

## Unknowns Or Missing Documentation

- Unknown:
- Who should clarify it:
- Where the missing documentation should live:
