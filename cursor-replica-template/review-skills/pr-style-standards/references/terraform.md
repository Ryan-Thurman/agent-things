# Terraform Review Focus

Prioritize:

- module interface churn without clear need
- variables or outputs that are ambiguous, weakly documented, or backwards-incompatible
- resource definitions that are hard to reason about across environments
- changes that mix unrelated infra concerns into one PR
- insecure defaults or widened access without explicit justification

Watch for:

- resource renames that imply replacement
- subtle drift caused by computed values or lifecycle settings
- policies or networking rules that are harder to audit after the change
