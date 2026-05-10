# Cost, Funding, and FinOps

AI cost has a way of surprising organizations that don't plan for it. A pilot that runs on a small model with short prompts and twenty users can look financially viable. Scale it to five thousand users with longer context, more retrievals, and a more capable model, and the economics look completely different. The teams that avoid this surprise are the ones who start thinking about cost before the first line of code is written.

This section covers what drives AI cost, how to fund different stages of a program, and how to keep cost under control once you're in production.

## Cost Drivers

| Driver | Examples |
| --- | --- |
| Model inference | Tokens, requests, images, audio, video, embeddings |
| Model training or fine-tuning | Compute, storage, labeling, experiments |
| Data processing | ETL, document parsing, chunking, embedding generation |
| Storage | Vector indexes, logs, datasets, model artifacts |
| Infrastructure | GPUs, CPUs, memory, networking, private endpoints |
| Vendor services | Model APIs, orchestration tools, observability, labeling |
| Evaluation | Test generation, human review, red teaming, benchmark runs |
| Operations | Monitoring, support, incident response, model refresh |
| Compliance | Audits, evidence collection, legal review, certifications |
| Change management | Training, communications, adoption support |

The hidden costs are usually evaluation, compliance, and change management. Build them into your estimates from the start.

## Cost Metrics

Track cost at the unit that means something to your product. "We spent $40,000 on AI last month" is interesting but not actionable. "We're spending $0.18 per customer support case resolved" is a number you can optimize against and compare to alternatives.

Useful cost metrics depending on your use case:

- Cost per user (or active user).
- Cost per task completed.
- Cost per transaction or document.
- Cost per case resolved.
- Cost per generated response.
- Cost per evaluation run.
- Cost per tenant or customer.

Pick two or three that matter most for your product and track them from the pilot forward.

## Funding Model

Different stages of an AI program have different funding needs and different risk profiles.

| Stage | Funding Approach |
| --- | --- |
| Discovery | Central innovation or transformation budget |
| Pilot | Time-boxed product or portfolio funding |
| Industrialization | Product roadmap funding plus platform contribution |
| Scale | Shared platform funding and chargeback or showback |
| Optimization | FinOps savings reinvested into high-value AI capabilities |

Pilots should be time-boxed by design. A pilot with no end date and no exit criteria is a project that will run forever without producing useful evidence. Set a budget, set a timeline, and define what outcome would justify moving to industrialization.

## FinOps Controls

- Budget limits by product, environment, and team — hard limits that generate alerts (and ideally automatic throttling) before they're exceeded.
- Model gateway quotas at the request and token level.
- Rate limits to prevent runaway usage from loops, bugs, or abuse.
- Context size limits — longer prompts are more expensive, and many use cases don't benefit from the extra context.
- Cost dashboards that teams can see without needing to ask finance.
- Alerts for unusual spend patterns, not just absolute thresholds.
- Environment shutdown schedules for development and staging environments that don't need to run overnight.
- Model selection standards — not every task needs the most expensive model.
- Caching for repeated requests — identical or near-identical queries can often be served from cache at a fraction of the inference cost.
- Batch processing for non-interactive workloads where latency isn't the constraint.
- Prompt optimization passes before scaling — a prompt that works at 2,000 tokens in development might be reducible to 800 tokens without quality loss.
- Chargeback or showback reporting so product teams feel the cost of their choices.

## Cost Optimization Levers

Once you're in production and have real usage data, these are the levers that reliably improve unit economics:

| Lever | Description |
| --- | --- |
| Model tiering | Use smaller or cheaper models for simple tasks; reserve powerful models for cases that need them |
| Prompt compression | Remove unnecessary instructions, redundant context, and padding from prompts |
| Retrieval precision | Retrieve fewer, better chunks rather than large amounts of loosely relevant context |
| Caching | Reuse stable answers, embeddings, and intermediate results |
| Batching | Process non-urgent work in groups rather than request by request |
| Asynchronous design | Avoid expensive low-latency paths when the user doesn't need an immediate response |
| Routing | Select model based on task complexity — classify the request, then choose the appropriate model tier |
| Guardrails | Stop invalid or low-value requests before model invocation rather than letting them run |
| Fine-tuning | Reduce prompt length or improve task performance for high-volume, consistent task types |
| On-premises hosting | Economical for predictable high-volume workloads if your operations team can support it |

