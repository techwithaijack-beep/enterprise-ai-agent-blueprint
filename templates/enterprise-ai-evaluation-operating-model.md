# Enterprise AI Evaluation Operating Model Template

Use this template to design how an enterprise AI system will be evaluated, governed, and improved over time.

This is not a benchmark sheet for a model demo.
It is an operating model for production teams running AI systems that affect customer experience, employee workflows, business decisions, or downstream operational work.

The goal is to answer a practical question:

**What evidence will tell us this AI system is safe enough, useful enough, and controllable enough to operate in production?**

This template is designed for:
- enterprise RAG applications
- copilots and assistants
- agent workflows with tools/actions
- omnichannel AI engagement systems
- document intelligence pipelines with LLM decision layers

---

## 1. System overview

### System / use case name
- **Name:**
- **Business owner:**
- **Technical owner:**
- **Primary users:**
- **Channels:**
- **Core workflows supported:**

### What the system actually does
Describe the practical job of the system in one paragraph.

Prompt:
- What user problem is this AI system solving?
- What is in scope vs out of scope?
- Where does it provide information only vs recommendations vs actions?

### Risk profile
Classify the operating risk.

- **Low risk** — informational support, reversible internal usage
- **Moderate risk** — workflow influence, moderate operational consequences
- **High risk** — customer-facing decisions, regulated processes, financial or material business impact

Notes:
- High-risk systems require stricter approval, release, and review gates.
- If external communication or system mutation is involved, document it explicitly.

---

## 2. Evaluation objectives

State what the evaluation program is supposed to prove.

### Primary evaluation objectives
Examples:
- answer quality is consistently acceptable for target user tasks
- retrieval is grounded in approved enterprise sources
- tool usage is accurate and policy-compliant
- the system handles low-confidence or ambiguous cases safely
- changes can be released without blind regressions
- business value can be measured, not merely assumed

### Non-objectives
List what this evaluation program is not trying to optimize.

Examples:
- maximizing benchmark scores unrelated to the real workflow
- optimizing for cleverness over traceability
- hiding escalations to force artificial containment metrics

---

## 3. Evaluation layers

Do not evaluate only the final answer.
Measure the system across layers.

### Layer A — Business outcome evaluation
Questions:
- Is the workflow actually improving a business outcome?
- Does the AI reduce time, cost, risk, or service friction?

Example metrics:
- containment / deflection rate
- average handling time improvement
- first-response time improvement
- case resolution rate
- conversion / completion rate
- operator productivity gain
- quality review pass rate
- cost per resolved interaction

### Layer B — User/task quality evaluation
Questions:
- Did the response or action actually solve the user task?
- Was the output clear, complete, and usable?

Example metrics:
- task success rate
- answer relevance
- completeness
- instruction adherence
- resolution usefulness
- user satisfaction score
- reviewer quality score

### Layer C — Grounding and retrieval evaluation
Questions:
- Did the system retrieve the right evidence?
- Were claims supported by approved sources?
- Was the source fresh enough and permission-appropriate?

Example metrics:
- retrieval hit quality
- citation correctness
- grounded answer rate
- unsupported claim rate
- stale-source usage rate
- permission violation rate

### Layer D — Tool and workflow execution evaluation
Questions:
- Did the system choose the right tool/workflow?
- Were actions successful, valid, and auditable?

Example metrics:
- tool selection accuracy
- tool execution success rate
- invalid action attempt rate
- workflow completion rate
- retry frequency
- rollback / recovery success rate

### Layer E — Policy and approval evaluation
Questions:
- Did the system obey access, policy, and approval rules?
- Were risky cases escalated correctly?

Example metrics:
- approval trigger precision
- approval trigger recall
- unauthorized action attempts
- policy violation rate
- exception override frequency
- escalation quality score

### Layer F — Operational reliability evaluation
Questions:
- Can the system operate predictably under production conditions?

Example metrics:
- latency percentile by workflow
- timeout rate
- error rate
- degraded-mode success rate
- uptime / availability
- queue backlog rate
- cost variance by request class

### Layer G — Release governance evaluation
Questions:
- Can we detect regressions before and after release?
- Are prompt/model/retrieval changes governed?

