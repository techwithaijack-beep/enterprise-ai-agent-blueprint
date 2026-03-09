# Enterprise AI Control Plane Assessment Scorecard

Use this scorecard to assess whether an enterprise AI solution is still a pilot/demo pattern or is ready to operate as a governed production system.

It works well for:
- architecture workshops
- readiness reviews
- proposal discovery sessions
- internal governance checkpoints
- partner/customer advisory engagements

## How to use

Score each dimension from **0 to 3**:
- **0 = not in place**
- **1 = partially defined / ad hoc**
- **2 = implemented but inconsistent or incomplete**
- **3 = production-ready and operationalized**

At the end:
- total the scores
- note the top 3 gaps
- define a 30/60/90-day improvement plan

---

## 1. Business scope and ownership

### What good looks like
The use case is clearly scoped, owned, and linked to measurable business value.

### Scoring guide
- **0** — No clear owner, no success criteria, broad or vague use case
- **1** — Business intent exists, but scope and ownership are weak
- **2** — Owner, scope, and KPIs are defined, but governance is inconsistent
- **3** — Clear owner, operating model, KPI baseline, target outcomes, and review cadence

### Evidence to look for
- named business owner
- in-scope / out-of-scope definition
- KPI baseline and target values
- escalation/support ownership

### Notes
- Current state:
- Gaps:
- Actions:

---

## 2. Knowledge layer quality

### What good looks like
Knowledge sources are curated, versioned, permission-aware, and fit for grounded enterprise use.

### Scoring guide
- **0** — Retrieval relies on unmanaged or unclear sources
- **1** — Some sources exist, but freshness/ownership/quality are weak
- **2** — Sources are organized and somewhat governed, but not consistently measured
- **3** — Sources have owners, refresh rules, metadata standards, permissions, and evaluation coverage

### Evidence to look for
- source registry with owners
- freshness cadence
- metadata taxonomy
- document lifecycle handling
- retrieval evaluation set

### Notes
- Current state:
- Gaps:
- Actions:

---

## 3. Retrieval trust and grounding

### What good looks like
The system retrieves relevant evidence reliably and exposes provenance to downstream users or systems.

### Scoring guide
- **0** — No citation/provenance, no retrieval evaluation
- **1** — Basic retrieval works, but quality is unstable or hard to verify
- **2** — Retrieval metrics and citations exist, but there are common failure modes
- **3** — Evidence quality is measured, tuned, explainable, and monitored over time

### Evidence to look for
- citation payloads
- retrieval precision/recall checks
- golden questions
- grounded answer review process
- unsupported-claim monitoring

### Notes
- Current state:
- Gaps:
- Actions:

---

## 4. Workflow vs agent decisioning

### What good looks like
The solution uses deterministic workflows where possible and reserves agentic behavior for cases that truly benefit from dynamic reasoning.

### Scoring guide
- **0** — Everything is treated as a generic chatbot/agent flow
- **1** — Some workflows are separated, but decisioning is mostly implicit
- **2** — Workflow vs agent boundaries are documented, with partial routing logic
- **3** — Clear routing strategy exists with reviewable criteria, fallbacks, and operating rules

### Evidence to look for
- task classification rules
- workflow catalog
- decision trees / routing logic
- agent autonomy boundaries
- fallback paths

### Notes
- Current state:
- Gaps:
- Actions:

---

## 5. Policy and access controls

### What good looks like
Model usage, tool permissions, and sensitive actions are constrained by explicit policy rather than hidden prompt logic.

### Scoring guide
- **0** — No clear policy layer; controls live in prompts or app code only
- **1** — Some manual controls exist, but policy is incomplete or not enforceable
- **2** — Policy rules are defined for many cases, but coverage or auditability is uneven
- **3** — Policy is explicit, enforceable, role-aware, environment-aware, and reviewable

### Evidence to look for
- tool allow/deny lists
- model restrictions by data class
- approval thresholds
- data handling rules
- policy versioning/change control

### Notes
- Current state:
- Gaps:
- Actions:

---

## 6. Tool and system integration discipline

### What good looks like
External systems are accessed through stable, observable adapters with bounded behavior.

### Scoring guide
- **0** — Raw system integrations are loosely controlled or undocumented
- **1** — Integrations exist, but schemas/timeouts/errors are inconsistent
- **2** — Most adapters are structured, but some risk controls are missing
- **3** — Tool interfaces are stable, observable, idempotent where needed, and safe by design

