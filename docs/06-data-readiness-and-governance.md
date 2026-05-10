# Data Readiness and Governance

AI quality and risk are shaped more by data than by model choice. A poor retrieval index produces confidently wrong answers. Unauthorized data in a prompt creates privacy and compliance exposure. Biased training data embeds bias into every output. Poor data lineage means you can't investigate incidents or satisfy auditors.

Getting this right isn't glamorous, but it's the difference between a system that works in production and one that fails in ways you didn't anticipate.

## Data Readiness Questions

Before any AI system can touch a data source, someone needs to answer these:

- What data does this use case actually need?
- Who owns the data and who can approve its use?
- Is the data accurate, complete, current, and representative of the real use cases?
- Is it legally and contractually permitted to use this data for AI?
- Does it contain personal, sensitive, confidential, regulated, or customer-owned information?
- What retention rules apply — and do those rules extend to embeddings and logs?
- Can the users who will benefit from this AI capability see this data today?
- Should AI access be broader, narrower, or identical to current user access?
- How will data lineage and transformations be recorded?
- How will data quality issues be detected and corrected once the system is in production?

## Data Categories

| Category | Examples | AI Considerations |
| --- | --- | --- |
| Public | Public websites, published manuals, open datasets | Verify licensing and content freshness before indexing |
| Internal | Policies, procedures, tickets, project documentation | Enforce employee role-based access at the retrieval layer |
| Confidential | Strategy, financials, source code, contracts | Strong access control and logging; narrow the retrieval scope carefully |
| Personal data | Names, emails, identifiers, employee and customer records | Privacy impact assessment, minimization, retention controls |
| Sensitive data | Health, biometric, financial, children's data, protected classes | Strict controls, legal review, human oversight for decisions |
| Customer-owned data | Tenant data, uploaded documents, customer environments | Tenant isolation and contractual restrictions on use |
| Regulated records | Audit logs, medical records, financial records | Evidence retention, immutable audit trail, immutability requirements |

## Data Governance Controls

- Data ownership and stewardship defined for each source.
- Data classification applied to every data asset entering an AI system.
- Access approval workflow before new data sources are added to retrieval or training.
- Lineage and metadata management — you need to know where data came from and what happened to it.
- Data quality monitoring that detects degradation before it becomes a quality incident.
- Retention and deletion processes including downstream artifacts (embeddings, logs, cached responses).
- Consent and lawful basis tracking where personal data is involved.
- Data sharing agreements reviewed for AI use restrictions.
- Training data approval — not all data that the system has access to is appropriate for model training.
- Synthetic data review — synthetic data can embed the biases of the generation process.
- Redaction and tokenization for sensitive fields that don't need to be in the model's context.
- Audit logging for all data access through AI systems.

## Training, Retrieval, and Inference Data

Different AI activities use data differently, and the obligations that apply vary accordingly.

| Activity | Data Use | Key Controls |
| --- | --- | --- |
| Training | Model learns parameters from data | Rights, consent, anonymization, lineage, bias review |
| Fine-tuning | Model adapts to specific examples | Dataset approval, versioning, evaluation before use |
| Retrieval | Model receives selected context at runtime | Access control, source citations, freshness monitoring |
| Inference | User input and context sent to model | Minimization, logging, retention, provider terms review |
| Evaluation | Test sets measure quality and risk | Representative data, privacy-safe examples |

## Data Quality Dimensions

Poor quality on any of these dimensions degrades AI output quality and can introduce risk:

- **Accuracy:** does the data correctly reflect the real-world state it's supposed to represent?
- **Completeness:** are the required fields and records present?
- **Timeliness:** is the data current enough for the use case?
- **Consistency:** does the same entity have the same values across different source systems?
- **Uniqueness:** are records appropriately deduplicated?
- **Validity:** does the data conform to expected formats and constraints?
- **Representativeness:** does the data cover the full range of real-world cases, including edge cases and minority groups?
- **Bias and coverage:** are any important groups underrepresented in ways that would affect model performance for those users?
- **Traceability:** can you trace any data point back to its source?

## Data Minimization Pattern

The simplest privacy and security control for AI systems is to give the model only the data it actually needs for the task. Systems that are minimized by design are harder to misuse, cheaper to operate, and easier to govern.

Implement this systematically:

1. Define the exact information the model needs — not what might be useful, but what's necessary.
2. Remove irrelevant fields before data reaches the prompt construction layer.
3. Redact or tokenize sensitive values that the model doesn't need to see in their original form.
4. Retrieve only records the current user is authorized to access.
5. Limit context window usage — larger contexts cost more and introduce more surface area for data leakage.
6. Avoid storing raw prompts and outputs unless there's a specific, governed reason.
7. Apply retention rules to logs, embeddings, and cached content, not just source databases.

## Embeddings and Vector Stores

Embeddings deserve special attention because teams often treat them as opaque technical artifacts rather than governed data. They're not opaque — they encode information about source content and can be used to reconstruct or infer sensitive information.

Controls:

- Classify embeddings according to the classification of their source data. An embedding of confidential content is confidential.
- Store metadata alongside embeddings: source document, owner, classification, tenant, and refresh date.
- Enforce access control at retrieval time, not just at indexing time.
- When source content expires or is deleted (including by a data subject exercising deletion rights), delete the corresponding embeddings.
- Prevent cross-tenant retrieval for multi-tenant systems — metadata filtering alone is not sufficient for high-risk isolation requirements.
- Monitor index quality and stale content regularly. An index that hasn't been refreshed reflects the world as it was, not as it is.

## Data Readiness Checklist

- [ ] Data owner identified for each source.
- [ ] Data classification completed.
- [ ] Legal and contractual usage rights confirmed.
- [ ] Privacy impact assessed.
- [ ] Data quality measured against key dimensions.
- [ ] Access rules documented and tested.
- [ ] Retention and deletion requirements defined, including for embeddings and logs.
- [ ] Lineage and metadata available and maintained.
- [ ] Retrieval or training dataset versioned.
- [ ] Data refresh process defined with a cadence appropriate to how quickly the underlying information changes.
- [ ] Audit logging enabled for all AI data access.
