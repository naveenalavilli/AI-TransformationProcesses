# Security, Privacy, and Compliance

AI enablement introduces attack surfaces and control requirements that your existing security program probably doesn't cover yet. This isn't just about protecting model endpoints — it's about securing the entire stack: the product, the data flowing into prompts, the retrieval layer, the model outputs, the integrations those outputs feed into, and the operational logs you keep for audit.

The mental model shift is important. Security teams used to dealing with deterministic software need to account for systems whose behavior is probabilistic, context-dependent, and influenced by inputs that are much harder to validate than traditional API parameters.

## Security Principles

Start with these and you'll avoid the most common mistakes:

- Apply least privilege everywhere — not just to users, but to services, models, and tools. An AI agent that can read everything and write anything is a single prompt injection away from a serious incident.
- Treat prompts, completions, embeddings, and AI logs as potentially sensitive. They can contain PII, confidential business information, or behavioral patterns you'd rather not expose.
- Never rely on the model as the only security boundary. Models can be manipulated. Your controls need to exist at the infrastructure and application layers.
- Validate AI outputs before using them in downstream systems. An AI-generated value that feeds into a database query, an API call, or a business rule is an injection vector if you don't sanitize it.
- Separate read-only assistance from actions that change records. When AI can only read, mistakes are recoverable. When it can write, they often aren't.
- Make all material AI activity auditable. If something goes wrong, you need to reconstruct exactly what happened.

## AI Threats

| Threat | Description | Mitigation |
| --- | --- | --- |
| Prompt injection | Malicious input tries to override instructions or exfiltrate data | Instruction hierarchy, retrieval filtering, output validation, tool restrictions |
| Data leakage | Sensitive data appears in prompts, outputs, logs, or retrieval results | Minimization, redaction, access control, logging controls |
| Unauthorized retrieval | User receives content they should not access | Identity-aware retrieval, metadata filtering, permission checks |
| Model misuse | Users use AI for prohibited or harmful activity | Policy enforcement, monitoring, user terms, abuse detection |
| Hallucination | Model creates unsupported claims | Grounding, citations, confidence thresholds, human review |
| Tool abuse | Agent calls APIs or tools in unsafe ways | Tool allowlists, scoped permissions, approval steps |
| Supply chain risk | Model, package, plugin, or dataset is compromised | Vendor assessment, artifact validation, SBOM, dependency scanning |
| Training data poisoning | Malicious or low-quality data changes model behavior | Dataset governance, anomaly detection, trusted sources |
| Model extraction | Attackers try to copy model behavior or proprietary prompts | Rate limits, monitoring, prompt protection, contractual controls |
| Denial of wallet | Attackers generate excessive AI cost | Quotas, budgets, throttling, abuse detection |

## Privacy Considerations

Privacy obligations don't disappear when you add AI — in many cases they become more complex because AI systems process data in ways that are harder to audit and easier to misuse.

Key areas to address:

- Lawful basis for processing personal data in AI workflows.
- Consent and notice requirements when AI influences decisions about individuals.
- Data subject rights (access, deletion, correction) and how they propagate to embeddings, logs, and training data.
- Data minimization — does the AI actually need all the data it's receiving?
- Purpose limitation — data collected for one purpose can't quietly be repurposed for AI training without appropriate controls.
- Retention and deletion, including embeddings and audit logs.
- Cross-border transfer when using cloud-hosted models.
- Vendor subprocessors — your AI provider's subprocessors become your compliance exposure.
- Automated decision-making restrictions in jurisdictions like the EU.
- Human review and contestability for decisions that affect individuals.

## Compliance Considerations

The compliance landscape for AI is still evolving, but the obligations that apply depend on your geography, industry, customer contracts, and data types. Common areas:

- Data protection and privacy regulations (GDPR, CCPA, and equivalents).
- Financial services regulations where AI influences advice, credit, or risk scoring.
- Healthcare and life sciences regulations where AI touches clinical data or patient outcomes.
- Public sector and defense requirements around data sovereignty and approved infrastructure.
- Accessibility standards when AI changes how users interact with a product.
- Records retention and audit requirements for AI-influenced decisions.
- Consumer protection and transparency rules, including disclosure of AI involvement.
- Employment and hiring laws where AI screens or scores candidates.
- Export controls and sanctions where AI capabilities or data cross regulated boundaries.
- Sector-specific AI regulations, including the EU AI Act's risk tier classifications.

## Control Families

### Identity and Access

- Single sign-on and strong authentication for all AI service access.
- Role-based or attribute-based access control — both for users and for the AI services themselves.
- Service identity for AI components, not shared credentials.
- Fine-grained permissions at the retrieval and tool layer, not just the application layer.
- Privileged access management for anyone who can modify prompts, model configuration, or retrieval indexes.

### Network and Infrastructure

- Private endpoints wherever available. Keep AI traffic off the public internet where possible.
- Network segmentation between your AI services and other systems.
- Egress controls to prevent unexpected data leaving your environment.
- Encryption in transit and at rest, with customer-managed keys for sensitive workloads.
- Secure runtime configuration — secrets in a secrets manager, not environment variables or code.

### Application Security

- Input validation before data reaches the prompt construction layer.
- Output validation before AI-generated content reaches downstream systems.
- Secure API design with rate limiting at every layer.
- Secrets management — API keys and model credentials treated with the same care as database passwords.
- Dependency scanning including model libraries and AI orchestration frameworks.
- Secure coding review for any code that constructs prompts or handles model outputs.
- Red-team testing specifically for AI misuse scenarios.

