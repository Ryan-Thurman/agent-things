# Python Databricks Performance Focus

Prioritize:

- collect-to-driver patterns
- Python loops over data that should stay in Spark
- repeated scans of the same data
- wide transformations without clear partitioning strategy
- unnecessary shuffles, repartitions, or cache misuse
- job orchestration that serializes work unnecessarily

Watch for:

- converting large datasets to pandas on hot paths
- implicit actions triggered repeatedly
- expensive UDF use where built-in Spark functions would be better
- code that will only perform acceptably on oversized clusters
