# Effort Estimation — Configure the requisition approval chain

> **Source user story:** [Configure the requisition approval chain](../../user-stories/configure-approval-chain.md) · **Use case:** UC-REQ-10 · **Priority:** P0
> **Tickets index:** [README.md](README.md)

## Methodology

Estimates were produced with **Planning Poker** using the **Fibonacci scale** (1, 2, 3, 5, 8, 13, 21) and recorded in **story points** as the primary unit. Story points are a relative measure of effort that blends three dimensions:

- **Complexity** — how intricate the logic/design is.
- **Uncertainty** — how many unknowns or external dependencies exist.
- **Volume** — how much work there is to do.

To make the points actionable for sprint planning, each ticket is also mapped to a **T-shirt size** and an **indicative hours range**. The hours range is a *planning aid only*; the team commits in points, not hours.

### Reference baseline (anchor stories)

| Points | T-shirt | Meaning | Anchor in this story |
|--------|---------|---------|----------------------|
| 1 | XS | Trivial, well-understood, < ½ day | — |
| 2 | S | Small, isolated change | — |
| 3 | S/M | Clear scope, low risk, ~1 day | Ticket 05 (SLA config) |
| 5 | M | Moderate logic + integration, ~2 days | Ticket 02 (CRUD API) |
| 8 | L | High complexity or breadth, multiple parts | Ticket 04 (resolution engine) |
| 13 | XL | Too large — should be split | — (none; nothing exceeds a sprint) |

### Points → hours conversion

Indicative band used for planning: **1 point ≈ 4–6 productive engineering hours** (including unit tests, code review, and ticket-local validation; excludes cross-team meetings). Ranges below are rounded.

## Per-ticket estimation

| ID | Ticket | Type | Complexity | Uncertainty | Volume | Points | T-shirt | Hours (≈) |
|----|--------|------|-----------|-------------|--------|--------|---------|-----------|
| 01 | [Data model & migrations](approval-chain-data-model.md) | Technical Task | Med | Low | Low | **3** | S/M | 12–18 |
| 02 | [Approval chain CRUD API](approval-chain-crud-api.md) | Feature | Med | Low | Med | **5** | M | 20–30 |
| 03 | [Conditional step rules](conditional-step-rules.md) | Feature | Med | Med | Med | **5** | M | 20–30 |
| 04 | [Resolution & snapshot engine](chain-resolution-engine.md) | Feature | High | Med | Med | **8** | L | 32–48 |
| 05 | [SLA per step (config)](sla-per-step-config.md) | Feature | Low | Low | Low | **3** | S/M | 12–18 |
| 06 | [Admin chain builder UI](admin-chain-builder-ui.md) | Feature | High | Med | High | **8** | L | 32–48 |
| 07 | [RBAC & audit logging](rbac-and-audit-logging.md) | Technical Task | Med | Low | Med | **5** | M | 20–30 |
| | | | | | **Total** | **37** | — | **148–222** |

## Rationale per ticket

- **01 — Data model & migrations (3 pts / S-M):** Well-understood CRUD schema with three related tables and constraints. Complexity is moderate (unique-active-chain constraint, cascade deletes) but there is little uncertainty — the shape is dictated by the spec's `approvalChain[]`. Low volume.

- **02 — CRUD API (5 pts / M):** Standard create/read/update/list/deactivate with validation and tenant scoping. Moderate volume across several endpoints; low uncertainty because it sits directly on the ticket-01 schema. The 409 duplicate-scope rule adds a little complexity.

- **03 — Conditional step rules (5 pts / M):** Bounded to predefined attributes (LEVEL / SALARY_BAND / COST_CENTER) and three operators, which caps complexity. Slight uncertainty in the match-predicate semantics (AND-combination, ordinal `GTE`) earns a 5 over a 3.

- **04 — Resolution & snapshot engine (8 pts / L):** The core enabler. High complexity: scope matching, conditional evaluation, ordered assembly, and immutable snapshotting at submission time. Carries the most downstream risk (UC-REQ-01/02 depend on it), so it is the largest backend item despite modest code volume.

- **05 — SLA per step (3 pts / S-M):** Smallest feature — persist a validated integer per step and carry it into the snapshot, plus a documented read contract. Runtime escalation is explicitly out of scope (owned by UC-REQ-02), which keeps this small and low-risk.

- **06 — Admin chain builder UI (8 pts / L):** Largest by volume. Builder with scope selector, drag-to-reorder steps, conditional-rule editor, SLA inputs, optimistic save, inline error handling, and accessibility. High volume + moderate UX uncertainty justify the 8.

- **07 — RBAC & audit logging (5 pts / M):** Cross-cutting security/compliance work across all write endpoints plus immutable audit entries with before/after diffs and 7-year retention. Moderate complexity, low uncertainty given the shared audit-log component.

## Aggregate view

- **Total:** **37 story points** ≈ **148–222 engineering hours**.
- **Backend share:** tickets 01–05, 07 = **29 pts** (~78%).
- **Frontend share:** ticket 06 = **8 pts** (~22%).
- **Critical-path items:** 04 (resolution engine) and, on the UI side, 06.

### Indicative sprint projection

Assuming a 2-week sprint and a team velocity of **~20 points/sprint**, this story spans roughly **2 sprints**:

- **Sprint 1 (≈18 pts):** 01 (3) → 02 (5) → 03 (5) + 05 (3) + start 07 (parallelizable). Establishes schema, API, rules, and SLA config.
- **Sprint 2 (≈19 pts):** 04 (8) resolution engine, 07 (5) finalize, 06 (8) admin UI built against the stable API contract.

Frontend (06) can begin against the ticket-02 contract once the API is stable, overlapping the backend work in Sprint 2.

## Assumptions & confidence

- Estimates assume the **predefined-conditions** scope (no generic rule builder) and **SLA config-only** boundary already agreed for this story; widening either would push 03/04 up a Fibonacci step.
- Confidence is **High** for 01, 02, 05, 07 (low uncertainty) and **Medium** for 03, 04, 06 (logic/UX unknowns).
- Points are relative and should be **re-evaluated** in the team's Planning Poker session; the values here are a calibrated starting proposal, not a commitment.

## Change history
- 31/05/2026: Created by Ivan
