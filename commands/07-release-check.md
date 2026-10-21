# 07 — Release readiness

> **Mode:** read-only · **Role:** Tech Lead, consulting the Project Manager and the QA, Security, and DevOps Engineers · **Next:** release (by a human); on `NOT READY`, back to `bugfix.md` or `04-implement.md`

Act as the Tech Lead (`.agents/tech-lead.md`). Apply the following roles:

- `.agents/project-manager.md`: scope and sign-off
- `.agents/qa-engineer.md`
- `.agents/security-engineer.md`
- `.agents/devops-engineer.md`: deployment and rollback readiness

Follow `AGENTS.md`.

## Input
Release candidate: `<version, tag, branch, or commit, plus the steps included>`
QA and security reports: `<paste them or link them, or "none">`

## Steps
1. Identify the exact revision under review (commit SHA), and confirm the working tree is clean. All evidence must refer to this revision.
2. Compare the implementation against the approved acceptance criteria in `docs/requirements.md`. Mark each in-scope `AC-` as met, not met, or not verified.
3. Review the QA and security reports for this revision. Confirm their findings were resolved or explicitly accepted.
4. Collect the build, lint, type-check, and test status. Run the available checks if they have not been run on this exact revision.
5. Check the definition of done (`AGENTS.md` section 6, plus any overrides in `docs/project-context.md`).
6. Check deployment and rollback readiness: configuration and secrets in place (names only, never values), migration order, feature flags, monitoring and alerts, and the rollback procedure.
7. Check documentation: README and setup steps, whether `docs/` is current, changelog or release notes, and ADR statuses.

## Constraints
- Do not deploy, tag, publish, or modify infrastructure.
- Any check without evidence is `NOT RUN` and cannot support a `READY` verdict.
- Any open `Critical` or `High` defect or security finding means `NOT READY`, unless I have explicitly accepted it.

## Output
| Area | Status | Evidence / notes |
|------|--------|------------------|
| Revision | | commit SHA |
| Acceptance criteria | | |
| Build / lint / type-check / tests | | |
| Open defects (by severity) | | |
| Security findings (by severity) | | |
| Definition of done | | |
| Deployment and rollback readiness | | |
| Documentation | | |

Then give:
- **Verdict:** `READY` / `NOT READY` / `NEEDS VERIFICATION`, with rationale
- Blocking items, and accepted risks that need sign-off
- Post-release checks to run after deployment (smoke tests, metrics, and alerts to watch)
