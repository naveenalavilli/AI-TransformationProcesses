# Implementation Patterns

Knowing you want to add AI to a product is a long way from knowing how. The patterns here are the building blocks — each one matches a specific situation and comes with the controls that make it safe to run in production. Real systems often combine two or three of these patterns, so read across them rather than treating each as a standalone recipe.

## Pattern 1: AI Sidecar for Legacy Products

If the core product is difficult or risky to change, don't change it. Instead, build an AI capability that wraps around it — connecting through APIs, database replicas, message queues, report exports, or file-based integrations.

This is the right first move for most legacy systems. Teams often spend months trying to figure out how to embed AI inside a monolith when the better answer is to leave the monolith alone entirely. A companion service, admin tool, browser extension, or workflow layer can deliver real value without touching the transaction core.

Good for: summaries, search, triage, recommendations, documentation assistance.

Controls:
- Start read-only. Don't route write actions through AI until you've built confidence in output quality and failure behavior.
- Use dedicated integration accounts with scoped permissions, not shared admin credentials.
- Log every AI-generated recommendation, including cases where the user ignored it.
- Test the integration against a realistic data copy before connecting to production data.

## Pattern 2: Embedded Copilot

An embedded copilot adds contextual AI assistance to an existing product workflow — inside a form, a case, a document, a record. Users get a suggestion, then decide what to do with it.

The key design principle is that the user stays in command. The copilot accelerates decisions; it doesn't make them. Keep the editing, undo, and reject paths obvious and fast.

Good for: drafting, summarizing, explaining, recommending next actions.

Controls:
- Make it visually clear which content was AI-generated. Users need to know what to verify.
- Always require human approval before any AI-suggested content is sent externally or committed to a record.
- Version prompts alongside your application code. A prompt change is a behavioral change.
- Capture user edits and rejections — this is your most valuable signal for improvement.

## Pattern 3: Retrieval-Augmented Knowledge Experience

When answers need to come from your organization's own knowledge — policies, procedures, product documentation, support history — RAG is the right pattern. The model doesn't need to know everything; it needs to know how to use what you retrieve for it.

The quality of your retrieval pipeline matters at least as much as the model. A great model with poor retrieval gives confidently wrong answers. Invest in chunking strategy, metadata, and access control before optimizing the model.

Good for: policy assistant, support knowledge, product documentation, engineering knowledge, compliance guidance.

Controls:
- Enforce access control at the retrieval layer, not just at the UI. A user should only ever receive context they're authorized to see.
- Always surface citations. Users need to know where an answer came from so they can verify it.
- Monitor content freshness. Stale documents produce stale answers, and users often can't tell the difference.
- When sources conflict or are missing, surface that uncertainty rather than letting the model synthesize an answer from incomplete context.

## Pattern 4: AI-Assisted Workflow Automation

Some workflows are a good candidate for AI-in-the-loop automation: AI extracts or classifies, business rules validate, and humans approve before anything consequential happens. This is different from full automation — you're using AI to accelerate and improve human-driven processes, not replace them.

The most common failure mode here is skipping the business rules validation step. Raw AI output feeding directly into downstream action is a reliability and compliance risk, even when the model's accuracy is high.

Good for: claims triage, invoice matching, procurement review, case management, compliance evidence collection.

Controls:
- Define confidence thresholds. Below a threshold, route to human review rather than proceeding automatically.
- Keep segregation of duties intact. AI should not extract data and approve the action in the same flow.
- Design operations to be idempotent. If something runs twice, the result should be the same.
- Maintain a complete audit trail: what the AI output was, what the business rules decided, and what the human approved.

## Pattern 5: Model Gateway

Once more than one team is building AI features, you need a model gateway. Without it, every team makes independent decisions about model providers, versions, logging, and rate limits — and you end up with sprawl that's expensive, insecure, and impossible to audit.

A model gateway centralizes access to approved models while giving teams enough flexibility to move quickly within defined boundaries. It's infrastructure, not bureaucracy.

Good for: enterprise standardization, cost control, security monitoring, vendor abstraction.

Controls:
- Authenticate every request. No anonymous model access.
- Enforce a model allowlist. Teams should choose from approved models, not any model available from a provider.
- Apply data classification policy at the gateway — certain data classifications should be blocked from certain providers entirely.
- Set quotas and budgets by team, product, and environment.
- Log enough to reconstruct what was sent, to which model, from which service, at what cost.

## Pattern 6: Private Knowledge Boundary

For regulated workloads, multi-tenant SaaS, or customer-specific AI experiences, standard retrieval isn't enough. You need tenant isolation baked into the retrieval architecture — not enforced by application-layer filtering, but structurally impossible to breach at the storage level.

The key risk this pattern addresses is cross-tenant leakage: tenant A's content appearing in tenant B's response. This can happen in subtle ways — shared embedding spaces, insufficient metadata filtering, or misconfigured access rules — which is why structural isolation matters more than query-time filters.

Good for: SaaS products, customer-specific knowledge bases, regulated client data.

