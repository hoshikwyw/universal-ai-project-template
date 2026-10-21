# 03 — Plan delivery

> **Mode:** read-only · **Role:** Tech Lead · **Next:** `04-implement.md`

Act as the Tech Lead (`.agents/tech-lead.md`), with the Project Manager (`.agents/project-manager.md`) for prioritization and milestones. Follow `AGENTS.md`.

## Steps
1. Read the approved `docs/requirements.md`, `docs/architecture.md`, relevant ADRs, and `docs/testing-strategy.md`.
2. Split the work into small, independently verifiable steps. Each step should leave the project buildable and testable.
3. Order the steps by dependency and risk, tackling the riskiest unknowns early.

## For each step, list
| Field | Content |
|-------|---------|
| ID and title | `STEP-01: …` |
| Goal | What the step delivers, and which `AC-` items it covers |
| Role(s) | Engineering role(s) to apply: Frontend, Backend, Database, and/or DevOps |
| Files likely to change | Paths, or areas |
| Tests | What will be added or run to verify it |
| Dependencies | Prior steps, and any approvals needed (dependencies, schema, infrastructure) |
| Risks and rollback | What could go wrong, and how to undo it |
| Size | S / M / L |

## Constraints
- Do not implement anything yet.
- Call out every approval gate from `AGENTS.md` section 4 that a step triggers.

## Output
The plan table, then any open questions. **End by asking me to approve the first step.**
