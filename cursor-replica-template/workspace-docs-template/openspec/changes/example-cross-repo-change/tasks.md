# Tasks

Use this as the execution checklist for the coordinated change.

## Workspace Coordination

- [ ] Confirm affected repos and contract owners
- [ ] Confirm rollout order
- [ ] Confirm validation plan

## Repo Tasks

### service

- [ ] Implement owned backend changes
- [ ] Update owned SRS docs
- [ ] Update owned SDD docs if workflow behavior changed
- [ ] Update `system-atlas.md` if boundary changes

### public_pages

- [ ] Implement owned UI changes
- [ ] Update owned SRS docs
- [ ] Update owned SDD docs if workflow behavior changed
- [ ] Update `system-atlas.md` if boundary changes

### etl

- [ ] Implement owned pipeline or data changes
- [ ] Update owned SRS docs
- [ ] Update owned SDD docs if workflow behavior changed
- [ ] Update `system-atlas.md` if boundary changes

Adjust the repo sections to match the actual change.

## Verification

- [ ] Validate repo-local tests and checks
- [ ] Validate end-to-end behavior across repo boundaries
- [ ] Validate rollback or safe failure path if relevant

## Completion

- [ ] Confirm repo-local durable docs are updated
- [ ] Confirm this change record matches the final implementation
