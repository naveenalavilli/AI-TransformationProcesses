# Testing, Evaluation, and Quality Gates

Traditional software testing proves that code does what the developer intended. For AI systems, that's necessary but not sufficient. You also need to prove that the system is useful, safe, honest, and economically viable — and that it stays that way as models evolve, data changes, and user behavior shifts.

The teams that run into trouble in production are usually the ones that cleared their sprint acceptance criteria but skipped the AI-specific evaluation work. Those are different things, and both matter.

## Test Types

| Test Type | Purpose |
| --- | --- |
| Unit tests | Validate deterministic code paths |
| Integration tests | Validate APIs, identity, data access, and workflows |
| Security tests | Validate access control, injection resistance, and abuse handling |
| Privacy tests | Validate minimization, redaction, retention, and deletion |
| Evaluation tests | Measure model output quality against representative scenarios |
| Adversarial tests | Challenge the system with malicious or unexpected inputs |
| Performance tests | Measure latency, throughput, and capacity |
| Cost tests | Estimate cost under realistic load |
| User acceptance tests | Validate workflow fit and adoption readiness |
| Operational tests | Validate monitoring, alerting, fallback, and incident response |

## Evaluation Dimensions

These dimensions define what "quality" means for an AI output. Not all of them apply to every use case — a code generation tool has different quality criteria than a customer communication assistant. Define which dimensions matter for your use case and what an acceptable score looks like before you start building.

| Dimension | Example Metrics |
| --- | --- |
| Accuracy | Correctness, exact match, classification accuracy |
| Groundedness | Output supported by approved sources |
| Relevance | Answer addresses the user's task |
| Completeness | Output covers required details |
| Consistency | Similar inputs produce acceptable similar outputs |
| Safety | Output avoids prohibited or harmful content |
| Privacy | Output avoids unauthorized personal or sensitive data |
| Fairness | Performance does not create unacceptable group impact |
| Explainability | Rationale is understandable and appropriate |
| Usability | Users can interpret, edit, and act on output |

## Evaluation Dataset

Your evaluation dataset is the foundation of everything else. Without representative test cases, your quality gates are decorative.

Create test cases that represent:

- Common successful workflows — the cases that should definitely work.
- Edge cases — unusual inputs that a minority of users will genuinely send.
- Ambiguous requests — where the right answer isn't obvious.
- Missing data — what happens when the retrieval returns nothing useful.
- Conflicting sources — when different documents say different things.
- Low-quality documents — scanned PDFs, poorly formatted inputs, incomplete data.
- High-risk user groups — scenarios where a wrong answer has higher consequences.
- Unauthorized access attempts — a user trying to retrieve information above their authorization level.
- Prompt injection attempts — malicious input designed to override instructions.
- Expected refusals — requests that should be declined, verified to be declined.
- Costly or long-context cases — inputs that stress your latency and cost model.

Each test case should include:

