# Tickets — Configure the requisition approval chain

> **Source user story:** [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md) · **Use case:** UC-REQ-10 · **Priority:** P0

## Decomposition summary

This user story lets an **Admin / Talent Ops** configure approval chains scoped to a department or cost center so requisitions are routed to the right approvers automatically and headcount governance is enforced consistently. It is a **P0 enabler**: without a configured, resolvable chain, requisitions cannot enter the approval flow (UC-REQ-01 / UC-REQ-02).

The story was split into seven tickets along its natural seams. A **data model** ticket lays the foundation, on top of which a **CRUD API** exposes chain configuration and the **conditional-rules** and **SLA** features add per-step behavior. The **resolution & snapshot engine** is the core enabler that turns saved configuration into an ordered approver sequence for a given requisition and freezes it at submission time (the verifiable "then" of Scenarios 1 and 2). An **admin builder UI** is the actor-facing surface for all three scenarios, and a cross-cutting **RBAC & audit** ticket secures the configuration and satisfies the 7-year audit-retention compliance rule.

Two scope boundaries were agreed up front: (1) **SLA auto-escalation runtime** is *out of scope* — this story only persists and exposes the per-step SLA; the timer/worker that fires on inaction is owned by UC-REQ-02 (a thin read contract is the seam between them). (2) **Conditional rules are predefined** (LEVEL / SALARY_BAND / COST_CENTER) rather than a generic rule builder, keeping the work estimable with no spike required.

## Tickets summary

| ID | Ticket | Type | Priority | Estimation | Assignee |
|----|--------|------|----------|-----------|----------|
| 01 | [Data model & migrations for approval chains](approval-chain-data-model.md) | Technical Task | Critical | 3 pts | Backend Team |
| 02 | [Backend API — Approval chain CRUD](approval-chain-crud-api.md) | Feature | High | 5 pts | Backend Team |
| 03 | [Conditional approval steps (predefined rules)](conditional-step-rules.md) | Feature | High | 5 pts | Backend Team |
| 04 | [Approval chain resolution & snapshot engine](chain-resolution-engine.md) | Feature | Critical | 8 pts | Backend Team |
| 05 | [SLA per approval step (configuration)](sla-per-step-config.md) | Feature | Medium | 3 pts | Backend Team |
| 06 | [Admin UI — Approval chain builder](admin-chain-builder-ui.md) | Feature | High | 8 pts | Frontend Team |
| 07 | [RBAC & audit logging for chain configuration](rbac-and-audit-logging.md) | Technical Task | High | 5 pts | Backend Team |

**Total estimated effort:** 37 story points

## Dependency order

```
01 data-model
   └─> 02 crud-api ──> 03 conditional-rules ─┐
                  └──> 05 sla-config ─────────┼─> 04 resolution-engine
                  └──> 07 rbac-audit          │
                  └──> 06 admin-ui  <──────────┘ (consumes 02/03/05)
```

Recommended sequence: **01 → 02 → (03, 05, 07 in parallel) → 04 → 06**. Ticket 04 (resolution engine) is the critical enabler downstream stories block on; ticket 06 (UI) can begin against the API contract once 02 is stable.

## Coverage of acceptance criteria

| Scenario | Covered by |
|----------|-----------|
| 1 — Define an ordered approval chain for a department | 01, 02, 04, 06 |
| 2 — Conditional escalation by role seniority | 03, 04, 06 |
| 3 — Configure an approval SLA | 05, 06 (runtime escalation → UC-REQ-02) |
