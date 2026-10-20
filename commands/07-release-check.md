# 07 — Release readiness

> **Mode:** read-only · **Role:** Tech Lead, consulting QA Engineer and Security Engineer · **Next:** release (by a human), or back to `04-implement.md`

Act as the Tech Lead (`.agents/tech-lead.md`), applying `.agents/qa-engineer.md` and `.agents/security-engineer.md`. Follow `AGENTS.md`.

## Input
Release candidate: `<version, tag, branch, or list of steps included>`

## Steps
1. Compare the implementation against the approved acceptance criteria in `docs/requirements.md`.
2. Review the latest QA and security reports and confirm that their findings were resolved or accepted.
3. Collect the current build, lint, type-check, and test status, with evidence. Run the available checks if they have not been run on this exact revision.
4. Check deployment and rollback readiness: configuration, migrations, feature flags, monitoring, and the rollback procedure.
5. Check documentation: README and setup steps, `docs/` currency, changelog or release notes, and ADRs.

## Constraints
- Do not deploy, tag, publish, or modify infrastructure.
- Any check without evidence is `NOT RUN` and cannot support a `READY` verdict.

## Output
| Area | Status | Evidence / notes |
|------|--------|------------------|
| Acceptance criteria | | |
| Build / lint / type-check / tests | | |
| Open defects (by severity) | | |
| Security findings (by severity) | | |
| Deployment and rollback readiness | | |
| Documentation | | |

Then give the **verdict**: `READY` / `NOT READY` / `NEEDS VERIFICATION`, with a rationale, any blocking items, and accepted risks that need sign-off.
