# 02 — Design architecture

> **Mode:** read-only until approved; then updates docs and ADRs · **Role:** Software Architect, consulting Database, DevOps, Security, and QA as relevant · **Next:** `03-plan.md`

Act as the Software Architect (`.agents/software-architect.md`). Follow `AGENTS.md`. Consult the following roles where their area is affected:

- `.agents/database-engineer.md`: data modeling and storage
- `.agents/devops-engineer.md`: hosting, environments, CI/CD, and deployment
- `.agents/security-engineer.md`: trust boundaries, authentication, and sensitive data
- `.agents/qa-engineer.md`: test approach and tooling
- `.agents/frontend-engineer.md` and `.agents/backend-engineer.md`: UI and API structure

## Steps
1. Read `docs/project-context.md`, `docs/requirements.md`, `docs/architecture.md`, `docs/security.md`, `docs/testing-strategy.md`, and the existing ADRs in `docs/decisions/`. If `docs/requirements.md` is not marked `Approved`, say so before continuing.
2. Inspect the current codebase and dependencies.
3. List the significant decisions this work needs (for example stack, data storage, integration style, authentication, deployment, test tooling). If there are none, say so and recommend going straight to `03-plan.md`.
4. For each decision, compare at least two reasonable options, covering trade-offs, cost, risk, and reversibility, and recommend one.
5. Describe the recommended minimal, fit-for-purpose architecture: components, interfaces, data flow, and trust boundaries, with a Mermaid or text diagram.
6. Folder layout: for a new project, propose one that fits the chosen stack's conventions. For an existing project, follow the current layout and propose changes only if they are needed.
7. Identify the security impact (assets, entry points, trust boundaries) and the testing approach (test levels and tools) implied by the design.

## Constraints
- Prefer the smallest design that meets the approved requirements. No speculative scaling.
- Do not add dependencies, scaffold code, or change any files until approved.

## Output
- Decisions table: decision, options, recommendation, and rationale
- Architecture overview and diagram
- Proposed updates to `docs/architecture.md`, including the ADR index
- Proposed ADR drafts, numbered from the next free `NNN` (`docs/decisions/NNN-short-title.md`, `Status: Proposed`)
- Proposed updates to `docs/security.md` (assets, trust boundaries, entry points) and `docs/testing-strategy.md` (test levels and tools)
- Proposed updates to `docs/project-context.md` if the stack or key directories change
- Risks, open questions, and how the design will be validated

**Wait for my approval.** Then:
- write the approved doc updates and ADRs, and set accepted ADRs to `Status: Accepted`
- set `docs/architecture.md` to `Status: Approved`
- update the `Last updated` date on every doc you changed