Example metrics:
- pre-release pass rate
- post-release regression rate
- rollback frequency
- time to detect quality drift
- release approval cycle time

---

## 4. Evaluation scenario inventory

Define the scenarios the system must handle well.

### Scenario table
Create a working list like this:

| Scenario ID | Scenario description | User type | Risk level | Must-pass? | Notes |
|---|---|---|---|---|---|
| EV-01 | | | | | |
| EV-02 | | | | | |
| EV-03 | | | | | |

### Recommended scenario categories
- common, high-volume standard requests
- ambiguous requests requiring clarification
- edge cases with incomplete information
- policy-sensitive requests
- low-confidence / conflicting-source cases
- tool failure / timeout cases
- retrieval miss cases
- adversarial or misuse attempts
- multilingual / regional phrasing variants if relevant

Rule:
Your scenario set should reflect real production traffic, not just neat demo questions.

---

## 5. Golden set / review set design

Define the evidence set used for structured evaluation.

### Golden set sources
- historical tickets or conversations
- known customer / employee workflow examples
- curated business scenarios from SMEs
- policy-sensitive edge cases
- failure cases from pilot logs
- retrieval challenge cases

### Golden set design notes
Document:
- who curated it
- how often it is refreshed
- how many samples exist by scenario class
- which items are must-pass vs informative
- whether labels come from SMEs, operations, or policy owners

### Recommended split
- **Core regression set** — must-pass cases for every major release
- **Risk set** — policy, compliance, or high-consequence cases
- **Exploration set** — broader cases for trend analysis and discovery
- **Live sampled review set** — production samples reviewed regularly

---

## 6. Scoring model

Use a scoring model that reflects the system’s real job.

### Example scoring dimensions
- factual correctness
- completeness
- groundedness / citation quality
- policy compliance
- tone / communication fit
- action validity
- escalation appropriateness
- workflow outcome success

### Suggested scoring scales
Use one of these consistently:
- binary pass / fail
- 0–3 maturity scale
- 1–5 reviewer score
- weighted composite score by workflow type

### Weighting guidance
Do not weight everything equally.

Examples:
- for regulated or high-risk workflows, policy compliance and escalation correctness may outweigh helpfulness
- for knowledge assistants, groundedness may matter more than stylistic polish
- for action-taking systems, tool validity may matter more than answer eloquence

### Example weighted view
| Dimension | Weight | Score | Weighted total |
|---|---:|---:|---:|
| Task success | 25% | | |
| Groundedness | 20% | | |
| Policy compliance | 20% | | |
| Tool/action validity | 15% | | |
| Completeness | 10% | | |
| User clarity | 10% | | |

---

## 7. Release gates

Define what must be true before changes go live.

### Change types to govern
- prompt changes
- model changes
- retrieval/index changes
- ranking changes
- tool integration changes
- approval-rule changes
- workflow orchestration changes

### Minimum release checks
- regression set pass threshold defined
- no increase in critical policy violations
- no increase in unsupported answer rate beyond tolerance
- tool/action success rate remains above threshold
- latency/cost stays within allowed operating band
- rollback path documented

### Example release gate table
| Change type | Offline eval required | Human approval required | Canary required | Rollback required |
|---|---|---|---|---|
| Prompt revision | Yes | Maybe | Recommended | Yes |
| Model swap | Yes | Yes | Yes | Yes |
| Retrieval pipeline change | Yes | Yes | Yes | Yes |
| Tool/action logic change | Yes | Yes | Yes | Yes |

---

## 8. Human review model

Define who reviews what, and when.

### Review roles
- business owner
- solution architect
- operations lead
- QA / evaluation analyst
- policy / governance owner
- domain SME

### Human review checkpoints
- pre-launch scenario review
- release candidate evaluation sign-off
- weekly sampled production review
- monthly trend / drift review
- incident review for severe failures

### Review prompts for human evaluators
Use prompts like:
- Did the output solve the user need?
- Was the answer properly grounded?
- Was any action or recommendation unsafe?
- Should the system have escalated instead?
- Would you trust this output in a real operating environment?

---

## 9. Telemetry and evidence capture

Evaluation collapses if the right evidence is not captured.

