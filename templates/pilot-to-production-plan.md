# Pilot to Production Plan

## Phase 0: Discovery and scope control
- Define the exact workflow, user personas, and success metrics
- Identify data sources, systems, and approval boundaries
- Decide where deterministic workflow is preferable to agent behavior
- Establish security, privacy, and regional constraints

## Phase 1: Pilot build
- Implement narrow workflow scope with limited tool surface area
- Use a small, representative knowledge set
- Add full tracing, prompt versioning, and audit logging from day one
- Keep risky actions behind approval or dry-run mode

## Phase 2: Controlled pilot
- Launch to limited users or one business unit
- Track quality, latency, escalations, and operational issues daily
- Review bad cases and unsupported claims systematically
- Tune retrieval, prompts, and policy rules before expanding scope

## Phase 3: Operational hardening
- Expand knowledge coverage and workflow depth carefully
- Add dashboards, alerts, and support playbooks
- Validate rollback procedures for prompts, models, and workflow releases
- Stress-test integrations, approval paths, and outage handling

## Phase 4: Production rollout
- Expand only after business and operational acceptance criteria are met
- Maintain change control for prompt/model/policy updates
- Continue evaluation with golden sets and sampled production reviews
- Use quarterly architecture and governance reviews to prevent drift

## Exit criteria from pilot
- Quality threshold met on representative scenarios
- Support team trained and escalation path tested
- High-risk actions protected by approval rules
- Observability and audit trail verified
- Business owner signs off based on defined metrics
