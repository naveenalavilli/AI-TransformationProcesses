# Glossary and Decision Guides

Shared vocabulary matters. When a product manager, an ML engineer, a security architect, and a compliance lead are in the same room discussing an AI use case, they need to be using the same words to mean the same things. This glossary establishes that common ground.

The decision guides that follow are quick-reference frameworks for the most common judgment calls teams face during AI enablement.

## Glossary

| Term | Meaning |
| --- | --- |
| Agent | An AI system that can plan sequences of steps, use tools, call external services, and coordinate work toward a goal — rather than simply responding to a single prompt |
| AI enablement | The disciplined process of adding AI capabilities to products, platforms, workflows, and operating models in a governed, measurable way |
| AI orchestration | The logic layer that manages prompts, retrieval, tool calls, model routing, output validation, and workflow state across an AI interaction |
| Chunking | Breaking source documents into smaller pieces for indexing and retrieval. Chunk size, overlap, and metadata strategy significantly affect retrieval quality |
| Context window | The maximum amount of text (measured in tokens) that a model can process in a single interaction. Inputs and outputs together must fit within this limit |
| Embedding | A numeric vector representation of text, images, or other content, used for semantic search and similarity comparison |
| Evaluation dataset | A curated set of test cases used to measure model quality, typically including inputs, expected outputs, and scoring criteria |
| Fine-tuning | Training an existing model on additional examples to improve behavior for a specific task, style, or domain |
| Foundation model | A large, general-purpose model trained on broad data that can be adapted to many tasks through prompting, retrieval, or fine-tuning |
| Function calling / tool calling | A capability that lets a model invoke predefined functions or APIs and incorporate the results into its response |
| Generative AI | AI that produces text, code, images, audio, video, or other content, as distinct from AI that classifies, predicts, or scores |
| Grounding | Connecting model output to specific, verifiable source content rather than relying on the model's parametric knowledge |
| Guardrails | Constraints applied to model inputs or outputs to enforce policy compliance, content safety, or scope limitations — either as prompting patterns or as separate classification layers |
| Hallucination | A model output that is presented confidently but is unsupported, incorrect, or fabricated |
| Human-in-the-loop | A design pattern where a human reviews and approves AI output before any downstream action is taken |
| LLM-as-judge | Using a capable language model to evaluate the outputs of another model against a defined rubric. Useful for scaling human-quality evaluation across large test sets |
| LLMOps | Operational practices for managing large language model applications in production, including prompt versioning, evaluation pipelines, drift monitoring, and model lifecycle management |
| MCP (Model Context Protocol) | An open protocol for connecting AI models to external data sources and tools in a standardized way, enabling model-agnostic integrations |
| Memory (agent) | The mechanisms by which an agent retains information across steps or sessions. In-context memory is within the current prompt window; external memory uses a vector store or key-value store the agent can query |
| Model gateway | A controlled access layer that routes requests to approved model providers, enforces policies, applies rate limits, and captures telemetry across all model usage in an organization |
| Multi-agent system | A design where multiple AI agents collaborate, with some agents orchestrating others or working in parallel on different parts of a task |
| Prompt | The input to a model, typically including a system instruction layer, context (retrieved or provided), and the user's request |
| Prompt injection | An attack where malicious input attempts to override the model's intended instructions, cause it to ignore safety rules, or exfiltrate data |
| RAG (Retrieval-Augmented Generation) | A pattern where relevant content is retrieved from an approved data source and provided to the model as context before generation, grounding the response in current, authorized information |
| Reasoning model | A model variant that exposes its reasoning process (chain-of-thought) explicitly before producing a final answer, often producing better results on complex problems at the cost of higher latency and token usage |
| Red teaming | Structured adversarial testing designed to find harmful, insecure, or policy-violating model behaviors before they occur in production |
| Reranking | A post-retrieval step that reorders retrieved chunks by relevance using a more sophisticated model or scoring function, improving the quality of context provided to the generation model |
| Responsible AI | The set of practices — fairness, transparency, accountability, safety, privacy — that make AI systems lawful, ethical, and trustworthy |
| Structured output | Model output constrained to a defined format (JSON, XML, a specific schema), making it easier to use programmatically without parsing free text |
| System prompt | The instructions provided to a model before the user's input, defining the model's persona, scope, constraints, and behavior. Typically controlled by the application developer rather than the user |
| Temperature | A parameter controlling randomness in model outputs. Lower temperature produces more deterministic, consistent output; higher temperature produces more varied, creative output |
| Token | The unit of text that models process. Roughly 0.75 words in English. Pricing, context window limits, and latency are all measured in tokens |
| Vector database | A database optimized for storing embeddings and executing similarity search queries efficiently at scale |

## Multi-Jurisdiction Compliance Framework

If you operate across multiple countries or regulatory environments, you're managing overlapping compliance obligations that don't always align. A single AI feature can simultaneously be subject to the EU AI Act, GDPR, US sectoral regulations, and customer contract requirements — with different requirements in each.

The framework below doesn't replace qualified legal counsel. It gives your team a structured way to identify which regulations apply before you find out from a regulator.

**Step 1 — Map your exposure.**

For each use case, identify:

- **Where the users are located.** User location often determines data protection jurisdiction. A US company serving EU customers is subject to GDPR for those users regardless of where the product is hosted.
- **Where the data is processed.** Data residency and cross-border transfer restrictions depend on where processing happens, not just where data originates.
- **What industry you're in.** Financial services, healthcare, and public sector all carry additional AI-specific obligations beyond general data protection.
- **What the use case does.** Automated decision-making that affects individuals triggers different obligations than internal productivity tools.
- **What your customer contracts say.** Enterprise customers often impose compliance obligations that go beyond the regulatory minimum.

