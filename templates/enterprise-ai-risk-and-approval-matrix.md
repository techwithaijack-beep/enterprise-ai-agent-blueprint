# Enterprise AI Risk & Approval Matrix Template

A practical template for defining which AI actions can run automatically, which require approval, what evidence is needed before execution, and how exceptions should be handled in production.

This artifact is designed for enterprise AI architects, platform owners, governance teams, and delivery leads who need to turn vague statements like "put a human in the loop" into explicit operating rules.

## Why this exists

Many enterprise AI teams know that some actions are too risky to automate freely, but they still operationalize approvals badly.

Common failure modes:
- approval rules are buried in someone's head rather than documented
- approval thresholds are inconsistent across channels and systems
- teams gate low-risk actions but accidentally automate high-impact ones
- confidence is used as the only control signal even when business risk is the real issue
- approvers receive requests with too little context to make good decisions
- exceptions are handled informally and never feed back into policy design

A production AI system needs a clear answer to four questions:
1. **What action is being taken?**
2. **What is the business or control risk if it goes wrong?**
3. **What approval, if any, is required before execution?**
4. **What evidence must be shown to the approver or audit trail?**

This template makes those decisions explicit.

## How to use this template

Use it during architecture workshops, governance reviews, rollout planning, or production hardening.

Recommended process:
1. inventory the actions your assistant, copilot, or agent can perform
2. classify each action by business impact and reversibility
3. define the approval pattern per action class
4. specify what evidence must accompany every approval request
5. wire the resulting rules into policy, workflow, and audit systems
6. review exceptions and incidents monthly to refine thresholds

## Core design principles

### 1) Approvals should follow risk, not novelty
Do not require human review simply because the system uses AI. Require it when the action creates meaningful business, customer, financial, legal, operational, or reputational risk.

### 2) Confidence is not a control plane
Low confidence may justify escalation, but high confidence should not automatically authorize high-impact actions.

### 3) Separate read, recommend, draft, and execute
These are different control categories.
- **Read** — retrieve or inspect data
- **Recommend** — suggest a decision or next step
- **Draft** — prepare an action for human review
- **Execute** — perform the action in a live system

Most governance failures happen when teams jump from draft to execute without explicit approval logic.

### 4) Reversibility matters
A reversible update should not be governed the same way as an irreversible deletion, financial transaction, or external commitment.

### 5) Approval requests must be decision-ready
If the approver cannot quickly see the proposed action, evidence, risk context, and fallback path, the approval process will become slow, inconsistent, or ceremonial.

## Step 1 — Action inventory

List the actions the system can perform or trigger.

| Action ID | Action description | Channel / workflow | Target system | Category | Typical actor |
|---|---|---|---|---|---|
| `send_external_message` | Send message to customer / partner / candidate | WhatsApp / email / CRM / web chat | Messaging platform / CRM | External communication | Support agent / sales copilot |
| `update_business_record` | Create or update structured business data | CRM / ERP / ticketing / HRIS | Core business system | System mutation | Operations / service workflow |
| `issue_financial_adjustment` | Refund, waiver, discount, credit | Support / finance workflow | Finance / billing system | Financial action | Service or finance workflow |
| `publish_content` | Post publicly under brand or executive identity | LinkedIn / website / CMS | Public platform | Public reputation action | Marketing / thought leadership flow |
| `export_sensitive_data` | Export or compile regulated or confidential records | Admin / analytics workflow | Data warehouse / file store | Data extraction | Analyst / admin flow |
| `delete_or_close_record` | Delete, close, or archive record with downstream impact | CRM / ticketing / ERP | Core business system | Irreversible mutation | Operations workflow |

Add every meaningful action your system can take, not just the ones that feel risky.

## Step 2 — Risk scoring model

Use a lightweight scoring model to classify action risk. Adjust dimensions to fit your environment.

### Suggested dimensions

