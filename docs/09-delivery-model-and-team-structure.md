# Delivery Model and Team Structure

AI enablement doesn't succeed with a single team working in isolation. Product, engineering, data, risk, security, compliance, and operations have to work together from discovery through production — and that collaboration needs structure, or it collapses into hand-offs and finger-pointing when something goes wrong.

## Operating Model Options

### Centralized AI Team

A central team owns most AI delivery, with product teams consuming what they build.

Works well when AI expertise is scarce and you need strong standardization early. The risks are real though: the team becomes a bottleneck, it loses touch with product context, and adoption tends to be slower because product teams have less ownership.

Best as a starting point, not a permanent state.

### Federated Product Teams

Product teams own their AI features end-to-end, operating within shared standards and on shared platforms.

Works well when your product organization is mature, engineering practices are strong, and you've already established governance and platform capabilities. The risk is inconsistent controls and vendor sprawl if the shared standards aren't enforced.

### Hub-and-Spoke Model

A central hub owns standards, platforms, model gateway, evaluation tools, governance, and enablement. Product team spokes own use cases, user experience, business outcomes, and production behavior.

This is the right model for most medium and large organizations. It captures the benefits of both centralization (consistency, reuse, shared platform investment) and federation (product ownership, speed, context). The governance overhead is manageable and the platform investment pays dividends at scale.

## Core Roles

| Role | Responsibilities |
| --- | --- |
| Executive sponsor | Funding, strategic alignment, risk acceptance |
| Product owner | Outcome, roadmap, user workflow, adoption |
| AI product manager | AI use case design, metrics, user value, responsible launch |
| Solution architect | Architecture, integration, non-functional requirements |
| Data scientist | Model development, experimentation, evaluation |
| ML engineer | Model serving, pipelines, deployment, monitoring |
| Data engineer | Data access, pipelines, quality, lineage |
| Software engineer | Product integration, UI, APIs, workflow logic |
| Prompt or conversation designer | Prompt behavior, interaction quality, user experience |
| Security architect | Threat model, controls, secure design |
| Privacy lead | Personal data review, privacy impact, retention |
| Compliance and risk lead | Regulatory interpretation, evidence, approvals |
| Legal counsel | Contract, IP, regulatory, and policy guidance |
| SRE and operations | Reliability, monitoring, incident response |
| Change manager | Training, communications, adoption |

## Minimum Team for a Pilot

A pilot can run leaner than production, but don't cut so much that the pilot fails to generate useful evidence. You need at minimum:

- Product owner.
- Technical lead.
- Software engineer.
- Data engineer or data owner.
- AI/ML specialist.
- Security representative (can be part-time for lower-risk pilots).
- Privacy or compliance reviewer (can be a structured review at a gate rather than full-time).
- Business subject matter expert.
- User representative.

Skipping the user representative is the most common mistake. Pilots that don't involve real users produce artifacts, not evidence.

## Production Team Requirements

Production AI needs long-term ownership — not "the team that built it" as a vague collective, but named individuals who are accountable for specific aspects:

- Product owner for business behavior and user outcomes.
- Engineering owner for application integration.
- Data owner for source data quality and access.
- Model owner for model behavior and lifecycle.
- Platform owner for shared AI services.
- Operations owner for reliability and incident response.
- Risk owner for compliance obligations.

## RACI

| Activity | Product | Engineering | Data | Security | Risk/Compliance | Legal | Operations |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Use case definition | A | C | C | C | C | C | I |
| Architecture design | C | A | C | C | C | I | C |
| Data access approval | C | C | A | C | C | C | I |
| Threat modeling | C | C | C | A | C | I | I |
| Evaluation design | A | C | C | C | C | I | I |
| Production deployment | C | A | C | C | C | I | C |
| Incident response | C | C | C | A/C | C | C | A |
| Periodic review | A | C | C | C | A/C | C | C |
| Vendor and contract review | C | C | I | C | C | A | I |

A = accountable, C = consulted, I = informed.

## Delivery Rituals

Delivery rituals aren't process for its own sake — they're the touch points that keep cross-functional teams aligned and surface problems before they become incidents:

- Use case intake review — is this use case ready to enter the pipeline?
- Weekly product delivery standup.
- Architecture and risk review at the design gate.
- Evaluation review before production approval.
- Production readiness review.
- Launch review (the day before or morning of launch).
- Post-launch quality and cost review (30 and 60 days after launch).
- Monthly portfolio governance review.

## Skills Development

Role-specific training closes faster than generic AI literacy programs. Tailor training to what each role actually needs to do.

| Audience | Training Topics |
| --- | --- |
| Executives | AI strategy, risk appetite, investment governance, responsible AI |
| Product teams | Use case design, metrics definition, responsible AI, user experience patterns |
| Engineers | AI integration patterns, security threats, evaluation approaches, LLMOps |
| Data teams | Data governance for AI, embeddings, feature pipelines, lineage |
| Security teams | Prompt injection, model threats, AI logging, tool safety, red teaming |
| Legal and compliance | AI regulations, vendor terms, evidence requirements, human oversight |
| Operations | Monitoring, incidents, cost management, model lifecycle |
| End users | Appropriate use, known limitations, feedback mechanisms, escalation paths |

## Scaling Practices

Once the operating model is established, these practices compound the investment:

- Build an AI community of practice where teams share what they've learned in production.
- Maintain reference architectures and reusable components in a discoverable place.
- Publish an approved model and tool catalog so teams don't evaluate the same options repeatedly.
- Run regular office hours for product teams who are earlier in their journey.
- Track delivery patterns, time-to-value, and lessons learned across use cases.
- Share production incidents and mitigations across the community — the most expensive way to learn is to repeat each other's mistakes.
