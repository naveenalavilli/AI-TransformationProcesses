# Vendor Evaluation Template

Use this template to compare AI model providers and tooling vendors before committing to a selection. Fill it in for each candidate and review side-by-side. Document the final decision in an Architecture Decision Record.

## Document Metadata

| Field | Value |
| --- | --- |
| Use case or platform | |
| Evaluation date | |
| Evaluator | |
| Decision owner | |
| Decision date | |
| Chosen vendor | |

---

## Vendors Under Evaluation

| ID | Vendor / Provider | Product / Service |
| --- | --- | --- |
| A |  |  |
| B |  |  |
| C |  |  |

---

## 1. Data and Privacy

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Training data use | Does the provider train on customer inputs by default? Can it be disabled? What are the contractual terms? | | | |
| Data retention | How long does the provider retain prompts, completions, and metadata? Is this configurable? | | | |
| Data residency | In which regions is data processed and stored? Can region be restricted? | | | |
| Cross-border transfer | Does data leave the contracted region? Under what legal mechanism? | | | |
| Subprocessors | Who are the downstream subprocessors? Is the list current and contractually controlled? | | | |
| Data subject rights | Can customer data be deleted on request, including from model training? What is the process? | | | |

**Notes:**

---

## 2. Security

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Certifications | SOC 2 Type II, ISO 27001, CSA STAR, or equivalent? How current? | | | |
| Encryption | Encryption at rest and in transit? Customer-managed key option? | | | |
| Private connectivity | VPC endpoints, private link, or equivalent available? | | | |
| Penetration testing | Is pen testing conducted? Are results available to enterprise customers? | | | |
| Incident notification | Contractual obligation to notify of security incidents? What timeline and scope? | | | |
| Access controls | Can access be restricted to specific users, IP ranges, or network paths? | | | |
| Logging and observability | What logs are available to customers? Format, retention, export options? | | | |

**Notes:**

---

## 3. Compliance

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Regulatory coverage | Which regulations does the vendor claim compliance with (GDPR, HIPAA, FedRAMP, etc.)? Is documentation available? | | | |
| Data processing agreement | Is a DPA or BAA available? Does it meet your requirements? | | | |
| Sector-specific requirements | Does the vendor support your industry's specific requirements (financial services, healthcare, public sector)? | | | |
| Audit support | Will the vendor support customer audits? What evidence can be provided? | | | |
| EU AI Act alignment | How does the vendor support compliance with the EU AI Act (if applicable)? | | | |

**Notes:**

---

## 4. Model Capability and Quality

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Task performance | How does the model perform on your specific use case evaluation set? | | | |
| Context window | Maximum context length? How does performance degrade toward the limit? | | | |
| Structured output | Does the model support reliable structured output (JSON, schemas)? | | | |
| Tool / function calling | Quality and reliability of tool calling for agentic use cases? | | | |
| Multilingual support | Languages supported and quality in languages relevant to your users? | | | |
| Safety and content filtering | Built-in content filtering? Configurability? How does it interact with your use case? | | | |
| Reasoning quality | For complex multi-step tasks, how does reasoning quality compare? | | | |

**Notes:**

---

## 5. Operational Reliability

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| SLA | Uptime SLA? What is the credit or remedy if it is breached? | | | |
| Latency | P50 and P95 latency for your expected request size? How does it vary by region? | | | |
| Rate limits | Default rate limits? How are they increased? What happens when exceeded? | | | |
| Quotas | Default token and request quotas? Process for increasing? | | | |
| Support tiers | What support tiers are available? Response times for critical issues? | | | |
| Status and incident communication | Is a status page available? How are incidents communicated to customers? | | | |

**Notes:**

---

## 6. Model Lifecycle

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Deprecation policy | How much advance notice is given before a model is deprecated? What is the historical track record? | | | |
| Version pinning | Can you pin to a specific model version? For how long? | | | |
| Migration support | What support is available when migrating to a new model version? | | | |
| Changelog and release notes | Are model behavior changes documented? How are updates communicated? | | | |
| Model provenance | Is information about training data and methodology available? | | | |

**Notes:**

---

## 7. Pricing and Economics

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Pricing model | How is pricing structured (per token, per request, per user, subscription)? | | | |
| Estimated cost at pilot volume | Cost at your expected pilot usage level? | | | |
| Estimated cost at production volume | Cost at your expected production usage level? | | | |
| Cost predictability | Are there mechanisms to cap spend? How unpredictable is the cost under varying load? | | | |
| Committed use discounts | Are volume or committed use discounts available? At what thresholds? | | | |
| Price change history | Has the vendor changed pricing recently? What notice is given? | | | |
| Lock-in risk | What is the cost of migrating away from this vendor? What data or configuration is portable? | | | |

**Notes:**

---

## 8. Integration and Developer Experience

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| SDK availability | SDKs available in your required languages? Quality and maintenance status? | | | |
| API stability | How often does the API change? What is the versioning and deprecation policy? | | | |
| Documentation quality | Is documentation sufficient to build and troubleshoot without vendor support? | | | |
| Local testing support | Can the API be tested locally or in a sandbox environment? | | | |
| Monitoring and observability hooks | What telemetry does the API expose for cost, latency, and errors? | | | |

**Notes:**

---

## 9. Vendor Risk

| Criterion | Questions | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Financial stability | Is the vendor financially stable? Relevant funding status or public company metrics? | | | |
| Strategic alignment | Is this vendor likely to remain in this market for your planning horizon? | | | |
| Concentration risk | How dependent does this selection make you on a single provider? | | | |
| Export controls | Are there export control restrictions on this vendor's technology for your use cases or geographies? | | | |
| Contractual protections | What IP protections, liability terms, and indemnification are available? | | | |

**Notes:**

---

## 10. Summary Scorecard

Rate each vendor 1–5 on each dimension. 1 = major gap, 5 = strong fit.

| Dimension | Weight | Vendor A | Vendor B | Vendor C |
| --- | --- | --- | --- | --- |
| Data and privacy | | | | |
| Security | | | | |
| Compliance | | | | |
| Model capability and quality | | | | |
| Operational reliability | | | | |
| Model lifecycle management | | | | |
| Pricing and economics | | | | |
| Integration and developer experience | | | | |
| Vendor risk | | | | |
| **Weighted total** | | | | |

---

## 11. Decision and Rationale

**Selected vendor:**

**Primary reasons for selection:**

**Key risks accepted:**

**Conditions or commitments required before contract:**

**Alternatives considered and why they were not selected:**

**Escalation path if selected vendor fails:**

**Review date:** (typically 12 months, or when major renewal or pricing change occurs)
