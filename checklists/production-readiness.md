# Production Readiness Checklist for Enterprise AI Agents

Use this before pilot launch, wider rollout, or production go-live.

## 1. Business and operating model
- [ ] Clear business owner identified
- [ ] Workflow scope documented, including out-of-scope cases
- [ ] Success metrics defined with baseline and target values
- [ ] Human support/escalation team identified
- [ ] Rollback and incident ownership agreed

## 2. Architecture and platform
- [ ] Clear separation exists between orchestration, retrieval, policy, and tools
- [ ] Deterministic workflow is used where agentic behavior is not required
- [ ] Environment separation exists for dev/test/prod
- [ ] State persistence and session strategy are documented
- [ ] Failure modes and graceful degradation paths are defined

## 3. Knowledge and retrieval
- [ ] Source systems are registered with owners
- [ ] Ingestion and refresh cadence is defined per source
- [ ] Access controls are enforced in retrieval layer
- [ ] Citation or evidence payload is available to downstream apps
- [ ] Source freshness, versioning, and deletion handling are documented
- [ ] Evaluation set exists for retrieval and answer grounding

## 4. Security and governance
- [ ] Secrets are stored outside code and rotated appropriately
- [ ] Tool permissions are role-based and least-privilege
- [ ] Policy rules define what the agent may read, write, or send
- [ ] PII/confidential data handling rules are documented
- [ ] Logging and transcript retention comply with policy
- [ ] Approval rules are defined for high-risk actions

## 5. Prompting and model management
- [ ] Prompt templates are version-controlled
- [ ] Structured output schemas are used where possible
- [ ] Approved model list exists by use case and data sensitivity
- [ ] Fallback model strategy exists
- [ ] Token/cost budgets are defined and monitored
- [ ] Offline evaluation exists for major prompt changes

## 6. Tooling and integrations
- [ ] Each tool has explicit input/output schema
- [ ] High-risk tools support dry-run or preview mode
- [ ] Idempotency strategy exists for write operations
- [ ] Retry, timeout, and error handling policies are implemented
- [ ] Integration SLAs and dependencies are documented

## 7. Human-in-the-loop
- [ ] Clear triggers for approval are defined
- [ ] Approvers see enough context to make decisions quickly
- [ ] Approval outcomes are logged with timestamp and actor
- [ ] Escalation path exists for timeouts or unavailable approvers
- [ ] Manual override and kill-switch are tested

## 8. Observability and operations
- [ ] Request tracing exists end-to-end
- [ ] Prompt/model/tool events are logged with correlation IDs
- [ ] Dashboards exist for latency, usage, failures, and approvals
- [ ] Alerts exist for critical failure patterns and budget breaches
- [ ] On-call/support playbook exists
- [ ] Post-incident review template exists

## 9. Evaluation and rollout
- [ ] Pilot acceptance criteria are documented
- [ ] Gold/test set exists for representative scenarios
- [ ] Shadow mode or limited rollout plan exists
- [ ] User feedback loop exists
- [ ] Release approval process exists for prompt/workflow/model updates
- [ ] Success review date is scheduled

## 10. Public credibility check
Before sharing externally or showcasing to customers:
- [ ] Claims are grounded in actual implementation capability
- [ ] Diagram matches real system boundaries
- [ ] Security/governance claims are supportable
- [ ] Metrics shown are real or clearly labeled illustrative
- [ ] Repo/document is understandable without verbal explanation
