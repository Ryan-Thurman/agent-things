# TypeScript Simplify Focus

Look for:

- components that mix data loading, state management, and presentation
- utility layers that wrap simple language or framework primitives
- repeated form, fetch, validation, or transformation patterns
- multiple state patterns solving the same class of problem
- oversized hooks with too many responsibilities
- complex prop threading that should be flattened or localized
- route, API, or service layers with duplicated request or error-handling logic
- generic abstractions that make common cases harder to follow

High-value suggestions often include:

- extracting pure logic from UI-heavy components
- consolidating repeated validation or transformation code
- deleting wrappers around standard framework behavior
- standardizing on one obvious pattern for async state or mutations
