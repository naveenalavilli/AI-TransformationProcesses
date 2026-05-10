# Product and Portfolio Assessment

Not every product is ready for AI, and not every AI idea is worth pursuing. A structured assessment prevents the most common trap in AI programs: teams selecting attractive use cases that are blocked by poor data, brittle architecture, high compliance exposure, or operational immaturity — then discovering the blockers after months of build.

Do this work before committing to delivery. It's far cheaper to find blockers at the assessment stage than mid-pilot.

## Portfolio Segmentation

Start by understanding where each product sits in your portfolio. The right AI strategy depends on the product's importance, maturity, and trajectory.

| Segment | Description | AI Enablement Strategy |
| --- | --- | --- |
| Strategic growth products | High market or business importance, active investment | Invest in differentiated AI capabilities that create competitive advantage |
| Operational backbone | Critical to internal operations, high stability requirements | Focus on productivity, reliability, and decision support with conservative controls |
| Legacy stable products | Older systems with limited change capacity | Add AI through integration, workflow, reporting, or knowledge layers — avoid invasive changes |
| Products under modernization | Systems already being replatformed | Embed AI architecture into the modernization roadmap rather than treating it as a separate workstream |
| Sunset products | Nearing retirement | Avoid major AI investment unless the value is immediate and the business case is clear |

## Product Readiness Dimensions

For each product and use case combination, assess readiness across these dimensions:

| Dimension | Assessment Questions |
| --- | --- |
| Business fit | Is the use case aligned with product strategy and measurable business outcomes? |
| User workflow | Is there a clear user journey and a realistic adoption path? |
| Architecture | Can the product integrate with AI services safely and reliably without excessive rework? |
| Data | Is the required data accessible, accurate, current, and authorized for this use? |
| Security | Are identity, access control, secrets management, network, and logging mature? |
| Compliance | Are the applicable regulations and contractual restrictions understood? |
| Operations | Can the team monitor, support, and roll back AI functionality in production? |
| Team capability | Does the team have sufficient product, engineering, data, security, and AI skills? |
| Economics | Is the expected value larger than implementation and operating cost at realistic volume? |

## Product Archetypes

### Legacy Monolith

Tight coupling between UI, business logic, and data. Limited APIs. Manual deployments. Sparse tests and documentation. Heavy dependency on individual experts.

These systems need AI augmentation, not AI integration. Work at the edges — around the system, not inside it.

**Recommended AI patterns:**
- AI assistant connected to documentation, tickets, logs, and knowledge bases.
- Document automation that processes inputs and outputs around the monolith.
- API wrapper or integration layer that the monolith doesn't need to know about.
- Read-only analytics and summarization.
- A modern UI companion experience.

**Avoid early:**
- Deep changes to core transaction logic.
- Autonomous write actions without strong controls and rollback capability.
- Direct model access to production databases.

### SaaS or Cloud-Native Product

API-first architecture. Mature identity and observability. Faster deployment cadence. Easier integration with managed AI services.

These products can support more sophisticated AI patterns but come with their own risk profile.

**Recommended AI patterns:**
- Embedded copilots.
- Personalization.
- Semantic search.
- Recommendations.
- Agent-assisted workflow orchestration.
- Real-time classification or prediction.

**Key concerns:**
- Tenant isolation — one tenant's data must never appear in another tenant's AI context.
- Vendor data use — what does your AI provider do with the data your tenants send?
- Cross-region data movement and its compliance implications.
- Token and inference cost at scale — pricing that looks acceptable at pilot volume can be prohibitive at production volume.

### On-Premises Regulated Product

Strict data residency. Limited outbound connectivity. Customer-controlled infrastructure. Audit-heavy operations.

AI for these products is possible, but it requires a fundamentally different deployment architecture.

**Recommended AI patterns:**
- Locally hosted models where hardware and licensing permit.
- Private model endpoints.
- Retrieval over customer-controlled content.
- Offline evaluation pipelines.
- Explicit deployment and upgrade packages.

**Key concerns:**
- Patch management — who is responsible for keeping model software current?
- Hardware capacity — does the customer's infrastructure support the model's requirements?
- Model licensing — open-weight models often have commercial use restrictions.
- Customer-specific compliance evidence — each customer may need their own audit artifacts.
- Supportability across diverse customer environments.

### Hybrid Enterprise Platform

Mix of cloud services, on-premises systems, data warehouses, and third-party platforms. Complex identity and network boundaries. Multiple data owners.

**Recommended AI patterns:**
- Central model gateway for consistent policy and observability across environments.
- Enterprise retrieval platform with access-aware indexing.
- Event-driven integration to avoid tight coupling between AI and source systems.
- Policy-based access control enforced at the retrieval layer.
- Shared evaluation and monitoring service that aggregates quality signals across products.

**Key concerns:**
- End-to-end auditability across environment boundaries.
- Data classification consistency — the same data may be classified differently in different systems.
- Latency across network boundaries, which can make interactive AI features feel slow.
- Consistent policy enforcement when data crosses from one environment to another.

## Scoring Model

Use a 1–5 score for each readiness dimension. The scoring is only useful if people apply it consistently — use the anchor descriptions below as calibration.

| Score | Meaning | Typical Characteristics |
| --- | --- | --- |
| 1 | Major blocker | A fundamental constraint that prevents delivery without significant remediation work; not addressable within the pilot timeline |
| 2 | Significant gaps | Material gaps that will require dedicated effort to close; deliverable but risky without a clear remediation plan |
| 3 | Feasible with mitigation | Gaps exist but are addressable with reasonable effort; a clear mitigation plan should be in place before build begins |
| 4 | Ready with minor gaps | Small gaps that can be addressed during delivery without significant risk or rework |
| 5 | Strong readiness | No meaningful gaps; the dimension is unlikely to cause delivery problems |

**Scoring guidance by dimension:**

*Data readiness example:* Score 1 if the data doesn't exist or can't be accessed. Score 3 if the data exists but has quality issues, access gaps, or unclear usage rights that need resolution. Score 5 if the data is accessible, high quality, properly governed, and the legal basis for AI use is confirmed.

*Security example:* Score 1 if there's no meaningful identity or access control and production data would be directly exposed to model APIs. Score 3 if basic controls exist but AI-specific threats (prompt injection, retrieval authorization, audit logging) haven't been addressed. Score 5 if the security architecture covers AI-specific threats and controls are validated.

**Decision guidance:**

- High value + high readiness: prioritize. This is where you start.
- High value + low readiness: plan foundational investment first. Don't skip it.
- Low value + high readiness: consider only if cost is low and it creates platform learning.
- Low value + low readiness: reject or defer. Don't let sunk cost pressure you into this quadrant.

## Assessment Outputs

Each product assessment should produce enough information for sponsors and delivery teams to make confident decisions:

- AI opportunity summary.
- Current architecture summary with integration points identified.
- Data source inventory with quality, access, and rights status.
- Compliance and policy constraints, with open questions noted.
- Integration dependencies and complexity estimate.
- Risk tier.
- Cost estimate range at pilot and production volume.
- Readiness score by dimension.
- Recommended next step — proceed, invest in prerequisites, or defer.

## Portfolio Review Cadence

- Monthly during early mobilization, when the portfolio is taking shape.
- Quarterly once AI delivery is established.
- Before annual planning and funding cycles.
- When a major incident, regulatory change, or platform change affects multiple products.
