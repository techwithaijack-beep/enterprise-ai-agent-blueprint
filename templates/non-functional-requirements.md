# Non-Functional Requirements Template for Enterprise AI Solutions

Use this template during discovery or solution definition.

## 1. Solution overview
- **Use case:**
- **Primary users:**
- **Regions / business units:**
- **Channels:**
- **Core systems involved:**

## 2. Availability and resilience
- **Target uptime / service window:**
- **Recovery time objective (RTO):**
- **Recovery point objective (RPO):**
- **Acceptable degraded modes:**
- **Dependencies requiring failover/fallback:**

## 3. Performance
- **Target response time (p50 / p95):**
- **Peak concurrent users / sessions:**
- **Peak request volume per hour/day:**
- **Batch or async workload requirements:**
- **Tool timeout thresholds:**

## 4. Security and access
- **Identity provider / auth pattern:**
- **Roles/personas:**
- **Tool permission boundaries:**
- **Sensitive data classes involved:**
- **Encryption requirements:**
- **Secret management standard:**

## 5. Data and governance
- **Source systems and owners:**
- **Data residency constraints:**
- **Retention requirements:**
- **PII or regulated data considerations:**
- **Audit requirements:**
- **Approval requirements:**

## 6. AI and model requirements
- **Tasks requiring LLMs:**
- **Tasks requiring deterministic workflows instead of LLMs:**
- **Grounding / citation requirements:**
- **Fallback model strategy:**
- **Structured output requirements:**
- **Cost guardrails / budget constraints:**

## 7. Observability and support
- **Logs required:**
- **Tracing required:**
- **Dashboards required:**
- **Alerts required:**
- **Support / on-call owner:**
- **Incident severity model:**

## 8. Compliance and review
- **Security review required:** yes / no
- **Legal/privacy review required:** yes / no
- **Model risk review required:** yes / no
- **Business approval required for go-live:** yes / no

## 9. Acceptance criteria
- **Business KPI targets:**
- **Operational KPI targets:**
- **Quality/evaluation thresholds:**
- **Go-live blockers:**
