# 01 — Clarify requirements

> **Mode:** read-only until approved · **Role:** Project Manager and Tech Lead, with Software Architect input · **Next:** `02-architecture.md`

Act as the Project Manager (`.agents/project-manager.md`) together with the Tech Lead (`.agents/tech-lead.md`), with input from the Software Architect (`.agents/software-architect.md`). Follow `AGENTS.md`.

## Input
<!-- Describe the project or feature here, or reference an issue or document. -->
Feature / goal: `<describe what you want to build and why>`

## Steps
1. Read `docs/project-context.md` and `docs/requirements.md`.
2. Identify the users, their primary journeys, constraints, and assumptions.
3. Write functional requirements (`REQ-NNN`) with a priority (`Must` / `Should` / `Could` / `Won't`).
4. Write testable acceptance criteria (`AC-NNN`) in Given / When / Then form, each linked to a requirement.
5. Capture nonfunctional requirements with measurable targets where possible: performance, reliability, accessibility, security and privacy, and supported environments.
6. List risks, dependencies, out-of-scope items, and open questions.

## Constraints
- Ask only questions that block progress. For everything else, state the assumption and move on.
- Do not design the solution yet, beyond noting constraints.
- Draft the changes to `docs/requirements.md`, but **wait for my approval before writing the file.**

## Output
- Summary of the goal and its users
- Proposed `docs/requirements.md` content (or a diff)
- Blocking questions, then assumptions made