| Dimension | Question | Score 1 | Score 3 | Score 5 |
|---|---|---|---|---|
| Customer impact | If wrong, how much does this affect a customer or partner? | minimal inconvenience | moderate service issue | major harm / breach of trust |
| Financial impact | If wrong, what is the financial consequence? | negligible | moderate loss or leakage | significant loss or liability |
| Legal / policy impact | Could this violate policy, regulation, or contractual terms? | unlikely | possible | high-risk / regulated |
| Reputational impact | Could this create public or executive visibility if mishandled? | internal only | local stakeholder concern | externally visible / executive-sensitive |
| Reversibility | How hard is it to undo? | easy to reverse | partially reversible | irreversible or costly |
| Data sensitivity | What kind of data does it touch? | low sensitivity | internal confidential | sensitive / regulated |

### Suggested risk bands

| Total score | Risk band | Default approval posture |
|---|---|---|
| 6-10 | Low | auto-execute allowed if policy and validation pass |
| 11-17 | Medium | auto-execute for bounded cases, otherwise queue approval |
| 18-24 | High | approval required before execution |
| 25-30 | Critical | approval plus stronger controls, dual review, or block automation |

Do not rely on scoring alone. Use mandatory overrides for specific action types.

## Step 3 — Mandatory override rules

Some actions should require approval regardless of risk score.

Common override candidates:
- sending customer-facing messages outside approved templates
- publishing public content under executive or company identity
- financial credits, refunds, pricing changes, or commercial commitments
- deletion of records or data with regulatory or operational significance
- exporting sensitive or regulated data
- policy exceptions or cross-boundary access requests
- actions performed with incomplete evidence or missing citations

Document overrides explicitly.

| Override condition | Required control |
|---|---|
| Public posting under executive identity | Named human approval before publish |
| Financial adjustment above threshold | Finance approval |
| External message with free-form generated content | Operator review before send |
| Sensitive data export | Owner approval + logged justification |
| Irreversible deletion | Change approval + rollback/backup confirmation |

## Step 4 — Approval pattern matrix

Use this table as the core operating artifact.

| Action ID | Action class | Example | Risk band | Default execution mode | Approval trigger | Required approver | Evidence shown to approver | Time SLA | Escalation path | Audit fields captured |
|---|---|---|---|---|---|---|---|---|---|---|
| `draft_customer_reply` | Draft only | Prepare support response | Low | Auto-draft | none | n/a | citations, confidence, source links | n/a | n/a | prompt version, sources, reviewer edits |
| `send_external_message` | Execute | Send final WhatsApp/email | High | Approval-first | free-form content, low confidence, policy flag, VIP customer, compensation mentioned | service owner / operator | message draft, source evidence, confidence notes, customer record, policy check | 15 min | team lead | request id, approver id, final content, send timestamp |
| `update_crm_record` | Execute | Change opportunity stage | Medium | Conditional auto-execute | confidence below threshold, missing source evidence, value above threshold | record owner | proposed field changes, source event, prior values | 30 min | sales manager | record id, before/after values, reason code |
| `issue_financial_adjustment` | Execute | Refund or waiver | Critical | Approval-first | always | finance approver | case summary, amount, policy basis, customer history | 4 h | finance lead | amount, currency, approver, policy rule, ticket id |
| `publish_content` | Execute | LinkedIn / website post | High | Approval-first | always unless pre-approved scheduling flow exists | named owner of identity/account | final copy, asset link, channel, schedule time | 24 h | content owner | draft id, approver, account, publish result |
| `export_sensitive_data` | Execute | Download regulated dataset | Critical | Block or approval-first | always | data owner + security, if required | purpose, scope, data classes, retention plan | 24 h | security lead | requester, scope, legal basis, expiry |

Add rows for your real actions.

## Step 5 — Approval packet design

Every approval request should include enough context for a fast, defensible decision.

### Minimum approval packet
- action ID and plain-language action summary
- proposed output or system change
- business reason / case context
- source evidence or citations
- relevant confidence or validation signals
- triggered policy rule or override reason
- rollback or mitigation path if available
- recommended decision: approve, reject, revise, or escalate

### Example approval packet — external message

```yaml
approval_request:
  action_id: send_external_message
  channel: whatsapp
  customer_segment: enterprise_account
  reason: case_update_after_ocr_review
  proposed_message: |
    Hi Sarah — we completed the first review of the submitted shipping documents...
  evidence:
    - source: ticket_48392
    - source: ocr_validation_report_2026_03_13
    - source: policy.customer_update_template.v3
  risk_flags:
    - free_form_generated_text
    - external_commitment_language
  confidence:
    extraction_confidence: 0.91
    policy_pass: true
  approver_options:
    - approve_and_send
    - request_revision
    - reject
```

