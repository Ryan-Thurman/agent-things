If a single feature usually touches 2-3 repos, then repo-local docs are not enough by themselves. You need a cross-repo change home.

What To Do Instead

Use 3 layers:

1. Workspace-level change spec
2. Repo-local truth
3. Owned contract docs

For a feature touching service, public_pages, and maybe etl, do not create three separate “main” specs. Create one canonical feature
change in a shared place, then let each repo hold only its local durable truth.

Recommended Structure

Create a small coordination repo or workspace-docs folder with:

workspace-docs/
workspace-system-map.md
openspec/
changes/
add-foo-feature/
proposal.md
design.md
tasks.md
validation.md

Then keep repo-local docs like:

service/
system-atlas.md
docs/sdd/
docs/srs/
openspec/specs/

public_pages/
system-atlas.md
docs/sdd/
docs/srs/
openspec/specs/

How To Split Responsibility

- workspace-docs/openspec/changes/...
  - one feature story
  - affected repos
  - contract changes
  - rollout order
  - validation matrix
  - sequencing and coordination risk
- each repo’s system-atlas.md
  - what that repo owns
  - upstream/downstream dependencies
  - risky boundaries
- each repo’s docs/sdd/
  - local workflow behavior in that repo
- each repo’s docs/srs/
  - contracts that repo owns

Important Rule

Put the contract doc in the repo that owns the contract.

Example:

- backend API contract belongs in service
- UI rendering/interaction behavior belongs in public_pages
- ETL schema or event contract belongs in etl

The cross-repo change spec should reference those docs, not duplicate them.

What Cursor Should Read For A Cross-Repo Feature

Start narrow:

1. workspace-system-map.md
2. the active cross-repo OpenSpec change
3. the atlas for the repo you’re editing first
4. the owned SRS/SDD docs for the contract being changed
5. only then the adjacent repo’s relevant docs

Do not ask Cursor to read all 10 repos just because they are indexed.

Best Workflow For You

For a feature spanning backend + UI + ETL:

1. Create one cross-repo OpenSpec change in workspace-docs
2. List affected repos explicitly
3. Identify which repo owns each changed contract
4. Implement repo by repo
5. Update local SDD/SRS only where durable truth changed
6. Use one shared validation checklist across repos
7. After merge, keep the workspace change as history, but keep durable truth in the repos

What Should Be In The Cross-Repo Change

For each feature, include:

- goal
- user-visible behavior
- affected repos
- owned contracts
- sequence of implementation
- rollout/flag strategy
- validation by repo
- failure/rollback concerns

That document becomes the thing Cursor reasons from during implementation.

What Not To Do

- Don’t duplicate the same full feature spec in every repo
- Don’t keep backend and UI requirements in one repo if ownership is split
- Don’t use Jira tickets as the main cross-repo source of truth
- Don’t let SRS become one giant master doc per repo

Split SRS by contract area, not by “everything this repo does.”

Concrete Example

For service + public_pages + privacy:

- workspace change:
  - feature intent
  - repos affected
  - rollout sequence
  - validation matrix
- service/docs/srs/...
  - API request/response changes
  - auth/validation rules
- public_pages/docs/sdd/...
  - page flow and user interaction changes
- privacy/docs/srs/...
  - consent/deletion/compliance rule changes
- each repo atlas:
  - note the boundary if it changed

Recommendation

Your real operating model should be:

- workspace-level OpenSpec for active cross-repo changes
- repo-level SDD/SRS/atlas for durable owned truth

  Best way to do it

  Start with a partially empty workspace-system-map.md, then have Cursor build it in passes.
  1. Repo role pass
  2. Contract/dependency pass
  3. Coordinated-change-flow pass
  4. Human review pass

  Do not ask Cursor to “map the whole workspace” in one shot. That usually produces vague junk.

  What Cursor is good at finding
  - service-to-service calls
  - API clients and route handlers
  - env vars pointing at other systems
  - queue/topic/event names
  - table/schema/bucket references
  - Terraform outputs and consumers
  - CI/deploy references
  - ownership clues in READMEs and deployment files
  - recurring repo pairings in code and docs

  What Cursor is bad at inferring reliably
  - actual business ownership
  - tribal rollout sequences
  - whether a connection is still active in production
  - whether an old integration is dead but still referenced
  - compliance/process expectations not encoded in code

  So the map should explicitly label confidence.

  Change the map format slightly

  Add this under each dependency or contract:
  - confidence: confirmed | inferred | unknown
  - evidence: file paths or config names

  That makes Cursor much more useful.

  Good workflow in Cursor

  Use read-only / planning mode first.

  Prompt 1, per repo:

  Map the role of the `service` repo in this workspace.

  Read only:
  - README files
  - package manifests
  - deployment/config files
  - Terraform or infra references
  - route handlers, clients, jobs, and integration points

  Output:
  - purpose
  - what it owns
  - likely upstream dependencies
  - likely downstream consumers
  - shared contracts
  - confidence per item: confirmed or inferred
  - evidence as file paths

  Do not guess silently. Call out unknowns explicitly.

  Prompt 2, adjacency pass:

  Review `service` and `public_pages` together.

  Find:
  - direct API calls
  - shared auth/session assumptions
  - shared payloads or schemas
  - deployment coupling
  - feature flows that normally require both repos

  Output:
  - confirmed connections
  - inferred connections
  - risky boundaries
  - what should be added to workspace-system-map.md
  - evidence as file paths

  Prompt 3, workspace synthesis:

  Using the repo-level findings already gathered, draft `workspace-system-map.md`.

  Rules:
  - keep it short
  - prefer concrete contracts over generic architecture language
  - distinguish confirmed from inferred
  - leave unknowns explicit

  Practical mapping order for your repos

  Start with the likely backbone first:
  1. service
  2. public_pages
  3. infra
  4. privacy
  5. etl

  Then fill in:
  - factory
  - learning
  - tco
  - pwd
  - hcp

  That order is better because backend/UI/infra/privacy usually reveal the main contracts fastest.

  What to look for repo by repo
  - service
    - APIs
    - auth/session
    - events
    - DB ownership
    - downstream consumers
  - public_pages
    - backend endpoints called
    - analytics/consent
    - feature flag dependencies
    - SEO/content release flow
  - infra
    - deployment boundaries
    - secrets
    - environment wiring
    - queue/topic/storage ownership
  - privacy
    - consent/deletion flows
    - policy enforcement hooks
    - shared identifiers
    - audit/compliance boundaries
  - etl
    - upstream sources
    - downstream datasets
    - schedules/jobs
    - contracts consumed by service/learning/reporting

  Important constraint

  Do not try to fully solve ownership from code alone. Let Cursor draft:
  - repo purpose
  - contracts
  - likely neighbors
  - evidence

  Then you review and correct:
  - ownership
  - real production importance
  - standard rollout order

  My recommendation

  Use Cursor to produce:
  - first-pass repo roles
  - first-pass adjacency maps
  - a draft workspace-system-map.md
