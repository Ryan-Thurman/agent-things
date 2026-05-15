---
name: srs-update
description: Update the relevant SRS after implementing a feature so the requirements and interface docs reflect the shipped contracts, validation rules, constraints, inputs, and outputs.
---

# SRS Update

Use this skill after implementation when a feature or non-trivial change affected interfaces, validation rules, requirements, inputs or outputs, operational constraints, or other contract-level behavior.

The goal is not to rewrite the requirements doc. The goal is to keep the SRS accurate and concise.

## What To Read

- the approved OpenSpec change
- the implemented code
- the current SRS in `docs/srs/`
- the relevant SDD if workflow behavior changed
- `system-atlas.md` if upstream or downstream contracts changed

## What To Update

- requirements that changed in practice
- constraints that now matter to the feature
- inputs and outputs that changed
- validation rules or acceptance rules that changed
- upstream or downstream dependency notes that changed
- related spec references if they changed

## Output Expectations

- update the existing SRS instead of creating parallel notes unless a new requirement area clearly needs its own document
- prefer contract and validation language over implementation detail
- keep the document short enough that future engineers will maintain it
- remove stale statements instead of layering new text on top of wrong text

## Important Constraints

- do not invent requirements that are not in the code or approved spec
- do not turn the SRS into a changelog
- if the implementation and approved spec disagree, call out the drift instead of silently documenting the wrong thing