### Evidence to look for
- structured input/output schemas
- timeout and retry policy
- correlation IDs
- dry-run or preview mode
- idempotency design for writes

### Notes
- Current state:
- Gaps:
- Actions:

---

## 7. Human approval and exception handling

### What good looks like
Sensitive actions pause for human review, and exception paths are operationally practical.

### Scoring guide
- **0** — No clear approval path for risky actions
- **1** — Manual approvals happen informally, without consistent triggers or evidence
- **2** — Approval flow exists, but turnaround, context, or logging is weak
- **3** — Approval triggers, UX, escalation, and audit trail are all operationalized

### Evidence to look for
- approval matrix
- exception queue/process
- approver context pack
- timeout handling
- manual override / kill switch

### Notes
- Current state:
- Gaps:
- Actions:

---

## 8. Observability and auditability

### What good looks like
The end-to-end chain can be reconstructed across prompts, retrieval, tools, approvals, and outputs.

### Scoring guide
- **0** — Minimal or fragmented logging
- **1** — Some logs exist, but they do not support investigation or improvement well
- **2** — Core traces exist, but gaps remain across components or teams
- **3** — Full traceability exists with usable dashboards, audit records, and incident support

### Evidence to look for
- request tracing
- prompt/model/tool logging
- approval logs
- audit schema
- dashboards and alerts

### Notes
- Current state:
- Gaps:
- Actions:

---

## 9. Evaluation and release governance

### What good looks like
Changes to prompts, models, workflows, and sources are evaluated before broad rollout and monitored after release.

### Scoring guide
- **0** — No structured evaluation or release controls
- **1** — Ad hoc testing exists, but no repeatable governance
- **2** — Formal evaluation exists for major changes, but coverage is incomplete
- **3** — Offline/online evaluation, release approval, rollback, and review cadence are in place

### Evidence to look for
- test sets
- acceptance thresholds
- release checklist
- rollback plan
- post-release review cadence

### Notes
- Current state:
- Gaps:
- Actions:

---

## 10. Business outcome instrumentation

### What good looks like
The system is measured against workflow and business outcomes, not just model fluency.

### Scoring guide
- **0** — Success is described qualitatively, with no operational KPI tracking
- **1** — Some KPIs are named, but baseline/target instrumentation is weak
- **2** — Business and operational KPIs are tracked, but not consistently tied to architecture decisions
- **3** — Outcome metrics drive prioritization, release decisions, and investment cases

### Evidence to look for
- containment rate
- handling time reduction
- resolution quality
- search success / deflection
- user trust/adoption
- conversion/revenue or cost impact where relevant

### Notes
- Current state:
- Gaps:
- Actions:

---

# Score summary

| Dimension | Score (0-3) |
|---|---:|
| 1. Business scope and ownership | |
| 2. Knowledge layer quality | |
| 3. Retrieval trust and grounding | |
| 4. Workflow vs agent decisioning | |
| 5. Policy and access controls | |
| 6. Tool and system integration discipline | |
| 7. Human approval and exception handling | |
| 8. Observability and auditability | |
| 9. Evaluation and release governance | |
| 10. Business outcome instrumentation | |
| **Total** | |

## Interpretation
- **0-9** — concept / demo stage
- **10-17** — pilot stage with major production gaps
- **18-24** — emerging production readiness
- **25-30** — strong production operating model

## Top 3 priority gaps
1.
2.
3.

## Recommended 30/60/90-day plan

### Next 30 days
- 
- 
- 

### Next 60 days
- 
- 
- 

### Next 90 days
- 
- 
- 

---

# Suggested workshop flow

## 60-minute version
- 10 min — use case scope and business objective
- 20 min — score the 10 dimensions
- 15 min — identify the 3 biggest operating risks
- 15 min — agree a 30/60/90-day action plan

## 90-minute version
- 15 min — business context and architecture walkthrough
- 30 min — collaborative scoring
- 20 min — evidence review and challenge assumptions
- 15 min — define target-state architecture priorities
- 10 min — agree owners and next steps

---

# Monetization fit

This scorecard can anchor:
- an enterprise AI readiness workshop
- a RAG/agent governance advisory sprint
- a proposal discovery engagement
- a partner solution assessment session

Use it as the front door into a broader architecture and governance offer.
