# Data model & migrations for approval chains

- **ID:** configure-approval-chain-01
- **Type:** Technical Task
- **Priority:** Critical
- **Estimation:** 3 story points
- **Assigned to:** Backend Team
- **Labels:** requisitions, backend, data-model, governance, MVP

## Description

**Purpose:** Establish the persistence foundation for approval-chain configuration. Every other ticket in this story (CRUD API, conditional rules, resolution engine, SLA config, admin UI) depends on a stable schema. Without it, requisitions cannot be routed for approval — this is the structural enabler for the whole approval flow.

**Specific details:**
- Add tables/entities in the `requisitions` module of the modular monolith:
  - `ApprovalChain { id, tenantId, name, scopeType (DEPARTMENT | COST_CENTER), scopeValue, isActive, createdBy, createdAt, updatedAt }`
  - `ApprovalChainStep { id, chainId, order, approverType (ROLE | USER), approverRef (e.g., FINANCE, HR_DIRECTOR, CEO, or userId), slaBusinessDays, isConditional, createdAt }`
  - `ApprovalChainCondition { id, stepId, attribute (LEVEL | SALARY_BAND | COST_CENTER), operator (EQ | GTE | IN), value }` — backs the predefined-condition rules (Scenario 2).
- Enforce **tenant isolation** (every row scoped by `tenantId`) per architecture driver G2.
- Unique constraint: only one active chain per `(tenantId, scopeType, scopeValue)`; steps unique per `(chainId, order)`.
- Provide forward and rollback migrations.
- Align field names with the existing `Requisition.approvalChain[]` snapshot shape in [requisitions/spec.md](../../specs/requisitions/spec.md) §4.

## Acceptance criteria

- [ ] Migrations create `ApprovalChain`, `ApprovalChainStep`, and `ApprovalChainCondition` with the fields above and run cleanly forward and backward.
- [ ] All tables are tenant-scoped and enforce the unique-active-chain-per-scope constraint.
- [ ] Referential integrity: deleting a chain cascades to its steps and conditions.
- [ ] Step ordering is enforced as unique and contiguous per chain.

### Validation tests
- Run the migration on a clean DB and on a populated DB; confirm both succeed and rollback restores the prior schema.
- Insert two active chains for the same `(tenant, department)` and confirm the unique constraint rejects the second.
- Delete a chain and confirm orphan steps/conditions are removed.

## Comments and notes
- Field naming must match the snapshot consumed by [approve-or-reject-requisition](../../user-stories/approve-or-reject-requisition.md) to avoid a translation layer later.

## Links / references
- Source user story: [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md)
- Domain spec: [requisitions/spec.md](../../specs/requisitions/spec.md) §4 (key data model)
- Architecture: [specs/design.md](../../specs/design.md) (modular monolith, tenant isolation G2)

## Change history
- 31/05/2026: Created by Ivan
