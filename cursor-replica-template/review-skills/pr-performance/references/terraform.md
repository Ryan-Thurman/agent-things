# Terraform Performance Focus

Prioritize:

- infrastructure changes that can create scaling bottlenecks or wasteful spend
- autoscaling or concurrency settings that do not match expected load
- missing caching, queueing, or async boundaries where synchronous scaling is expensive
- database, network, or storage defaults that are too small or too expensive for projected traffic

Watch for:

- single-instance bottlenecks
- undersized connection pools or throughput limits
- unnecessary cross-region traffic
- expensive resources introduced without clear scaling rationale
