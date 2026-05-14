# TypeScript Review Focus

Prioritize:

- type regressions, unnecessary `any`, and unsafe casts
- APIs that are hard to understand or easy to misuse
- divergence from existing patterns in `package.json` scripts, validation, state handling, or data access
- duplicated business logic instead of reuse of existing helpers
- weak error handling around network, parsing, or async paths
- tests that cover only happy paths

Watch for:

- hidden nullable paths
- optional chaining masking missing invariants
- broad utility abstractions that make simple code harder to follow
- large components or handlers that should be split by responsibility