- Input.
- User role and authorization context.
- Data context (what's in the retrieval index at test time).
- Expected behavior.
- Acceptable answer criteria.
- Risk category.
- Evaluation method (automated, human, or both).

## Reference Thresholds

These are starting points, not universal requirements. The right thresholds depend on your use case, risk tier, and domain. A clinical decision support tool has different acceptance bars than an internal knowledge assistant. Use these as a calibration reference, validate them with domain experts, and adjust based on your evaluation results.

| Use Case Type | Metric | Starting Threshold |
| --- | --- | --- |
| Customer-facing knowledge assistant | Groundedness | >80% of outputs fully supported by retrieved sources |
| Customer-facing knowledge assistant | Hallucination rate | <5% of outputs contain unsupported factual claims |
| Customer-facing knowledge assistant | Relevance | >85% of outputs address the user's actual question |
| Internal knowledge assistant (employee-facing) | Groundedness | >75% |
| Internal knowledge assistant | Hallucination rate | <10% |
| Document extraction (structured fields) | Field accuracy | >95% for high-value fields |
| Document extraction | Confidence-threshold routing | Route to human review below 80% model confidence |
| Classification / routing | Accuracy | >90% on representative held-out test set |
| Classification | Precision / recall balance | Calibrate to cost of each error type in your domain |
| Customer-facing generation (drafts, summaries) | Safety filter pass rate | 100% — no prohibited content in any output |
| Customer-facing generation | Policy compliance | 100% — outputs consistent with organizational policies |
| Code generation | Security scan pass rate | 100% — no known vulnerabilities in generated code |
| Code generation | Test generation coverage | >80% branch coverage on generated tests |
| Agentic workflows | Step success rate | >95% of planned steps complete without error |
| Agentic workflows | Human override rate | Establish a baseline, monitor for drift |
| Any production use case | Latency (p95) | Within the response-time budget defined at design time |
| Any production use case | Fallback rate | <5% — if fallback triggers frequently, investigate the cause |

**How to set your own thresholds:**

1. Run your evaluation set against a baseline before launch.
2. Have domain experts review a sample and rate acceptability.
3. Define a minimum acceptable score based on that review.
4. Set a target score that you'll work toward over time.
5. Treat threshold misses as blocking issues for high-risk use cases, improvement priorities for lower-risk ones.

## Quality Gates

### Design Gate

Before anyone writes code, you should be able to answer these:

- What is the risk tier of this use case?
- What is the data flow and who can see what?
- Where does a human remain in the loop?
- How will quality be measured and what will "good" look like?
- What security and privacy controls are in place?

If you can't answer these before build, you'll be answering them under pressure after launch.

### Pilot Gate

After building but before scaling:

- Does it work in a realistic environment, not just a demo?
- What do the initial evaluation results actually show?
- What did real or representative users say when they tried it?
- What does it cost per task at realistic usage volumes?
- What are the known gaps and limitations?

### Production Gate

Evidence required to ship:

- Evaluation thresholds met.
- Security review completed.
- Privacy review completed.
- Compliance approval where required.
- Monitoring and alerting ready.
- Fallback and rollback tested.
- Support runbook ready.

### Post-Launch Gate

Thirty to sixty days after launch, review:

- Are production quality metrics matching what you saw in evaluation?
- What do incidents and user feedback reveal about failure modes you didn't anticipate?
- Is the cost tracking to forecast?
- Are your prompt and model versions still the right choices?
- What's on the improvement backlog?

## Human Evaluation

Automated scoring can tell you a lot, but some questions require human judgment — especially in domains where "correct" is nuanced or where the cost of a mistake is high.

When using human reviewers, have them assess:

- Correctness — is the factual content right?
- Usefulness — does this actually help the user?
- Missing context — is the answer complete?
- Unsupported claims — is the model asserting things not backed by sources?
- Tone and style — is the output appropriate for the audience?
- Policy compliance — does it stay within acceptable use boundaries?
- Safety concerns — anything harmful, misleading, or inappropriate?
- Required human action — is there something in this response that a human needs to do before it's sent?

Use multiple reviewers for high-risk domains and measure inter-rater agreement. Low agreement usually means your evaluation rubric needs to be more specific.

## Automated Evaluation

Automated evaluation can run continuously in CI/CD and on a scheduled basis, catching regressions before users do.

Examples that work well at scale:

- Golden dataset scoring against a fixed reference set.
- Retrieval precision checks — are the right sources being retrieved?
- Citation presence verification for RAG systems.
- Structured output validation against expected schemas.
- Toxicity and policy checks using a secondary classifier.
- Regression checks across prompt or model versions.
- Latency and cost checks against defined budgets.

An increasingly useful technique is **LLM-as-judge**: using a capable model (often a larger, more expensive model than the one in production) to evaluate the outputs of your production model against a rubric. This scales human-quality evaluation to large test sets. It works best when the evaluation criteria are explicit and the judge model is consistent — validate it against human judgments before relying on it as your primary evaluation signal.

## Red Teaming

Red teaming is structured adversarial testing — putting the system through scenarios designed to make it fail in ways that matter. It's not a one-time activity before launch; it should happen on a schedule and whenever significant changes are made.

Focus on:

- Prompt injection — can malicious input override the system prompt or exfiltrate data?
- Data exfiltration attempts — can a user extract information they're not authorized to see?
- Jailbreak attempts — can users bypass content filters or policy constraints?
- Unauthorized tool execution — for agentic systems, can a user trigger tool calls outside intended scope?
- Cross-tenant access — for multi-tenant systems, can one tenant access another's data?
- Harmful instruction requests — does the system handle requests for prohibited content consistently?
- Bias-sensitive scenarios — does the system perform consistently across user groups?
- Adversarial documents — does the system behave safely when retrieval sources contain manipulative content?

## Production Monitoring Signals

Evaluation doesn't end at launch. These signals tell you how your system is performing in the real world:

- User feedback ratings and free-text comments.
- Escalation rate — how often users seek human help.
- Human override rate — how often users reject or correct AI output.
- Refusal rate — how often the system declines requests (too high or too low can both signal problems).
- Fallback rate — how often the system can't answer and falls back to a default.
- Hallucination reports from users or reviewers.
- Retrieval miss rate — how often queries return no useful context.
- Latency distribution, especially p95 and p99.
- Error rate and error categorization.
- Cost per task tracked against forecast.
- Policy violation detections.
- Drift indicators — are any of these metrics trending in the wrong direction over time?

## Evaluation Checklist

- [ ] Representative evaluation dataset created.
- [ ] Risk-based metrics defined.
- [ ] Acceptance thresholds documented and approved.
- [ ] Human review rubric created.
- [ ] Automated tests integrated into CI/CD where feasible.
- [ ] LLM-as-judge or automated scorer validated against human ratings.
- [ ] Adversarial tests included.
- [ ] Cost and latency measured at realistic load.
- [ ] Regression process defined for prompt and model changes.
- [ ] Production monitoring signals configured.
- [ ] Post-launch review scheduled.
