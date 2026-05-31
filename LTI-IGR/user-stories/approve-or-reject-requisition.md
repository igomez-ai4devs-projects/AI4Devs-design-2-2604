# Approve or reject a requisition

> **Use case:** UC-REQ-02 · **Domain:** Requisitions & Job Posting · **Priority:** P0

## Story
As an **Approver (Finance / HR / Exec)**, I want **to review a submitted requisition and approve or reject it with comments** so that **headcount spend is governed and only sanctioned roles enter the hiring funnel**.

## INVEST justification
- **Independent:** Operates on an already-submitted requisition; the approval decision is a self-contained increment of governance value.
- **Negotiable:** The format of the review screen, comment requirements, and notification channels are open; the story fixes only that approvers can approve/reject with comments and that routing advances.
- **Valuable:** Enforces budget and headcount governance — a hard requirement before any job goes live.
- **Estimable:** Bounded to a review action, comment capture, chain advancement, and state transitions.
- **Small:** One decision action per approver, completable within a sprint.
- **Testable:** Deterministic outcomes for approve (advance / final), reject (return to draft), and timeout escalation.

## Acceptance criteria

### Scenario 1: Intermediate approval advances the chain
- **Given** I am the current approver in a multi-stage approval chain
- **When** I approve the requisition with optional comments
- **Then** the system advances routing to the next approver and notifies them.

### Scenario 2: Final approval opens the requisition for publication
- **Given** I am the last approver in the chain
- **When** I approve the requisition
- **Then** the status becomes `Approved`, the owning Recruiter is notified, and a `requisition.approved` event is emitted.

### Scenario 3: Rejection returns the requisition to the Hiring Manager
- **Given** I am reviewing a requisition
- **When** I reject it with a mandatory comment
- **Then** the status returns to `Draft`, the Hiring Manager is notified with the rejection reason, and a `requisition.rejected` event is emitted.

### Scenario 4: Approval SLA timeout
- **Given** an approver has not acted within the configured SLA (e.g., 3 business days)
- **When** the SLA elapses
- **Then** the system auto-escalates the approval per the configured policy.

## Notes / dependencies
- Depends on UC-REQ-01 / [create-requisition-from-template](create-requisition-from-template.md) and the approval chain from UC-REQ-10 / [configure-approval-chain](configure-approval-chain.md).
- Every approval action is retained in the audit trail for 7 years.
