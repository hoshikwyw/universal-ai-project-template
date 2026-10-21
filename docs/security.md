# Security Context

> **Status:** Draft <!-- Draft | Approved --> · **Last updated:** YYYY-MM-DD · **Owner:** TODO

<!--
Never paste secret values, tokens, connection strings, or real personal data into this file.
Describe *where* secrets live and *how* they are managed, not what they are.
-->

## Assets and data classification
| Asset / data | Classification | Where stored | Retention / deletion |
|--------------|----------------|--------------|----------------------|
| TODO | Public / Internal / Confidential / Regulated | TODO | TODO |

## Identities and access
- **User roles and permissions:** TODO
- **Authentication / session model:** TODO
- **Service-to-service authentication:** TODO
- **Admin / privileged access:** TODO

## Trust boundaries and entry points
- TODO (for example a public HTTP API, file uploads, webhooks, CLI arguments, or LLM prompts and tool calls)

## External integrations
| Integration | Data shared | Auth method | Notes |
|-------------|-------------|-------------|-------|
| TODO | TODO | TODO | TODO |

## Secrets management
- **Storage mechanism:** TODO (for example environment variables, a secret manager, or CI secrets; **do not paste values**)
- **Rotation:** TODO

## Threat model summary
| Threat | Affected asset | Existing control | Gap / action |
|--------|----------------|------------------|--------------|
| TODO | TODO | TODO | TODO |

## Security checks
| Check | Tool | Command | When run |
|-------|------|---------|----------|
| Dependency audit | TODO / unavailable | TODO | TODO |
| Secret scanning | TODO / unavailable | TODO | TODO |
| Static analysis (SAST) | TODO / unavailable | TODO | TODO |

## Testing authorization
- **Authorized test environment(s):** TODO
- **Explicitly out of bounds:** production systems, and third-party services unless written authorization exists

## Known risks and accepted exceptions
| Risk | Severity | Decision / owner | Review date |
|------|----------|------------------|-------------|
| TODO | TODO | TODO | TODO |

## Incident and vulnerability contact
TODO: who to notify, and how.