**Step 2 — Assess by regulatory area.**

| Regulation | Scope Trigger | Key AI Requirements |
| --- | --- | --- |
| EU AI Act | Use cases with EU users or EU-deployed systems | Risk tier classification; prohibited uses; transparency; human oversight for high-risk; conformity assessment for high-risk; registration |
| GDPR / EU data protection | Personal data of EU residents | Lawful basis; data minimization; deletion rights; automated decision-making restrictions (Art. 22); data protection impact assessment |
| UK AI (voluntary framework) | UK-based deployment | Currently principles-based; sector regulators (FCA, ICO, CQC) apply own AI expectations |
| US Executive Order 14110 + sectoral rules | Federal agencies, financial services, healthcare, critical infrastructure | Varies by sector; FDA for medical devices; OCC/CFPB for financial AI; EEOC for hiring; FTC for consumer protection |
| CCPA / US state privacy laws | California consumers (and growing number of US states) | Consumer rights; opt-out of certain automated decisions; disclosure requirements |
| ISO/IEC 42001 | Organizations seeking AI management system certification | AI governance structure; risk management; policies; evidence documentation |
| NIST AI RMF | US organizations, especially those working with government | Govern, Map, Measure, Manage framework; voluntary but increasingly referenced in procurement |
| Sector-specific (healthcare, finance, insurance) | Industry-specific | HIPAA for health data; FDA for clinical decision support; SEC/FINRA for financial advice; insurance commissioner requirements by state |

**Step 3 — Close compliance gaps.**

For each applicable regulation, work through:

- What controls does this regulation require that we don't currently have?
- What evidence do we need to demonstrate compliance?
- Who internally owns the interpretation and implementation?
- When does this obligation apply — at design time, before launch, or as an ongoing operation?
- What are the consequences of non-compliance, and how does that affect our risk acceptance decision?

**Step 4 — Maintain a compliance register.**

As the regulatory landscape evolves (and it's evolving quickly), maintain a living register:

- Which regulations apply to which use cases.
- The current compliance status for each.
- Open gaps and their owners.
- Upcoming regulatory changes that will require action.
- Evidence and documentation location.

Review this register before launching new use cases and when regulatory changes are announced.

## Model Selection Decision Guide

| Need | Consider |
| --- | --- |
| Fast pilot with common language tasks | Managed general-purpose model from a major provider |
| Strict data residency or air-gap requirement | Private cloud or on-premises hosted model |
| Low latency and high volume | Smaller model, aggressive caching, model routing, or local hosting |
| Domain-specific extraction or classification | Fine-tuned or specialized model |
| Answers grounded in enterprise knowledge | Retrieval-augmented generation with appropriate model |
| Complex multi-step reasoning | Reasoning model — expect higher cost and latency |
| Regulated high-impact decisions | Explainable model approach, human accountability, formal risk review |
| Strong cost constraints at scale | Model tiering, shorter prompts, retrieval optimization, caching |

## Deployment Decision Guide

| Constraint | Preferred Direction |
| --- | --- |
| Data cannot leave the facility | On-premises or air-gapped deployment |
| Data can leave the network but not the region | Regional private cloud deployment |
| Product already runs in cloud | Cloud-native AI service or private endpoint |
| Legacy system cannot be changed | AI sidecar or integration layer |
| Multi-tenant SaaS | Tenant-isolated retrieval with strict identity propagation throughout |
| Unpredictable usage patterns | Managed service with quotas and budget alerts |
| Predictable high-volume workload | Compare managed inference cost against self-hosted economics carefully |

## Build vs. Buy Decision Guide

| Choose Buy When | Choose Build When |
| --- | --- |
| The capability is a commodity | The capability differentiates your product |
| Speed to market matters more than customization | Control, IP ownership, or domain behavior matters |
| The vendor meets your security and compliance requirements | Vendor terms or deployment model are unacceptable |
| Internal skills are limited | Your team can build and operate it safely |
| The cost is acceptable at production scale | Unit economics favor owned infrastructure |

## RAG vs. Fine-Tuning

| Use RAG When | Use Fine-Tuning When |
| --- | --- |
| Knowledge changes frequently | Task behavior needs consistent, learned examples |
| Source citations are required | Output format or style needs to be highly specialized |
| Access control matters at runtime | The data has been approved and governed for training use |
| Users ask about enterprise-specific content | The model must classify or extract with high consistency at scale |

In practice, many production systems use both: RAG for knowledge and fine-tuning for behavior.

## Human Oversight Decision Guide

| Risk Level | Recommended Oversight |
| --- | --- |
| Low-risk productivity support (internal, reversible) | Human-informed — AI provides suggestions, user decides |
| Customer communication | Human-in-the-loop before anything is sent |
| Reversible operational routing or classification | Human-on-the-loop with monitoring and override capability |
| Financial, employment, legal, medical, safety, or rights-impacting output | Human-in-command — a named human is accountable for the decision |
| Prohibited or unlawful use | Don't build it |

## Common Decision Records to Keep

Good governance means documenting consequential decisions, not just making them. For each AI use case, keep records of:

- Why this use case was prioritized over alternatives considered.
- Why a specific model or provider was selected, including alternatives evaluated.
- Why the data used for training, retrieval, or inference is authorized for this purpose.
- Why a specific deployment environment was selected.
- Why the human oversight approach is sufficient for the risk tier.
- Why the cost model is viable at production volume.
- Why production launch was approved despite known limitations.

These records aren't bureaucracy — they're what you need when a regulator, auditor, customer, or executive asks why you made the choices you made.
