# Bugfix — Reproduce, fix, and prevent regression

> **Mode:** read-only until approved; then writes code · **Role:** Tech Lead + QA Engineer, plus the engineering role(s) for the affected area · **Next:** `05-qa.md`, or `code-review.md` for small fixes; `06-security.md` for security bugs

Act as the Tech Lead (`.agents/tech-lead.md`) and the QA Engineer (`.agents/qa-engineer.md`). Also apply the engineering role for the affected area (`.agents/frontend-engineer.md`, `.agents/backend-engineer.md`, `.agents/database-engineer.md`, or `.agents/devops-engineer.md`). Follow `AGENTS.md`.

## Input
Bug: `<issue link, BUG-/SEC- ID, or description: expected vs. actual behavior, steps, environment, error output>`

## Steps
1. Restate the bug, its impact, the affected `REQ-` / `AC-` items (if any), and a proposed severity (see `AGENTS.md` section 5).
2. Check the working-tree status, and preserve any uncommitted changes that are not yours.
3. Reproduce the bug locally with synthetic data. If you cannot reproduce it, stop and report what you tried and what information is missing. Continue on a hypothesis only if I agree.
4. Find the root cause, not just the symptom. Cite the specific code path (`path:line`).
5. Propose a minimal fix and a regression test. For nontrivial fixes, or fixes that need any approval from `AGENTS.md` section 4 (including data repair), **wait for approval** before changing code.
6. Write the regression test first, and confirm it fails for the right reason.
7. Apply the minimal fix, and confirm the test now passes.
8. Run the related test suites and the available lint, type-check, and build steps.
9. Search for the same defect pattern elsewhere. Report any other occurrences; don't fix them in this change.

## Constraints
- Fix only this bug. List refactors and related issues as follow-ups.
- Never use production data or real credentials to reproduce the bug.
- If the bug is a security vulnerability, apply `.agents/security-engineer.md`, and keep exploit details out of public issues, commits, and PR descriptions.
- Do not commit or push unless asked.

## Output
- **Root cause:** what was wrong, and why
- **Fix:** changed files, with the reason for each
- **Regression test:** name and location, with evidence that it failed before the fix and passes after
- **Verification:** commands and their results (`PASS` / `FAIL` / `BLOCKED` / `NOT RUN`)
- **Other occurrences and follow-ups**
- **Next step:** `05-qa.md` or `code-review.md`, and whether `06-security.md` is needed
