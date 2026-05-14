# TypeScript Performance Focus

Prioritize:

- repeated fetches or RPC calls
- N+1 data access patterns
- large JSON payloads or over-fetching
- synchronous CPU-heavy work on request or render paths
- repeated expensive transforms during rendering
- missing pagination, memoization, batching, caching, or indexing where the access pattern demands it

Frontend watchpoints:

- rerender cascades
- large list rendering without virtualization where needed
- unnecessary derived-state recomputation
- oversized client bundles on critical paths

Backend watchpoints:

- serial awaits that could be parallelized safely
- per-item database or service calls
- missing indexes for new query shapes
- expensive joins or filters moved into app code
