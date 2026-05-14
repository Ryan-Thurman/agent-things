# Terraform Simplify Focus

Look for:

- modules that are more configurable than the organization actually needs
- repeated resource patterns that should be one shared module
- variable sets that expose too much surface area
- environment differences encoded as copy-paste instead of a cleaner input model
- locals, dynamic blocks, or conditionals that make plans difficult to reason about
- compatibility outputs or variables that are no longer needed

High-value suggestions often include:

- shrinking module interfaces
- standardizing repeated infrastructure patterns
- removing obsolete toggles and backward-compatibility layers
- making environment behavior easier to audit from a small set of inputs
