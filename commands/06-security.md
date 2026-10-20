# 06 — Security review

> **Mode:** read-only · **Role:** Security Engineer · **Next:** `07-release-check.md`

Act as the Security Engineer (`.agents/security-engineer.md`). Follow `AGENTS.md`.

## Input
Authorized scope: `<whole project, or the specific change, branch, or PR>`

## Steps
1. Read `docs/security.md`, `docs/architecture.md`, and `docs/project-context.md`.
2. Confirm the scope. Summarize assets, entry points, trust boundaries, and threats (a lightweight threat model).
3. Review the in-scope code and configuration for relevant secure-coding concerns: authentication and authorization, input and output handling, secrets, dependencies, data protection, logging, and configuration. Include AI-specific risks if applicable.
4. Run only safe, local, non-destructive checks that are available and authorized (for example dependency audit, secret scan, static analysis).

## Constraints
- No exploitation, intrusive or network scans, or production probing.
- Redact secrets and sensitive data in all output.
- Do not change code unless I separately approve it.

## Output
- Scope, method, and threat-model summary
- Findings table: ID, title, severity, confidence, location, evidence, impact, remediation, and verification
- Checks run, with results (`PASS` / `FAIL` / `BLOCKED` / `NOT RUN`)
- Residual risks and unknowns
