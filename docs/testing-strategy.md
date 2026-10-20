# Testing Strategy

> **Status:** Draft · **Last updated:** YYYY-MM-DD · **Owner:** TODO

<!--
Record what actually exists. If a level has no tooling yet, write "unavailable" rather than a guess.
Assistants will use these commands verbatim.
-->

## Scope and risk
- **Highest-risk workflows:** TODO
- **Recently changed or fragile areas:** TODO

## Test levels
| Level | Framework / tool | Command | Location | Runs in CI? |
|-------|------------------|---------|----------|-------------|
| Unit | TODO / unavailable | TODO | TODO | TODO |
| Integration | TODO / unavailable | TODO | TODO | TODO |
| End-to-end | TODO / unavailable | TODO | TODO | TODO |
| Static checks (lint / types) | TODO / unavailable | TODO | — | TODO |
| Accessibility | TODO / unavailable | TODO | TODO | TODO |
| Performance / load | TODO / unavailable | TODO | TODO | TODO |

## Environments and test data
- **Test environments:** TODO
- **Fixtures / seed data:** TODO
- **Test data policy:** synthetic data only. No production data, real personal data, or real credentials.
- **Required platforms / browsers / devices:** TODO

## Quality gates
<!-- Adjust to the project. These gates apply before merge or release. -->
- All required test levels `PASS` on the change
- No new lint or type errors
- Coverage does not decrease for changed code (target: TODO)
- No open `Critical` or `High` defects or security findings, unless explicitly accepted
- TODO: project-specific gates

## Flaky test policy
Treat a flaky test as a defect. Quarantine it with a linked issue and an owner, and fix it promptly. Never silently retry or delete it.

## Known testing gaps
- TODO
