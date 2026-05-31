# Configure the requisition approval chain

> **Use case:** UC-REQ-10 · **Domain:** Requisitions & Job Posting · **Priority:** P0

## Story
As an **Admin / Talent Ops**, I want **to configure approval chains per department or cost center** so that **requisitions are routed to the right approvers automatically and headcount governance is enforced consistently**.

## INVEST justification
- **Independent:** Approval-chain configuration is a standalone setup capability that delivers value as a reusable governance asset.
- **Negotiable:** Chain-builder UX, conditional rules (e.g., by salary band or level), and SLA defaults are open for refinement; the story fixes that admins can define ordered approver chains scoped to a department/cost center.
- **Valuable:** Without a configured chain, requisitions cannot be routed for approval — it is the enabler for the entire approval flow.
- **Estimable:** Bounded to a configuration CRUD over chain definitions with scoping rules.
- **Small:** A focused admin configuration screen, completable within a sprint.
- **Testable:** Verifiable by a saved chain correctly resolving the approver sequence for a matching requisition.

## Acceptance criteria

### Scenario 1: Define an ordered approval chain for a department
- **Given** I am an Admin
- **When** I create an approval chain (e.g., Finance → HR Director → CEO) scoped to a department or cost center and save it
- **Then** the chain is persisted and applied to new requisitions matching that scope.

### Scenario 2: Conditional escalation by role seniority
- **Given** an approval chain with a rule that senior-level roles require an additional executive approver
- **When** a senior-level requisition is submitted in that scope
- **Then** the resolved chain includes the executive approver step.

### Scenario 3: Configure an approval SLA
- **Given** I am editing an approval chain
- **When** I set an SLA (e.g., 3 business days) per step
- **Then** the SLA is stored and drives auto-escalation when an approver does not act in time.

## Notes / dependencies
- Enabler for UC-REQ-01 / [create-requisition-from-template](create-requisition-from-template.md) and UC-REQ-02 / [approve-or-reject-requisition](approve-or-reject-requisition.md).
- Chains are snapshotted onto each requisition at submission time.
