# Backend API — Approval chain CRUD

- **ID:** configure-approval-chain-02
- **Type:** Feature
- **Priority:** High
- **Estimation:** 5 story points
- **Assigned to:** Backend Team
- **Labels:** requisitions, backend, api, governance, MVP

## Description

**Purpose:** Expose the API that lets an Admin / Talent Ops create, read, update, list, and deactivate approval chains scoped to a department or cost center. This realizes the configuration half of Scenario 1 ("create an approval chain … scoped to a department or cost center and save it").

**Specific details:**
- Implement endpoints in the `requisitions` module:
  - `POST /approval-chains` — create a chain with ordered steps.
  - `GET /approval-chains` / `GET /approval-chains/{id}` — list and detail, filterable by scope.
  - `PUT /approval-chains/{id}` — update steps, order, scope, name.
  - `DELETE /approval-chains/{id}` (or `PATCH` to deactivate) — soft-delete / deactivate.
- Validate: ordered, non-empty steps; valid `scopeType`/`scopeValue`; no duplicate active chain for the same scope (surface the constraint from ticket 01 as a 409).
- Tenant-scoped: a caller can only operate on chains within their tenant.
- Emit no domain event on configuration changes beyond the audit log (see ticket 07); chains are referenced, not published, until resolved at submission time.
- Depends on the schema from [approval-chain-data-model](approval-chain-data-model.md).

## Acceptance criteria

- [ ] An Admin can create a chain with an ordered list of approver steps scoped to a department or cost center and it is persisted (Scenario 1).
- [ ] The chain can be retrieved, listed (filtered by scope), updated, and deactivated.
- [ ] Creating a second active chain for the same scope returns a 409 with a clear message.
- [ ] All endpoints reject cross-tenant access.
- [ ] Invalid payloads (empty steps, bad scope, duplicate order) return 400 with field-level errors.

### Validation tests
- Integration test: POST a Finance → HR Director → CEO chain scoped to "Engineering" department; GET it back and assert step order is preserved.
- Integration test: PUT to reorder steps and confirm the new order persists.
- Integration test: attempt cross-tenant GET/PUT and assert 403/404.
- Contract test against the OpenAPI definition for all endpoints.

## Comments and notes
- Keep the CRUD payload aligned with the admin UI builder (ticket 06) to avoid a mapping layer.

## Links / references
- Source user story: [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md)
- Depends on: [approval-chain-data-model](approval-chain-data-model.md)
- Domain spec: [requisitions/spec.md](../../specs/requisitions/spec.md)

## Change history
- 31/05/2026: Created by Ivan
