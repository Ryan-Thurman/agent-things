# Workspace Map Prompts

Use these prompts in Cursor to build `workspace-system-map.md` in read-only passes.

Do not ask Cursor to map all repos at once.

## Pass 1: Repo Role

```md
Map the role of the `<repo-name>` repo in this workspace.

Read only:
- README files
- package manifests or build files
- deployment and config files
- Terraform or infra references
- route handlers, clients, jobs, and integration points

Output:
- purpose
- what it likely owns
- likely upstream dependencies
- likely downstream consumers
- key contracts
- confidence per item: confirmed, inferred, or unknown
- evidence as file paths or concrete config names

Do not guess silently. Call out unknowns explicitly.
```

## Pass 2: Repo Pair Adjacency

```md
Review `<repo-a>` and `<repo-b>` together.

Find:
- direct API calls
- shared auth or identity assumptions
- shared payloads, schemas, events, or storage paths
- deployment coupling
- feature flows that normally require both repos

Output:
- confirmed connections
- inferred connections
- risky boundaries
- likely coordinated change flows
- confidence per item
- evidence as file paths
```

## Pass 3: Workspace Synthesis

```md
Using the repo-level and adjacency findings already gathered, draft `workspace-system-map.md`.

Rules:
- keep it short
- prefer concrete contracts over generic architecture language
- distinguish confirmed from inferred
- leave unknowns explicit
- include evidence where possible
```

## Suggested Order

Start with the backbone repos first:

1. `service`
2. `public_pages`
3. `infra`
4. `privacy`
5. `etl`

Then fill in the remaining repos.
