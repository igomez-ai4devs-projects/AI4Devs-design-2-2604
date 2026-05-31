# Admin UI — Approval chain builder

- **ID:** configure-approval-chain-06
- **Type:** Feature
- **Priority:** High
- **Estimation:** 8 story points
- **Assigned to:** Frontend Team
- **Labels:** requisitions, frontend, ui, governance, MVP

## Description

**Purpose:** Give Admin / Talent Ops a focused configuration screen to create and edit ordered approval chains — set scope, add/reorder steps, attach predefined conditions, and set per-step SLAs. This is the primary surface through which the actor in the story performs the "create … and save" actions of all three scenarios.

**Specific details:**
- New admin screen under Requisitions settings: list of chains + a chain builder.
- Chain builder supports:
  - Scope selector (department or cost center).
  - Ordered, drag-to-reorder list of approver steps (role or specific user).
  - Per-step toggle for "conditional" with the predefined attribute/operator/value selectors (LEVEL / SALARY_BAND / COST_CENTER) from ticket 03.
  - Per-step SLA input (business days) from ticket 05.
- Recruiter-grade UX per driver G5: keyboard-friendly, optimistic save, inline validation, clear error states (including the duplicate-active-chain 409 from ticket 02).
- Consumes the CRUD API (ticket 02); no business logic duplicated client-side beyond field validation.

## Acceptance criteria

- [ ] An Admin can create a chain (e.g., Finance → HR Director → CEO), set its department/cost-center scope, and save it; the saved chain appears in the list (Scenario 1).
- [ ] An Admin can mark a step conditional and configure a predefined condition (e.g., add executive approver for senior roles) (Scenario 2).
- [ ] An Admin can set a per-step SLA (e.g., 3 business days) (Scenario 3).
- [ ] Steps can be reordered and the order is reflected on save.
- [ ] Server validation errors (duplicate active chain, invalid SLA, unknown attribute) are surfaced inline.

### Validation tests
- E2E test: build and save a 3-step chain with a conditional executive step and an SLA, then reload and assert all fields render correctly.
- E2E test: reorder steps via drag-and-drop and confirm the persisted order.
- E2E test: attempt to create a duplicate active chain for the same scope and assert the inline 409 error.
- Accessibility check: full keyboard navigation of the builder.

## Comments and notes
- Coordinate the form payload shape with ticket 02 to avoid a client-side mapping layer.

## Links / references
- Source user story: [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md) (all scenarios)
- Depends on: [approval-chain-crud-api](approval-chain-crud-api.md), [conditional-step-rules](conditional-step-rules.md), [sla-per-step-config](sla-per-step-config.md)
- UX driver: [specs/design.md](../../specs/design.md) (G5 recruiter-grade UX)

## Change history
- 31/05/2026: Created by Ivan
