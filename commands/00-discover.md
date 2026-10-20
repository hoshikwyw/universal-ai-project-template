# 00 — Discover project

> **Mode:** read-only · **Role:** Tech Lead, with Software Architect input · **Next:** `01-requirements.md`

Act as the Tech Lead (`.agents/tech-lead.md`), with input from the Software Architect (`.agents/software-architect.md`). Follow `AGENTS.md`.

## Steps
1. Read `AGENTS.md` and every file in `docs/`.
2. Inspect the repository: folder layout, manifests and lockfiles, languages, frameworks, tooling, tests, CI configuration, and scripts.
3. Identify the real commands for setup, run, lint, type-check, test, and build. Run only commands that are clearly read-only and safe (for example listing files or printing versions). Mark everything else `NOT RUN`.
4. Compare what you found against `docs/`, and note every discrepancy.

## Constraints
- Do not edit, create, or delete files. Do not install anything.
- Do not assume this template is already a working application. Empty placeholders are normal.

## Output
1. **Project snapshot:** type, stack and versions, and stage (or `UNKNOWN`)
2. **Structure:** key directories and what each contains
3. **Commands:** a table of purpose, command, and source (where you found it), with the status of each
4. **Discrepancies** between the docs and the repository
5. **Unknowns and risks**
6. **Proposed updates to `docs/project-context.md`**, as a draft for my approval
7. **Top five questions** to resolve before moving on, most important first