## Step 6 — Threshold and routing rules

Use thresholds for bounded automation, but keep them subordinate to business policy.

| Signal | Example rule |
|---|---|
| Confidence threshold | Auto-update CRM only when confidence >= 0.95 and evidence count >= 2 |
| Monetary threshold | Auto-approve credits below MYR 50 only for approved scenarios |
| Data scope threshold | Approval required if export contains personal, regulated, or executive data |
| Customer tier threshold | Approval required for strategic or high-risk accounts |
| Content type threshold | Approval required for any free-form external communication |
| Environment threshold | Production actions require stricter approval than sandbox/staging |

## Step 7 — Exception handling model

Approvals should not be the only safeguard. Define what happens when execution is blocked, delayed, or rejected.

| Scenario | Recommended system behavior |
|---|---|
| Approval not received within SLA | escalate to secondary approver or fall back to human queue |
| Approval rejected | store reason code, prevent execution, request revision if allowed |
| Policy conflict detected | block execution and surface the violated rule |
| Missing evidence | downgrade to draft-only or request more data |
| Repeated exception on same action type | trigger policy review or workflow redesign |

## Step 8 — Review cadence

Approval design should evolve with real operating data.

### Weekly
- review blocked actions and approval queue volume
- identify noisy or unnecessary approval triggers
- inspect any execution performed despite weak evidence

### Monthly
- review rejected approvals and incident patterns
- tune thresholds for speed vs control
- check whether approver load is concentrated on low-value decisions

### Quarterly
- reassess action classes, override rules, and escalation paths
- align approval design to new channels, tools, or regulatory requirements
- validate that audit logs still support investigation and reporting needs

## Example starter matrix

Use this starter set if you need a working first draft.

| Action class | Default posture | Notes |
|---|---|---|
| Retrieval / search | Auto-execute | read-only, still log evidence and source usage |
| Internal summarization | Auto-execute | no external commitment or data mutation |
| Draft generation | Auto-execute to draft | human review required before send/publish if external |
| Low-risk record update | Conditional auto-execute | require schema validation and before/after logging |
| Customer-facing communication | Approval-first | especially when free-form, escalatory, or commercially sensitive |
| Financial action | Approval-first or dual approval | threshold- and policy-based |
| Public publishing | Approval-first | identity and reputation risk dominate |
| Sensitive export / deletion | Block by default or strict approval | use strongest controls |

## Implementation checklist

- [ ] action inventory exists and is current
- [ ] action classes map to real system operations
- [ ] risk scoring dimensions are agreed with stakeholders
- [ ] mandatory overrides are documented
- [ ] required approvers are named by role
- [ ] approval packets include evidence, not just confidence
- [ ] SLA and escalation paths are defined
- [ ] audit logs capture who approved what and why
- [ ] blocked/rejected actions feed into policy review
- [ ] policy engine and workflow implementation match this matrix

## Related assets in this repo

- [`templates/control-plane-assessment-scorecard.md`](control-plane-assessment-scorecard.md)
- [`templates/workflow-vs-agent-decision-matrix.md`](workflow-vs-agent-decision-matrix.md)
- [`templates/enterprise-ai-evaluation-operating-model.md`](enterprise-ai-evaluation-operating-model.md)
- [`examples/policy-pack.yaml`](../examples/policy-pack.yaml)
- [`offers/enterprise-ai-readiness-control-plane-review.md`](../offers/enterprise-ai-readiness-control-plane-review.md)

## Suggested usage in client work

This template works well in:
- enterprise AI readiness reviews
- governance and approval-design workshops
- customer engagement AI programs with external messaging risk
- RAG and agent projects that can mutate records or trigger workflows
- pilot-to-production programs where leadership needs clearer operating boundaries

## Closing point

The question is not whether an AI system should have human approval somewhere in the loop.

The real question is whether approvals are designed around actual business risk, supported by evidence, and operationally usable at scale.

That is what turns approval from a vague safety slogan into a production control.