# SLA per approval step (configuration)

- **ID:** configure-approval-chain-05
- **Type:** Feature
- **Priority:** Medium
- **Estimation:** 3 story points
- **Assigned to:** Backend Team
- **Labels:** requisitions, backend, sla, governance, MVP

## Description

**Purpose:** Let an Admin set and store an SLA (e.g., 3 business days) per approval step so that the value is available to drive auto-escalation (Scenario 3). **Scope decision:** this story persists and exposes the SLA configuration only; the runtime escalation engine (timer/worker that fires when an approver does not act) is owned by [approve-or-reject-requisition](../../user-stories/approve-or-reject-requisition.md) (UC-REQ-02).

**Specific details:**
- Add/persist `slaBusinessDays` per step via the data model (ticket 01) and CRUD API (ticket 02).
- Validate SLA is a positive integer within a sane bound (e.g., 1–30 business days).
- Include the SLA value in the resolved chain snapshot (ticket 04) so the downstream escalation worker can read it without re-querying configuration.
- Provide a small, documented read contract (`getStepSla` / field on the snapshot) that the UC-REQ-02 escalation worker will consume — this is the thin enabler seam between the two stories.

## Acceptance criteria

- [ ] An Admin editing a chain can set an SLA per step and it is persisted (Scenario 3, config side).
- [ ] The SLA value is carried into the resolved-chain snapshot at submission time.
- [ ] Invalid SLA values (non-positive, out of bound) are rejected with a 400.
- [ ] A documented read contract exposes the per-step SLA for the escalation worker owned by UC-REQ-02.

### Validation tests
- Integration test: set SLA = 3 on the HR Director step, save, reload, and assert it persists.
- Integration test: submit a requisition and assert the snapshot carries the per-step SLA.
- Negative test: set SLA = 0 or 999 and assert rejection.

## Comments and notes
- Runtime auto-escalation behavior (alternative flow A3 in the spec) is intentionally **out of scope** here per the agreed boundary; this ticket only guarantees the SLA is configurable and readable. Tracked as a dependency on UC-REQ-02.

## Links / references
- Source user story: [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md) (Scenario 3)
- Depends on: [approval-chain-data-model](approval-chain-data-model.md), [approval-chain-crud-api](approval-chain-crud-api.md), [chain-resolution-engine](chain-resolution-engine.md)
- Escalation runtime owned by: [approve-or-reject-requisition](../../user-stories/approve-or-reject-requisition.md) (UC-REQ-02, alt flow A3)

## Change history
- 31/05/2026: Created by Ivan
