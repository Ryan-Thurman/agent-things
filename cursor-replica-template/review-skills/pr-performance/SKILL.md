---
name: pr-performance
description: Review a pull request for performance risks, scalability limits, and efficiency regressions. Use when changes may affect latency, throughput, query count, rendering cost, memory growth, or infrastructure cost, especially for systems expected to serve around 500k users.
---

# PR Performance Review

Use this skill for a performance-focused review pass. The standard is not micro-optimization. The goal is to catch code that will become expensive, slow, or fragile at production scale.

Assume the organization expects code to hold up for roughly 500k users. Review with that scale in mind.

## What To Look For

- Repeated work inside hot paths
- N+1 queries or repeated remote calls
- Unbounded scans, loops, or payload growth
- Large data loads when filtering, paging, or batching should exist
- Excessive rendering or recomputation
- Memory growth tied to request size, user count, or dataset size
- Missing caching, indexing, batching, pagination, or backpressure where clearly needed
- Changes that move work from offline/background paths into synchronous request paths

## Review Output

Lead with findings.

For each finding, state:

- severity
- file or area
- hot path or scale assumption
- what could degrade at higher load
- the likely better direction

If there are no material findings, say so explicitly and note any assumptions you could not validate locally.

## Stack References

- For TypeScript repos, read `references/typescript.md`.
- For Terraform repos, read `references/terraform.md`.
- For Python Databricks repos, read `references/python-databricks.md`.

## Review Principles

- Focus on realistic production risks, not speculative micro-optimizations.
- Challenge anything that scales with number of rows, users, requests, renders, or remote calls.
- Prefer simple, robust fixes over clever ones.
