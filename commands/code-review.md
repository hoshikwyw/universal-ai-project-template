# Code review — Review a diff, branch, or PR

> **Mode:** read-only · **Role:** Tech Lead, plus the relevant engineering and security roles · **Next:** fix the findings with `04-implement.md` or `bugfix.md`, or merge (by a human)

Act as the Tech Lead (`.agents/tech-lead.md`) and apply its review checklist. Add the engineering role(s) for the changed areas. Add `.agents/security-engineer.md` if the change touches authentication, authorization, user input, sensitive data, dependencies, or CI/CD. Follow `AGENTS.md`.

## Input
Change to review: `<uncommitted diff, branch name compared with its base, commit range, or PR link>`
Intent / linked items: `<issue, STEP-, REQ- / AC- IDs, or "none">`

## Steps
1. Understand the intent from the linked items. If none are given, infer the intent from the diff, and state it.
2. Read the full diff, and enough surrounding code to judge it in context.
3. Review for:
   - **Correctness:** logic, edge cases, error paths, concurrency
   - **Scope:** matches the intent; no unrelated changes or debug leftovers
   - **Security:** input handling, authorization, secrets, data exposure
   - **Compatibility:** public APIs, persisted data, configuration, migrations
   - **Tests:** coverage of the new behavior; tests that would fail if the behavior broke
   - **Docs:** README, `docs/`, and ADRs updated where behavior or setup changed
   - **Readability and consistency:** with existing conventions
   - **Performance and operability:** obvious hotspots; logging and errors
4. Run the available lint, type-check, test, and build steps if they are safe and local. Otherwise mark them `NOT RUN`.

## Constraints
- Do not modify code. Suggest changes instead.
- Do not post comments to GitHub or any other external system unless asked.
- Every finding must point to a specific location and explain the concrete problem. Leave out style preferences that formatters and linters already enforce.

## Output
| # | Severity | Location | Finding | Suggested fix |
|---|----------|----------|---------|---------------|
| 1 | High | `path:line` | … | … |

Severity follows `AGENTS.md` section 5. Use `Info` for optional suggestions.

Then give:
- Checks run, with results (`PASS` / `FAIL` / `BLOCKED` / `NOT RUN`)
- What looks good (brief)
- **Recommendation:** `Approve` / `Request changes` / `Comment` (questions only), with a one-line rationale. Any `Critical` or `High` finding means `Request changes`.
