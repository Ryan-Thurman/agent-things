---
name: sdd-update
description: Update the relevant SDD after implementing a feature so the design doc reflects the shipped behavior, workflow intent, dependencies, and failure modes.
---

# SDD Update

Use this skill after implementation when a feature or non-trivial change affected behavior, workflow intent, integrations, or important operational assumptions.

The goal is not to rewrite the design doc. The goal is to keep the SDD accurate and concise.

## What To Read

- the approved OpenSpec change
- the implemented code
- the current SDD in `docs/sdd/`
- the relevant SRS if interfaces or validation rules changed
- `system-atlas.md` if dependencies or boundaries changed

## What To Update

- summary of the capability or workflow
- system behavior that changed in practice
- major flows that are now different
- dependencies that matter to the feature
- failure modes or fallback behavior newly introduced by the change
- related spec references if they changed

## Output Expectations

- update the existing SDD instead of creating parallel notes unless a new domain document is clearly needed
- prefer precise workflow language over implementation trivia
- keep the document short enough that future engineers will maintain it
- remove stale statements instead of layering new text on top of wrong text

## Important Constraints

- do not invent behavior that is not in the code or approved spec
- do not turn the SDD into a changelog
- if the implementation and approved spec disagree, call out the drift instead of silently documenting the wrong thing
