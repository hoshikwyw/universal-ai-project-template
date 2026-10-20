# 04 — Implement one approved step

> **Mode:** writes code (approved scope only) · **Role:** Tech Lead · **Next:** `05-qa.md`

Act as the Tech Lead (`.agents/tech-lead.md`). Follow `AGENTS.md`.

## Input
Approved step: `<STEP-ID and title from the delivery plan>`

## Steps
1. Check working-tree status, and preserve any uncommitted changes that are not yours.
2. Inspect the existing code in the affected area before editing.
3. Implement **only** the approved step, using existing conventions and dependencies.
4. Add or update focused tests for the new behavior.
5. Run the available targeted checks (tests, lint, type-check, build).
6. Self-review the diff using the Tech Lead review checklist.

## Constraints
- Do not deploy, migrate schemas, install or upgrade dependencies, delete files, or touch secrets without separate approval.
- If the step turns out larger or different than planned, stop and report back instead of expanding scope.
- Do not commit or push unless asked.

## Output
Use the task report format from `AGENTS.md` section 7: summary, assumptions, changed files, verification (commands and results), risks, and next steps. **Stop after this step.**
