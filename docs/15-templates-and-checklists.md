# Templates and Checklists

Every use case should produce a consistent set of documentation — not for compliance theater, but because the discipline of filling these out surfaces gaps and decisions that would otherwise surface at the worst possible time. Use these templates as working documents, not sign-off forms.

## Available Templates

- [AI Transformation Charter](../templates/ai-transformation-charter.md) — captures vision, scope, sponsors, governance, risk appetite, and funding for your AI program. Fill this out in Phase 0.
- [Use Case Intake Template](../templates/use-case-intake-template.md) — structures the information a use case needs before it enters the delivery pipeline.
- [Product Readiness Assessment](../templates/product-readiness-assessment.md) — evaluates whether a specific product is ready for AI delivery across all key dimensions.
- [Risk and Compliance Review](../templates/risk-and-compliance-review.md) — documents the risk assessment and compliance obligations for a use case.
- [Production Readiness Checklist](../templates/production-readiness-checklist.md) — the gate that a use case must clear before shipping to production.
- [AI Incident Runbook](../templates/ai-incident-runbook.md) — the step-by-step guide for incident response, tailored to AI-specific failure types.
- [AI Architecture Decision Record](../templates/ai-architecture-decision-record.md) — documents consequential architecture decisions, including alternatives considered and rationale.
- [AI Cost Model](../templates/ai-cost-model.md) — structures the cost estimate from pilot through production scaling.
- [Vendor Evaluation Template](../templates/vendor-evaluation-template.md) — a structured comparison framework for evaluating AI model providers and tools.

## Recommended Document Set Per Use Case

Keep these together for every AI use case. If any are missing at production time, that's a gate failure — not a documentation gap to fill later.

- Use case intake.
- Product and data readiness assessment.
- Architecture and data flow diagram.
- Security threat model.
- Privacy and compliance review.
- Evaluation plan and results.
- Cost estimate and model.
- Architecture decision records for key choices.
- Production readiness checklist.
- Runbook and support model documentation.
- Post-launch review notes.

## Minimum Approval Checklist

Every production launch requires documented approval from each of these owners:

- [ ] Business owner approved.
- [ ] Product owner approved.
- [ ] Architecture approved.
- [ ] Security approved.
- [ ] Privacy approved.
- [ ] Compliance approved where required by regulation or risk tier.
- [ ] Data owner approved.
- [ ] Operations approved.
- [ ] Cost owner approved.
- [ ] Launch decision documented (Go / No-go / Go with conditions).

## Evidence to Keep

These artifacts need to be retained — both for your own incident investigation and for regulators, auditors, and customers who may ask for them:

- Architecture diagrams and data flow diagrams.
- Data source inventory with classification and access rights.
- Model and provider approval records.
- Prompt and model versions at each deployment.
- Evaluation datasets and results.
- Security test results including adversarial tests.
- Privacy assessment and approvals.
- Compliance approval records.
- Monitoring dashboard screenshots or links at launch.
- Incident records with root cause and resolution.
- User training records (especially important in regulated environments).
- Periodic review notes and decisions.