## Cost Risk Patterns

These are the cost surprises that come up repeatedly. Most of them are avoidable with planning:

- A pilot uses a powerful model and long prompts, then becomes too expensive when usage scales to production volume. Test your cost model at target volume before committing to an architecture.
- Teams log every token of every prompt and output with long retention periods. Logging costs accumulate quickly and most of it isn't needed for debugging or compliance.
- Vector indexes are rebuilt on a schedule without lifecycle management. Full index rebuilds are expensive — incremental updates and smart refresh policies are much cheaper.
- Autonomous or agentic workflows loop or retry excessively. A bug that causes an agent to retry ten times per request is ten times the intended cost.
- Evaluation runs aren't budgeted. Running your full evaluation suite frequently is expensive. Build evaluation cost into your operational budget.
- Vendor pricing changes aren't monitored. AI provider pricing changes more frequently than traditional software vendors. Assign someone to track this.
- AI cost is invisible inside platform spend. If your AI cost is buried in a shared infrastructure line, no one knows which products or features are expensive. Tag AI spend from day one.

## Benefits Realization

Writing a business case is the easy part. Actually closing the loop — proving that the AI investment delivered what you promised — is where most programs fall short. Benefits that aren't tracked tend to get claimed once and never revisited.

**Define outcomes before launch, not after.**

Before a use case goes into production, document:

- The specific metric you expect to improve.
- The current baseline value of that metric (measured, not estimated).
- The target improvement and the timeline to reach it.
- How the improvement will be attributed — separating AI impact from other changes happening simultaneously.
- Who is accountable for measuring and reporting it.

If you can't define a measurable baseline, you can't prove improvement. This is a forcing function: if the expected value isn't measurable, the use case may not be as well-defined as you think.

**Attribution methodology.**

Attributing a business outcome to a specific AI feature is harder than it sounds, especially in complex environments where process changes, headcount changes, and market changes are all happening at the same time. Approaches that work:

- **Controlled rollout:** Release the AI feature to a randomly selected subset of users or tenants while keeping a control group at baseline. Compare outcomes between the two groups.
- **Pre/post measurement:** Measure the outcome metric for at least four to six weeks before launch, then compare against the same period after. Control for seasonality and other known variables.
- **Activity-based tracing:** Track which actions, decisions, or outputs were AI-assisted, and measure outcomes for AI-assisted cases versus non-AI-assisted cases.
- **Proxy metrics:** Where the primary business outcome is hard to attribute directly, identify a proxy metric that the AI feature demonstrably influences (time saved per task, cases resolved per agent per day) and maintain the business case at the proxy level.

**Portfolio-level reporting.**

Individual use case benefits need to aggregate into a portfolio view for executives and sponsors to understand program value. Track across all production AI features:

- Total claimed benefits by category (cost savings, revenue, productivity, risk reduction).
- Benefits achieved versus business case forecast.
- Time from pilot approval to measurable production benefit.
- Cost versus benefit by use case — which investments are paying off?
- Use cases where benefits are not materializing and decisions needed.

Review this portfolio quarterly. Use it to inform prioritization decisions: where to invest more, where to hold, and where to shut down.

**Kill criteria.**

Define before launch the conditions under which you'll discontinue a use case if benefits don't materialize. "We'll keep running it and see" is not a plan. Examples of kill criteria:

- No measurable improvement in the target metric after 60 days of production operation.
- Cost per unit of benefit exceeds the threshold defined in the business case.
- User adoption falls below the level needed for the use case to generate value.
- Quality doesn't reach the acceptance threshold within two improvement cycles.

Shutting down a use case that isn't working isn't failure — it's good program management. It frees resources for use cases that will work.

## Cost Review Checklist

- [ ] Cost per unit defined.
- [ ] Usage forecast created at target volume, not pilot volume.
- [ ] Model choice justified against cost and performance.
- [ ] Context size estimated with realistic inputs.
- [ ] Evaluation cost included.
- [ ] Monitoring and logging cost included.
- [ ] Budget and quota configured.
- [ ] Cost owner named.
- [ ] Showback or chargeback approach defined.
- [ ] Benefits baseline measured before launch.
- [ ] Benefits attribution methodology defined.
- [ ] Portfolio reporting cadence established.
- [ ] Kill criteria documented.
- [ ] Optimization review scheduled (typically 60-90 days after launch).
