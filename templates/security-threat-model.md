# Security Threat Model

Use case:

Product:

Review date:

Owners:

## 1. Scope

Describe the AI capability, system boundaries, deployment environment, and what is in and out of scope.

## 2. Architecture And Data Flow

- Entry points:
- Components:
- Data stores:
- External dependencies:
- Trust boundaries:

## 3. Assets And Sensitivity

| Asset | Classification | Owner | Notes |
| --- | --- | --- | --- |
|  |  |  |  |

## 4. Identity And Access

- User identity and authorization model:
- Service-to-service authentication:
- Privileged access controls:
- Tenant isolation approach (if applicable):

## 5. Threat Scenarios

| Threat | Attack Path | Impact | Likelihood | Risk (H/M/L) | Mitigation | Owner |
| --- | --- | --- | --- | --- | --- | --- |
| Prompt injection |  |  |  |  |  |  |
| Unauthorized retrieval |  |  |  |  |  |  |
| Data leakage in prompts/outputs/logs |  |  |  |  |  |  |
| Tool abuse / unsafe actions |  |  |  |  |  |  |
| Cross-tenant data exposure |  |  |  |  |  |  |
| Supply chain compromise |  |  |  |  |  |  |
| Denial of wallet / runaway cost |  |  |  |  |  |  |
| Model misuse / policy bypass |  |  |  |  |  |  |

## 6. Required Controls

- [ ] Input validation and sanitization
- [ ] Output validation and filtering
- [ ] Retrieval access enforcement
- [ ] Tool allowlist with scoped permissions
- [ ] Prompt and model version control
- [ ] Secrets management
- [ ] Audit logging
- [ ] Security monitoring and alerting
- [ ] Rate limits and quotas
- [ ] Fallback and rollback controls

## 7. Validation Plan

| Test | Method | Owner | Due Date | Status |
| --- | --- | --- | --- | --- |
| Prompt injection tests |  |  |  |  |
| Unauthorized access tests |  |  |  |  |
| Adversarial retrieval tests |  |  |  |  |
| Tool safety tests |  |  |  |  |
| Incident tabletop exercise |  |  |  |  |

## 8. Residual Risk And Decisions

Residual risks accepted:

Compensating controls:

Escalation path:

## 9. Approvals

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Security owner |  |  |  |
| Product owner |  |  |  |
| Engineering owner |  |  |  |
| Risk/compliance |  |  |  |
| Legal (where required) |  |  |  |

## 10. Review Cadence

Next review date:

Trigger events for re-review (for example model change, new tool, new data source, incident):
