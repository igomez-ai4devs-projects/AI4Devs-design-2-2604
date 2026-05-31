# Conditional approval steps (predefined rules)

- **ID:** configure-approval-chain-03
- **Type:** Feature
- **Priority:** High
- **Estimation:** 5 story points
- **Assigned to:** Backend Team
- **Labels:** requisitions, backend, rules, governance, MVP

## Description

**Purpose:** Let an Admin attach **predefined conditions** to a step so that the resolved chain adapts to the requisition — e.g., senior-level roles require an additional executive approver (Scenario 2). Scoped to a fixed, estimable set of attributes (no generic expression builder).

**Specific details:**
- Support conditions on a step using a fixed attribute set: `LEVEL`, `SALARY_BAND`, `COST_CENTER`.
- Supported operators: `EQ`, `GTE` (for level/band ordinal comparison), `IN` (set membership).
- A step marked `isConditional` is included in the resolved chain **only when its condition(s) match** the requisition; non-conditional steps are always included.
- Multiple conditions on one step are combined with AND (keep simple; document the choice).
- Validation: conditional steps must reference a valid attribute/operator/value; reject unknown attributes (this is the guard rail that keeps the feature bounded — not a free-form rule engine).
- Backed by `ApprovalChainCondition` from [approval-chain-data-model](approval-chain-data-model.md); persisted/edited through the CRUD API ([approval-chain-crud-api](approval-chain-crud-api.md)).

## Acceptance criteria

- [ ] An Admin can mark a step conditional and define one or more predefined conditions (attribute + operator + value).
- [ ] A condition such as "LEVEL GTE Senior → add Executive approver" is persisted with the step.
- [ ] The resolution engine (ticket 04) includes the conditional step only when the requisition matches; this ticket guarantees the condition data is correctly stored and queryable.
- [ ] Unknown attributes/operators are rejected at save time with a 400.

### Validation tests
- Unit test the condition-match predicate for `EQ`, `GTE`, `IN` across LEVEL / SALARY_BAND / COST_CENTER.
- Integration test: save a chain with an executive step conditioned on `LEVEL GTE Senior`; reload and assert the condition round-trips.
- Negative test: attempt to save a condition on an unsupported attribute (e.g., `LOCATION`) and assert rejection.

## Comments and notes
- Multi-condition combine semantics fixed to AND for MVP per the "predefined conditions" scope decision; revisit if a rule builder is requested later.

## Links / references
- Source user story: [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md) (Scenario 2)
- Depends on: [approval-chain-data-model](approval-chain-data-model.md), [approval-chain-crud-api](approval-chain-crud-api.md)
- Consumed by: [chain-resolution-engine](chain-resolution-engine.md)

## Change history
- 31/05/2026: Created by Ivan