### AI-Specific Controls

- Prompt versioning and approval — system prompt changes are behavioral changes, treat them as production deployments.
- System instruction protection to reduce prompt extraction risk.
- Retrieval source allowlisting — the model should only retrieve from approved, classified data sources.
- Tool allowlisting with scoped permissions for any agentic or tool-calling pattern.
- Content filtering for prohibited outputs, calibrated to your risk tier.
- Human approval for any material action AI recommends or takes.
- Evaluation against adversarial examples before production launch.
- Model and provider approval process — not every model from every provider is appropriate for every use case.

### Audit and Evidence

Audit logs for AI systems need to capture more than standard application logs. At minimum:

- User identity and session context.
- Request timestamp and product/use case context.
- Model name and prompt version used.
- Data sources retrieved and which documents were returned.
- Tool calls made and their results.
- Output delivered to the user.
- Human approvals or overrides.
- Safety filter results.
- Cost and latency metadata.

This combination lets you reconstruct any interaction for debugging, compliance evidence, or incident investigation.

## Shadow AI: The Governance Gap You Probably Have

Here's a problem most organizations have but few have solved: your employees are using personal ChatGPT, Claude, Gemini, and Copilot accounts to do work. They're pasting customer data, internal strategy documents, proprietary code, and confidential communications into tools that sit entirely outside your governance perimeter. They're doing this because the tools are useful and because your organization hasn't given them a sanctioned alternative.

This isn't a hypothetical. In 2025–2026 this is happening at scale in almost every enterprise, regardless of what your acceptable use policy says.

**Why it matters:**

- Data posted to consumer AI tools may be used for model training by the provider, depending on their terms. This applies to code, customer data, financial information, and anything else employees paste in.
- It creates regulatory exposure under data protection laws, customer contracts, and sector-specific regulations.
- When a security incident occurs, you'll have no visibility into what data left your environment through these channels.
- Proprietary methodologies and business information in prompts can be inferred from model behavior by sophisticated adversaries.

**How to find out how much you have:**

You probably have more than you think. Ways to measure:

- Network monitoring and DLP policies that can detect traffic to known AI provider domains. Many organizations find the volume surprising.
- Employee surveys during mobilization — ask directly, without judgment. People will tell you.
- Vendor data exposure notifications if a provider discloses that enterprise data was processed through consumer accounts.
- Code scanning for AI-generated code patterns that don't match your approved toolchain.

**What to do about it:**

Prohibition alone doesn't work. Employees use shadow AI because it's helpful and because there's no approved alternative. The durable solution is a combination of supply-side and demand-side response:

- Provide an approved alternative that's at least as capable as what they're using unsanctioned. If your approved tool is slower, has fewer features, or requires a procurement process, usage will route around it.
- Publish a clear approved tool catalog — specific tools, approved use cases, and data classifications that are permitted in each. Make it easy to find and easy to act on.
- Update your acceptable use policy to specifically address AI tools, including which data types are prohibited in which contexts. Generic "don't use unauthorized software" policies don't give employees enough guidance.
- Implement DLP controls at the endpoint and network level for the highest-risk data classifications — customer PII, financial data, regulated health information, source code.
- Create a reporting channel for employees who are unsure whether a specific use case is permitted. Friction around "is this allowed?" often pushes people toward using things first and asking forgiveness later.
- Communicate transparently about what you're monitoring and why. Employees who understand the business risk tend to make better decisions than those who feel surveilled without explanation.

## High-Risk Use Case Requirements

High-risk use cases — those affecting customers, finances, health, employment, legal matters, or safety — need formal review before production.

Required controls:

- Documented risk assessment.
- Privacy impact assessment.
- Security threat model.
- Named human accountable for outcomes.
- Explainability or rationale appropriate to the domain.
- Bias and fairness evaluation where relevant.
- Redress or escalation path for affected individuals.
- Audit logging.
- Monitoring and periodic review schedule.
- Legal and compliance approval.

## Vendor and Model Provider Assessment

Before committing to a model provider or third-party AI service, work through these:

- Data retention and training use terms. Does the provider train on your inputs? If so, under what conditions?
- Regional availability and data residency. Can they keep data in the regions your compliance obligations require?
- Subprocessors — who else handles your data downstream of the provider?
- Security certifications (SOC 2, ISO 27001, etc.) and how current they are.
- Incident notification terms. What are they contractually obligated to tell you, and how quickly?
- Service-level agreements for availability and latency.
- Model lifecycle and deprecation process. How much notice will you get before a model is retired?
- Logging and observability options. Can you get the audit data you need from their service?
- Encryption and key management options.
- Exportability and lock-in risk. What's your exit path if the relationship ends?
- Pricing and quota model, including what happens when you exceed limits.

## Security Checklist

- [ ] Threat model completed.
- [ ] Data classification completed.
- [ ] Identity-aware access control implemented.
- [ ] Prompt injection mitigations designed.
- [ ] Retrieval permissions enforced.
- [ ] Sensitive data redaction applied where required.
- [ ] Tool permissions scoped.
- [ ] Audit logging implemented.
- [ ] Security monitoring enabled.
- [ ] Shadow AI assessment completed and remediation plan in place.
- [ ] Approved AI tool catalog published.
- [ ] Vendor assessment completed.
- [ ] Incident response runbook created.
- [ ] Compliance evidence captured.
