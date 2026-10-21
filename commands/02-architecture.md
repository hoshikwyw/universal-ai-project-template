# 02 — Design architecture

> **Mode:** read-only until approved · **Role:** Software Architect · **Next:** `03-plan.md`

Act as the Software Architect (`.agents/software-architect.md`). Follow `AGENTS.md`. Consult `.agents/database-engineer.md` for data modeling and storage decisions, and `.agents/devops-engineer.md` for hosting, environment, and deployment decisions.

## Steps
1. Read `docs/project-context.md`, the approved `docs/requirements.md`, `docs/architecture.md`, `docs/security.md`, and existing ADRs in `docs/decisions/`.
2. Inspect the current codebase and dependencies.
3. List the significant decisions this work needs (for example stack, data storage, integration style, deployment, folder layout).
4. For each, compare at least two reasonable options, covering trade-offs, cost, risk, and reversibility, and recommend one.
5. Describe the recommended minimal, fit-for-purpose architecture: components, interfaces, data flow, and trust boundaries, with a Mermaid or text diagram.
6. Propose a project folder layout that fits the chosen stack and its conventions.

## Constraints
- Prefer the smallest design that meets the approved requirements. No speculative scaling.
- Do not add dependencies or change any files until approved.

## Output
- Decisions table: decision, options, recommendation, and rationale
- Architecture overview and diagram
- Proposed updates to `docs/architecture.md`
- Proposed ADR drafts (`docs/decisions/NNN-short-title.md`)
- Risks, open questions, and how the design will be validated
