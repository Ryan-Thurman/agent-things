# Python Databricks Simplify Focus

Look for:

- notebook logic that should live in reusable Python modules
- orchestration, I/O, and transformation logic mixed in the same function
- repeated Spark session, path, config, or secret access code
- job code that duplicates pipeline steps across notebooks or tasks
- wrappers around Databricks or Spark APIs that do not meaningfully simplify usage
- configuration branching that obscures the happy path

High-value suggestions often include:

- moving business logic into testable modules
- standardizing shared pipeline utilities
- separating orchestration from transformation logic
- deleting convenience wrappers that hide straightforward Spark operations
