# 03 — Plan delivery

> **Mode:** read-only · **Role:** Tech Lead, with the Project Manager · **Next:** `04-implement.md` (one step at a time)

Act as the Tech Lead (`.agents/tech-lead.md`), with the Project Manager (`.agents/project-manager.md`) for prioritization and milestones. Follow `AGENTS.md`.

## Steps
1. Read `docs/requirements.md`, `docs/architecture.md`, relevant ADRs, `docs/testing-strategy.md`, and `docs/project-context.md`. Flag any doc that is not marked `Approved` but should be.
2. If the project has no tooling yet (no manifest, test runner, linter, or CI), make `STEP-01` a setup step that creates exactly that. It will need approval for the dependency installs.
3. Split the work into small, independently verifiable steps. Each step should leave the project buildable and its tests passing.
4. Order the steps by dependency and risk, tackling the riskiest unknowns early. Group them into milestones if the work is large.

## For each step, list
| Field | Content |
|-------|---------|
| ID and title | `STEP-01: …` |
| Goal | What the step delivers, and which `REQ-` / `AC-` items it covers |
| Role(s) | Engineering role(s) to apply: Frontend, Backend, Database, and/or DevOps |
| Files likely to change | Paths, or areas |
| Tests | What will be added, and which commands verify the step |
| Approvals needed | Every gate from `AGENTS.md` section 4 the step triggers (dependencies, schema, infrastructure, file deletion, …) |
| Reviews | Whether the step needs `06-security.md`, in addition to `05-qa.md` |
| Risks and rollback | What could go wrong, and how to undo it |
| Size | S / M / L |

## Constraints
- Do not implement anything yet.
- Every `Must` acceptance criterion in scope must be covered by at least one step. List any criteria left uncovered.

## Output
1. The plan table
2. Coverage check: `AC-` → `STEP-`
3. Open questions

**End by asking me to approve the first step.** Each step must be self-contained, so I can paste a single row into `04-implement.md` in a new session.
