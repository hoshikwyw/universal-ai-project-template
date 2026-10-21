# 01 — Clarify requirements

> **Mode:** read-only until approved; then updates `docs/requirements.md` · **Role:** Project Manager and Tech Lead, with Software Architect input · **Next:** `02-architecture.md`, or `03-plan.md` if no design decisions are needed

Act as the Project Manager (`.agents/project-manager.md`) together with the Tech Lead (`.agents/tech-lead.md`), with input from the Software Architect (`.agents/software-architect.md`). Follow `AGENTS.md`.

## Input
Feature / goal: `<describe what you want to build and why, or link an issue or document>`

## Steps
1. Read `docs/project-context.md` and the current `docs/requirements.md`. Continue the existing ID numbering; never renumber or reuse IDs.
2. Restate the goal, and propose how success will be measured.
3. Identify the users, their primary journeys, constraints, and assumptions.
4. Write functional requirements (`REQ-NNN`), each with a priority (`Must` / `Should` / `Could` / `Won't`).
5. Write acceptance criteria (`AC-NNN`) in Given / When / Then form, each linked to a requirement. Every `Must` needs at least one. Each criterion must be specific enough for QA to verify with a test.
6. Write nonfunctional requirements (`NFR-NNN`) with measurable targets where possible: performance, reliability, accessibility, security and privacy, and supported environments.
7. List risks, dependencies, out-of-scope items, and open questions (each with an owner).

## Constraints
- Ask only questions that block progress. For everything else, state the assumption and move on.
- Describe *what* and *why*, not *how*. Note technical constraints, but do not design the solution.

## Output
- Summary of the goal, users, and success measures
- Proposed `docs/requirements.md` content (or a diff, if the file already has content)
- Blocking questions, then the assumptions made
- Recommended next step: `02-architecture.md` if the work needs new components, a stack choice, data-model changes, or new integrations; otherwise `03-plan.md`

**Wait for my approval.** Then write `docs/requirements.md`, set its `Status` to `Approved`, and update its `Last updated` date.
