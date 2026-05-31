# Approval chain resolution & snapshot engine

- **ID:** configure-approval-chain-04
- **Type:** Feature
- **Priority:** Critical
- **Estimation:** 8 story points
- **Assigned to:** Backend Team
- **Labels:** requisitions, backend, core, governance, MVP

## Description

**Purpose:** Turn a saved chain configuration into an **ordered, resolved approver sequence** for a given requisition, applying predefined conditional rules, and **snapshot** that resolved chain onto the requisition at submission time. This is the core enabler the downstream approval flow consumes (UC-REQ-01 / UC-REQ-02) and the verifiable outcome of Scenarios 1 and 2.

**Specific details:**
- Implement a `resolveApprovalChain(requisition)` service that:
  1. Selects the active chain matching the requisition's department or cost center scope.
  2. Evaluates each step's predefined conditions (from [conditional-step-rules](conditional-step-rules.md)) against the requisition attributes (level, salary band, cost center).
  3. Returns the ordered list of resolved approver steps including any conditionally-added steps (e.g., executive approver for senior roles).
- **Snapshot** the resolved chain onto `Requisition.approvalChain[]` at submission time so later org/config changes don't alter in-flight requisitions (business rule in [requisitions/spec.md](../../specs/requisitions/spec.md) §4).
- Handle no-matching-chain gracefully: return a clear, typed result so the caller (submission flow) can block submission with an actionable message rather than failing opaquely.
- Pure resolution + snapshot only — **does not** notify approvers or advance the workflow (that is UC-REQ-02).

## Acceptance criteria

- [ ] Given a saved chain (e.g., Finance → HR Director → CEO) scoped to a department, a matching requisition resolves to exactly that ordered sequence (Scenario 1, "then").
- [ ] Given a conditional executive step on senior roles, a senior-level requisition resolves to a chain that **includes** the executive step; a non-senior one does **not** (Scenario 2, "then").
- [ ] The resolved chain is snapshotted onto the requisition at submission; subsequent edits to the source chain do not change already-submitted requisitions.
- [ ] When no active chain matches the scope, resolution returns a typed "no chain" result (no exception leak).

### Validation tests
- Unit test resolution for: simple linear chain, conditional step matched, conditional step not matched, multiple conditional steps.
- Integration test: submit a requisition, edit the source chain, and assert the requisition's snapshot is unchanged.
- Integration test: submit against a scope with no active chain and assert the typed no-chain result.

## Comments and notes
- Snapshot format must match the `approvalChain[]` shape the approval-flow story reads; coordinate field names with ticket 01.

## Links / references
- Source user story: [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md) (Scenarios 1 & 2)
- Depends on: [approval-chain-data-model](approval-chain-data-model.md), [conditional-step-rules](conditional-step-rules.md)
- Enables: [create-requisition-from-template](../../user-stories/create-requisition-from-template.md), [approve-or-reject-requisition](../../user-stories/approve-or-reject-requisition.md)

## Change history
- 31/05/2026: Created by Ivan
