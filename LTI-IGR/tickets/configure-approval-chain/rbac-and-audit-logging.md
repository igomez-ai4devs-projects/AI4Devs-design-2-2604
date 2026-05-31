# RBAC & audit logging for chain configuration

- **ID:** configure-approval-chain-07
- **Type:** Technical Task
- **Priority:** High
- **Estimation:** 5 story points
- **Assigned to:** Backend Team
- **Labels:** requisitions, backend, security, compliance, audit, MVP

## Description

**Purpose:** Approval chains are a governance asset that controls who can authorize headcount spend, so configuration must be restricted to authorized roles and every change must be auditable. This satisfies compliance driver G4 and the spec's 7-year audit-retention rule for approval-related actions.

**Specific details:**
- **RBAC:** restrict create/update/delete/deactivate of approval chains to **Admin / Talent Ops** roles; other roles get read-only or no access per tenant policy. Enforce server-side on every CRUD endpoint (ticket 02), not just in the UI.
- **Audit logging:** write an audit entry for every chain configuration change (create, update, reorder, condition change, SLA change, deactivate) capturing actor, tenant, timestamp, before/after diff, and entity id.
- Route audit entries to the platform audit log used by the requisitions domain (the same trail referenced by approve/publish/distribute actions in [requisitions/spec.md](../../specs/requisitions/spec.md) §4).
- Ensure audit entries are immutable and retained per the 7-year policy.

## Acceptance criteria

- [ ] Only Admin / Talent Ops can mutate approval chains; unauthorized roles receive 403 on all write endpoints.
- [ ] Every chain configuration change produces an immutable audit entry with actor, timestamp, tenant, entity id, and before/after diff.
- [ ] Audit entries are queryable via the existing audit log surface for the requisitions domain.
- [ ] Read access follows the tenant's role policy.

### Validation tests
- Integration test: attempt each write endpoint as a non-admin role and assert 403.
- Integration test: create then update a chain as Admin and assert two audit entries with correct actor and a meaningful diff.
- Test that audit entries cannot be modified or deleted via the API.

## Comments and notes
- Reuse the shared audit-log component rather than introducing a requisitions-local log, to keep the 7-year retention and compliance reporting centralized.

## Links / references
- Source user story: [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md)
- Depends on: [approval-chain-crud-api](approval-chain-crud-api.md)
- Compliance: [specs/design.md](../../specs/design.md) (G4 — RBAC, audit log); [requisitions/spec.md](../../specs/requisitions/spec.md) §4 (7-year audit retention)

## Change history
- 31/05/2026: Created by Ivan
