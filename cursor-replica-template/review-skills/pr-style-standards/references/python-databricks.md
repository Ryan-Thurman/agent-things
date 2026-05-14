# Python Databricks Review Focus

Prioritize:

- business logic trapped inside notebooks instead of reusable Python modules
- environment-specific assumptions embedded in code
- import-time side effects
- weak separation between transformation logic and job orchestration
- missing tests around transformation behavior

Watch for:

- direct workspace paths or secrets handling in normal code paths
- Spark session assumptions that make code hard to test locally
- large functions that mix I/O, orchestration, and transformation logic
