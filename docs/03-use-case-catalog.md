# Use Case Catalog

This catalog describes the AI enablement opportunities that appear most frequently across legacy and current products. It's a starting point, not an exhaustive list — the most valuable use cases in your organization will be shaped by your specific users, data, regulatory environment, and operating model.

Use the catalog to accelerate discovery workshops and give stakeholders a concrete vocabulary for discussing AI opportunities. Don't use it to shortcut the actual discovery work.

## Use Case Prioritization Criteria

Before evaluating specific use cases, agree on the criteria you'll use to compare them. These are the questions that matter:

| Criterion | Questions |
| --- | --- |
| Business value | Does it grow revenue, reduce cost, reduce risk, or improve experience in a measurable way? |
| User value | Does it remove real friction from a real workflow, or does it add steps? |
| Feasibility | Are the required systems, data, and integrations actually accessible today? |
| Data readiness | Is the data accurate, authorized, current, and well-governed? |
| Risk | Could the output materially affect rights, safety, finances, employment, health, or compliance? |
| Explainability | Can users understand and challenge the result where it matters? |
| Operational fit | Can the organization support, monitor, and improve this in production? |
| Cost | Is the cost per task justified by the benefit, at production volume (not just pilot volume)? |

## High-Value Horizontal Use Cases

These use cases apply across industries and product types. They're often the right place to start because they have well-understood patterns, manageable risk profiles, and fast paths to demonstrable value.

### Knowledge Assistant

**What it does:** answers user questions using enterprise documents, policies, procedures, product manuals, and support knowledge — grounded in your organization's content, not model training data.

Common patterns: retrieval-augmented generation, semantic search, citation and source grounding, role-based access filtering.

**Benefits:**
- Faster employee onboarding.
- Reduced support burden as users can self-serve answers.
- Better policy adherence when guidance is easy to find.
- Institutional knowledge that survives employee turnover.

**Risks to manage:**
- Incorrect or confidently wrong answers.
- Stale content that hasn't been updated as policies change.
- Overreliance — users treating AI answers as authoritative when they should verify.
- Retrieval of confidential information by users without appropriate authorization.

**Controls:** source citations, access-aware retrieval, content freshness monitoring, disclaimers on non-authoritative answers, clear escalation to human experts.

### Customer Support Copilot

**What it does:** assists support agents with case summaries, next-best actions, knowledge suggestions, sentiment detection, and response drafting — keeping the agent in control while reducing cognitive load.

**Benefits:**
- Lower average handle time.
- Improved response quality, especially for newer agents.
- Faster onboarding and reduced training burden.
- More consistent case handling.

**Controls:** human review before any AI-suggested content is sent to customers, restricted tone and policy guardrails, PII redaction where appropriate, audit logging of generated suggestions and final responses.

### Document Intelligence

**What it does:** extracts, classifies, validates, summarizes, and routes documents — invoices, contracts, claims, forms, PDFs, emails, scanned files. Replaces the manual data entry and review steps that slow down business processes.

**Benefits:**
- Reduced manual data entry and the error rate that comes with it.
- Faster cycle times for document-dependent workflows.
- Improved compliance traceability.

**Controls:** confidence thresholds before automation, human review for low-confidence or high-value cases, document retention and redaction policies aligned with data governance, field-level validation against source systems.

### Workflow Automation

**What it does:** combines AI extraction, decision support, rules, APIs, and human approval to accelerate repetitive business processes without removing human accountability.

Common applications: intake triage, ticket routing, invoice matching, claims pre-review, compliance evidence collection, change request summarization.

**Controls:** segregation of duties preserved, human approval required for high-risk actions, idempotent operations to handle retries safely, rollback and compensation logic, complete audit trail.

### Developer Productivity

**What it does:** assists engineering teams with code search, documentation generation, test creation, migration support, dependency analysis, and incident response — particularly valuable for large or legacy codebases where institutional knowledge is thin.

**Benefits:**
- Faster modernization and refactoring.
- Better documentation coverage across the codebase.
- Reduced maintenance burden for systems that are hard to onboard onto.

**Controls:** code licensing checks (especially for open-source), secret scanning in generated code, secure coding review, approval process before AI-generated changes are merged.

## Product-Specific Use Cases

| Product Area | AI Opportunities |
| --- | --- |
| CRM | Lead scoring, opportunity summaries, customer next-best action, call analysis |
| ERP | Invoice matching, demand forecasting, procurement recommendations, anomaly detection |
| Healthcare | Clinical documentation support, coding assistance, care gap detection, operational forecasting |
| Financial services | Fraud detection, risk scoring, document review, regulatory surveillance |
| Insurance | Claims triage, policy comparison, loss estimation, underwriting support |
| Manufacturing | Predictive maintenance, quality inspection, scheduling optimization, safety monitoring |
| Retail | Personalization, inventory forecasting, pricing intelligence, customer service |
| Legal | Contract review, clause extraction, matter summaries, legal research support |
| HR | Job description drafting, employee support, workforce analytics, learning recommendations |
| IT operations | Incident summarization, alert correlation, root-cause assistance, change risk prediction |

## Legacy Product Modernization Use Cases

These are the opportunities that come up repeatedly when organizations look at their older systems with fresh eyes. The common thread is that AI can add value at the edges of a legacy system without requiring changes to the core.

| Legacy Challenge | AI Enablement Opportunity |
| --- | --- |
| Poor documentation | Generate system summaries from code, logs, tickets, and database schemas |
| Hard-to-use UI | Add natural language query, guided workflows, and explainable recommendations |
| Manual back-office process | Extract data, classify requests, and recommend next actions |
| Mainframe or monolith constraints | Add AI at the API, integration, or workflow layer without touching the core |
| Knowledge trapped in experts | Build knowledge assistants and expert review workflows |
| High defect rate | AI-assisted test generation, log analysis, and regression risk detection |
| Slow reporting | Natural language analytics and automated narrative summaries |

## Use Case Risk Tiers

Risk tier determines how much oversight, governance, and evidence is required before launch. Assign a tier at intake and revisit it if the scope changes.

| Tier | Description | Examples | Required Oversight |
| --- | --- | --- | --- |
| Low | Productivity support with limited business impact | Drafting internal notes, summarizing public documents | Basic review and logging |
| Medium | Operational decisions with reversible impact | Ticket routing, support suggestions, document classification | Human review capability, monitoring, defined controls |
| High | Decisions affecting customers, money, rights, safety, or compliance | Credit recommendations, hiring screening, clinical decision support | Formal risk review, explainability, named human accountability |
| Prohibited | Uses that conflict with law, policy, or ethics | Deceptive surveillance, unauthorized profiling, illegal discrimination | Blocked by policy — not a design decision |

## Use Case Intake Questions

Every use case proposal should be able to answer these before entering the delivery pipeline:

- What user problem does this actually solve?
- Who is the accountable product owner?
- What business outcome will measurably improve?
- What systems and data are required?
- What decisions or actions will the AI influence?
- What happens if the AI output is wrong — how bad is the worst case?
- What regulations, policies, contracts, or data restrictions apply?
- Is human review required, and if so, by whom and when?
- How will quality be measured in production?
- How will cost be measured per unit of value delivered?
- What is the fallback if the AI capability is unavailable?