Controls:
- Use tenant-specific encryption keys where required.
- Test cross-tenant isolation explicitly. Don't assume it works — verify it with adversarial test cases.
- When content is deleted by a customer, propagate deletion to their embeddings and any associated metadata.
- Audit retrieval access by tenant, not just by user.

## Pattern 7: Human Review Queue

Some AI outputs are too important or uncertain to deliver directly to users. Route them to a human reviewer who can approve, edit, reject, or escalate before any downstream action happens.

The review queue is also one of your best evaluation tools. Reviewer decisions, corrections, and escalation patterns tell you where your model or retrieval is failing and where it's performing well. Capture this data systematically.

Good for: contract review, medical, legal, financial, or compliance support, high-value transactions, customer communications.

Controls:
- Reviewers need to be authorized for the content they're reviewing — don't let review bypass access controls.
- Track review decisions in your audit log alongside the original AI output.
- Define escalation paths for cases reviewers can't resolve.
- Set service-level targets. A review queue that takes three days to clear isn't helping the workflow.

## Pattern 8: AI Feature Flag and Rollback

Every AI feature in production should be releasable and disableable without a code deployment. Model behavior can degrade unexpectedly — from model provider updates, data changes, or simply cases the system hadn't encountered before. When that happens, you need to turn it off fast.

Feature flags also enable progressive rollout: start with internal users, then a small percentage of real users, then broader. This gives you real production signal before full exposure.

Controls:
- Build the kill switch before launch, not after an incident.
- Design a meaningful fallback experience. Turning off AI shouldn't break the product — users should see something useful.
- Tie your monitoring alerts to your feature flag system so an alert can trigger automatic containment.
- Version your prompt and model configuration alongside your feature flags so a rollback restores a known-good configuration, not just known-good code.

## Pattern 9: On-Premises Model Appliance

Some customers or regulatory environments require the AI to run entirely inside customer-controlled infrastructure. That means packaging the model runtime, orchestration layer, retrieval indexes, and monitoring into a deliverable that can be deployed, updated, and supported without cloud connectivity.

This is operationally demanding. Many teams underestimate what it takes to maintain model currency, manage hardware, and provide a supportable deployment across dozens of customer environments. Be honest about this cost before committing to it.

Controls:
- Sign all artifacts. Customers need to verify that what they're running is what you intended to ship.
- Plan model updates as a product release process. Customers can't just pull from a managed endpoint.
- Track model licensing carefully. Open-weight models often have commercial use restrictions.
- Provide hardware sizing guidance. A model running on undersized hardware will be slow and unreliable.

## Pattern 10: AI Analytics and Decision Support

Not all AI needs to act. For many use cases, the goal is to help humans make better decisions — faster, with more context, and with AI surfacing patterns they wouldn't spot manually. Forecasting, anomaly detection, risk scoring, and narrative explanations all fall here.

The critical design principle is that the human owns the decision. AI provides the evidence and recommendation; the user evaluates it and acts. Don't hide uncertainty — surfaces confidence levels, data gaps, and the reasoning behind recommendations.

Controls:
- Make the evidence visible. Users should be able to trace a recommendation back to its sources.
- Monitor for bias and performance drift across user groups and over time.
- Separate the AI recommendation from the human decision in your audit log.

## Pattern 11: Agentic AI and Multi-Agent Systems

Agentic AI is different in kind from the patterns above. An agent doesn't just generate a response — it takes a sequence of steps, calls external tools, maintains state across turns, and may spawn sub-agents to complete parts of a task. The model is acting in the world, not just describing it.

This creates capabilities that simpler patterns can't match: long-horizon task completion, autonomous research, multi-step workflows without constant human prompting. It also creates failure modes that don't exist in stateless inference — failure modes that compound with each step.

**When to use agentic patterns:**
Use them when the task genuinely requires dynamic planning, multiple tool calls, or coordinating work across systems that can't be captured in a single prompt-response exchange. Don't use them for tasks that can be solved with a well-designed RAG retrieval or a simple workflow automation — agentic overhead adds cost, latency, and complexity that simpler patterns don't carry.

**Architecture elements:**

The core of any agent is the agent loop: plan, act, observe, update. Around that loop, you need:

