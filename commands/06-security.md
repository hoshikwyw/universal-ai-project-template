# 06 — Security review

> **Mode:** read-only; `docs/security.md` updated only after approval · **Role:** Security Engineer · **Next:** `07-release-check.md`; for `Critical` / `High` findings, `bugfix.md`, then re-review

Act as the Security Engineer (`.agents/security-engineer.md`). Follow `AGENTS.md`.

## Input
Authorized scope: `<whole project, or specific step(s), branch, commit, or PR>`

## Steps
1. Read `docs/security.md`, `docs/architecture.md`, `docs/project-context.md`, and the security and privacy requirements in `docs/requirements.md`.
2. Confirm the scope and any exclusions. Summarize assets, entry points, trust boundaries, and threats (a lightweight threat model).
3. Review the in-scope code and configuration for:
   - authentication and authorization
   - input validation and output encoding
   - secrets handling
   - dependencies and lockfiles
   - data protection and retention
   - logging
   - configuration and CI/CD
   - AI-specific risks (prompt injection, tool permissions, data leakage), if applicable
4. Run only safe, local, non-destructive checks that are already available (for example a dependency audit, secret scan, or static analysis). If a tool is not installed, mark the check `NOT RUN`. Do not install tools without approval.
5. Re-check any previously reported findings that are in scope.

## Constraints
- No exploitation, intrusive or network scans, or production probing.
- Redact secrets and sensitive data in all output.
- Do not change code unless I separately approve it.

## Output
- Scope, method, and threat-model summary
- Findings table (`SEC-NNN`): title, severity, confidence, location, evidence, impact, remediation, and verification
- Checks run, with results (`PASS` / `FAIL` / `BLOCKED` / `NOT RUN`)
- Residual risks and unknowns
- Proposed updates to `docs/security.md`: threat model, security checks, and known risks

**Wait for my approval** before updating `docs/security.md`.
