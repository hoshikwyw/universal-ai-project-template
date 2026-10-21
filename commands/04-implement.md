# 04 — Implement one approved step

> **Mode:** writes code (approved scope only) · **Role:** Tech Lead, plus the engineering role(s) the step needs · **Next:** `05-qa.md`, plus `06-security.md` if the step is security-relevant

Act as the Tech Lead (`.agents/tech-lead.md`). Also apply the engineering role(s) named in the plan for this step: `.agents/frontend-engineer.md`, `.agents/backend-engineer.md`, `.agents/database-engineer.md`, and/or `.agents/devops-engineer.md`. Follow `AGENTS.md`.

## Input
Approved step:
```
<paste the full STEP row from the 03-plan output: ID, goal, AC items, roles, files, tests, approvals, risks>
```
Approvals granted for this step: `<for example "install X", or "none">`

## Steps
1. Check the working-tree status, and preserve any uncommitted changes that are not yours.
2. Read the acceptance criteria the step covers, and inspect the existing code in the affected area before editing.
3. Implement **only** this step, using existing conventions and dependencies.
4. Add or update focused tests for the new behavior. Cover the step's `AC-` items and its main error paths.
5. Run the step's verification commands, plus the available lint, type-check, and build steps.
6. Update any docs affected by the change: README and setup steps, `docs/project-context.md` commands, `docs/architecture.md`, and ADR status.
7. Self-review the diff against the review checklist in `.agents/tech-lead.md`, and against the definition of done in `AGENTS.md` section 6.

## Constraints
- Approval-gated actions (`AGENTS.md` section 4) are allowed only if they are listed under *Approvals granted for this step*. Anything else needs separate approval.
- If the step turns out larger or different than planned, stop and report back instead of expanding scope.
- Do not commit or push unless asked.

## Output
- The task report from `AGENTS.md` section 7: summary, assumptions, changed files, verification (commands and results), risks, and next steps
- Definition-of-done status: each item checked, or why it is not met
- The recommended next prompt: `05-qa.md`, and whether `06-security.md` is needed

**Stop after this step.**
