# 00 — Discover project

> **Mode:** read-only; docs updated only after approval · **Role:** Tech Lead, with Software Architect input · **Next:** `01-requirements.md`

Act as the Tech Lead (`.agents/tech-lead.md`), with input from the Software Architect (`.agents/software-architect.md`). Follow `AGENTS.md`.

## Steps
1. Read every file in `docs/`. Note which fields are still `TODO` or `UNKNOWN`.
2. Check the working-tree status and current branch.
3. Inspect the repository: folder layout, manifests and lockfiles, languages, frameworks, tooling, tests, CI configuration, scripts, and `.github/` templates.
4. Identify the real commands for setup, run, lint, type-check, test, and build, and where each is defined. Run only commands that are clearly read-only and safe (for example listing files or printing tool versions). Mark everything else `NOT RUN`.
5. Compare what you found against `docs/`, and note every discrepancy.

## Constraints
- Do not edit, create, or delete files, and do not install anything, until I approve the proposed doc updates.
- If this is a fresh copy of the template with no application code yet, say so. Mostly `UNKNOWN` results are expected; do not invent a stack.

## Output
1. **Project snapshot:** type, stack and versions, and stage (or `UNKNOWN`)
2. **Structure:** key directories and what each contains
3. **Commands:** a table of purpose, command, source (where you found it), and status
4. **Discrepancies** between the docs and the repository
5. **Unknowns and risks**
6. **Proposed doc updates:** drafts for `docs/project-context.md` (stack, directories, commands), and for the test-commands table in `docs/testing-strategy.md`
7. **Top five questions** to resolve before moving on, most important first

After I approve, apply only the approved doc updates, and set each updated doc's `Last updated` date.