### Capture per request where appropriate
- request type / scenario class
- user / role context (appropriately privacy-controlled)
- prompt or prompt version
- model and parameters
- retrieved sources and ranks
- tool calls and outcomes
- approval triggers and outcomes
- final output
- latency, token usage, and cost
- reviewer decision if sampled
- downstream business outcome if available

### Minimum observability artifacts
- request logs
- trace or step-level execution view
- retrieval evidence log
- tool execution log
- approval audit trail
- release/version registry
- evaluation result history

---

## 10. Failure taxonomy

Classify failure modes so the team can improve systematically.

### Example failure categories
- incorrect answer
- incomplete answer
- unsupported claim / hallucination
- wrong source / weak citation
- stale knowledge usage
- unsafe recommendation
- policy violation
- missed escalation
- unnecessary escalation
- wrong tool selected
- tool execution failure
- workflow dead-end / loop
- latency breach
- cost anomaly
- poor user communication

### Incident severity example
- **SEV-1** — material business risk, compliance risk, unsafe external action
- **SEV-2** — major workflow failure, repeated production impact
- **SEV-3** — contained quality issue, workaround available
- **SEV-4** — low-impact or cosmetic issue

---

## 11. Thresholds and action rules

Define what happens when metrics move.

### Example thresholds
- grounded answer rate must remain above: ______
- policy violation rate must remain below: ______
- critical scenario pass rate must remain above: ______
- tool execution success rate must remain above: ______
- P95 latency must remain below: ______
- sampled production review pass rate must remain above: ______

### Example action rules
- if critical scenario pass rate drops below threshold, pause release
- if policy violations rise, trigger governance review
- if latency or cost spikes, revert or constrain workload routing
- if unsupported claim rate rises, investigate retrieval, prompting, and source freshness
- if escalation quality drops, retrain rules and reviewer guidance

---

## 12. Operating cadence

Evaluation is not a one-time test.
It needs a running cadence.

### Recommended cadence
#### Weekly
- review sampled production outputs
- inspect major failure categories
- review tool/action exceptions

#### Monthly
- evaluate drift trends
- refresh scenario inventory
- review threshold performance
- compare business KPI movement

#### Quarterly
- reassess golden set coverage
- review policy and approval design
- retire stale metrics
- align evaluation to new business priorities

---

## 13. Improvement backlog

Use evaluation outputs to drive implementation priorities.

| Priority | Issue / finding | Evidence | Recommended fix | Owner | Due |
|---|---|---|---|---|---|
| P1 | | | | | |
| P2 | | | | | |
| P3 | | | | | |

Prioritize issues that combine:
- high business impact
- repeated occurrence
- control-plane weakness
- feasible remediation

---

## 14. Executive summary template

Use this summary for leadership readouts.

### Current evaluation posture
- **System maturity:**
- **Confidence level:**
- **Primary risks:**
- **Strongest indicators:**
- **Weakest indicators:**

### What leadership should know
- Where the system is already reliable
- Where the system is still pilot-like
- What must improve before broader rollout
- What metrics should be watched at executive level

### Recommended next moves
- 30-day actions:
- 60-day actions:
- 90-day actions:

---

## 15. Practical guidance

### What strong enterprise AI evaluation usually looks like
- evaluation covers the whole operating system, not just answer quality
- high-risk scenarios are explicitly tested and gated
- retrieval, policy, tool use, and business outcomes are all visible
- release decisions are evidence-backed
- failures are categorized and turned into engineering work

### What weak evaluation usually looks like
- only a demo benchmark exists
- no one owns scenario curation
- business metrics are disconnected from quality metrics
- prompt/model changes ship without regression discipline
- failures are discussed anecdotally instead of measured systematically

---

## Suggested companion assets
- `templates/control-plane-assessment-scorecard.md`
- `templates/workflow-vs-agent-decision-matrix.md`
- `templates/non-functional-requirements.md`
- `checklists/production-readiness.md`
- `templates/pilot-to-production-plan.md`

## Monetization angle

This template can be used in:
- enterprise AI readiness reviews
- RAG evaluation workshops
- pilot-to-production governance programs
- evaluation/observability advisory engagements
- architecture discovery sessions with platform and operations teams