- **Tool registry:** a defined, versioned list of tools the agent is allowed to call, with scoped permissions for each. Agents should not have access to every available API — only what they need for the task.
- **Memory:** in-context memory (what's in the current prompt window) degrades as conversations grow long. External memory — a vector store or key-value store the agent can query — lets it recall context from earlier steps or prior sessions without bloating the prompt.
- **Approval checkpoints:** points in the workflow where the agent must pause and get human approval before proceeding. These are especially important before any irreversible action — sending an email, executing a transaction, modifying a record.
- **Budget limits:** maximum steps, maximum tool calls, maximum wall-clock time, maximum cost. Without these, an agent that gets confused can loop indefinitely or generate enormous costs before anyone notices.
- **Trace log:** every step the agent takes, every tool it calls, every decision it makes, recorded in a format you can reconstruct later for debugging, auditing, and evaluation.

**Multi-agent patterns:**

When a task is too large or complex for a single agent, you can split it across multiple agents:

- **Orchestrator + workers:** a planning agent breaks down a task and delegates subtasks to specialized worker agents. The orchestrator doesn't do the work; it coordinates.
- **Peer agents:** independent agents work in parallel on different parts of a problem and return results to a human or a summarizing agent.
- **Supervisor patterns:** a supervisor agent monitors worker output and can redirect, retry, or escalate.

Multi-agent systems multiply both capability and risk. A mistake by a worker agent can propagate to the orchestrator's next decision. Test the coordination layer thoroughly.

**Agentic failure modes — the ones that hurt:**

- **Infinite loops:** the agent gets stuck in a retry cycle, burning tokens and time without making progress. Budget limits and step caps are the primary defense.
- **Compounding hallucinations:** each step builds on the output of the previous one. A small hallucination in step 2 becomes a confident wrong conclusion by step 7. Validate intermediate outputs, not just final ones.
- **Hallucinated tool calls:** the agent invents tool names or parameters that don't exist, then treats the error response as real information and continues confidently. Strict tool allowlisting catches most of these.
- **Scope creep:** the agent interprets its task broadly and takes actions the user never intended. Start with narrow, explicit task definitions and expand carefully.
- **Latency amplification:** each tool call adds latency. A workflow that calls eight tools sequentially could easily take 30 seconds or more. Design for acceptable latency before optimizing for capability.

**Controls:**

- Tool allowlist with scoped permissions per agent. No open-ended API access.
- Human approval required before irreversible actions. Define "irreversible" explicitly for your domain.
- Hard limits on steps, cost, and wall-clock time — not soft limits that can be overridden.
- Sandboxed execution for any code the agent writes or runs.
- Full trace logging in a structured format. You need to be able to reconstruct exactly what happened.
- Adversarial test cases: what happens if the agent receives malicious content from a tool response? What happens if a tool returns unexpected output?

## Pattern 12: Prompt Engineering and Governance

Prompts are production code. They determine how your AI system behaves, and changes to them can have significant behavioral consequences — yet many teams treat prompts as informal configuration managed in a spreadsheet or committed to a config file with no review process. That's how you end up with quality regressions you can't trace.

**System prompt architecture:**

Production prompts are rarely a single block of text. A layered architecture gives you control at each level:

- **Global policy layer:** instructions that apply to every request in every product — prohibited behaviors, safety rules, organizational values. This layer is centrally owned and rarely changes.
- **Product context layer:** instructions specific to this product and use case — persona, scope, tone, what the AI is and isn't authorized to do. Product teams own this layer.
- **Task instructions:** prompt components that vary by task type within the product — different instructions for summarizing versus answering questions versus extracting fields.
- **User context:** dynamic data injected at runtime — the user's identity, role, relevant account details, current workflow state. This layer should never contain sensitive data the user isn't authorized to see.

Keeping these layers separate makes it much easier to update one without breaking another, and to understand which layer is responsible when behavior is unexpected.

**Versioning and approval:**

Treat every change to a production prompt as a change to production code — which means it needs version control, review, and evaluation before deployment. At minimum:

- Store prompts in version control alongside your application code.
- Require evaluation against a representative test set before any prompt change goes to production.
- Tag prompt versions in your audit logs so you can reconstruct which prompt version was in use for any given interaction.
- Maintain a rollback path: if a new prompt version causes a regression, you need to restore the previous version quickly without a full deployment cycle.

**Protecting system prompts:**

System prompts often contain proprietary instructions, business logic, and behavioral rules that you don't want exposed. Users can and do attempt to extract them — through direct requests, jailbreak patterns, or indirect probing. Mitigations:

- Never instruct users or the model to repeat the system prompt verbatim.
- Design system prompts to be robust to extraction attempts — even if someone extracts part of the prompt, the complete behavioral picture shouldn't be reconstructable.
- Monitor for prompt extraction patterns in your request logs.
- Separate proprietary retrieval content from the system prompt itself; use retrieval access control rather than embedding sensitive instructions in the prompt.

**Prompt drift:**

One of the most underappreciated operational risks in production AI is prompt drift: the same prompt produces meaningfully different behavior after a model provider updates the underlying model. This happens without any change on your side, and often with minimal notice.

- Run your evaluation set on a schedule, not just when you deploy changes. If evaluation scores drop without a code change, suspect a model update.
- Subscribe to provider changelogs and model version announcements.
- When a provider releases a new model version, test it against your evaluation set before it becomes the default in your environment. Use version pinning where available.
- Include prompt regression tests in your CI/CD pipeline, not just functional tests.

**Prompt library management:**

As an organization scales AI across products, you'll develop reusable prompt components — standard safety instructions, formatting patterns, extraction schemas, citation styles. Without a library, teams rebuild these independently and inconsistently.

A prompt library doesn't need to be complex: a centrally maintained repository of reviewed, versioned prompt components that teams can import and compose. The governance requirement is that changes to shared components go through review before any team's production system can consume them.
