# Disposition a candidate with a reason and email

> **Use case:** UC-CAND-10 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Recruiter**, I want **to disposition (reject) a candidate with a structured reason and a templated email** so that **candidates receive timely, consistent communication and the organization keeps a compliant audit trail of decisions**.

## INVEST justification
- **Independent:** Dispositioning is a self-contained terminal action on an `Application`.
- **Negotiable:** Reason taxonomy, email template selection, and send-now vs. batch are open; the story fixes that a rejection always carries a reason and triggers candidate communication.
- **Valuable:** Protects employer brand (no "black hole") and supports compliance with a documented decision reason.
- **Estimable:** Bounded to a reason selection, stage transition to `Rejected`, and a templated email.
- **Small:** A single disposition flow, completable within a sprint.
- **Testable:** Verifiable by `stage = Rejected`, a stored reason, and the dispositioning email.

## Acceptance criteria

### Scenario 1: Reject with reason and email
- **Given** I am reviewing a candidate in any active stage
- **When** I disposition the candidate, select a reason from the configurable taxonomy, and confirm
- **Then** the system sets `Application.stage = Rejected`, stores the rejection reason, sends a templated rejection email, and emits `application.rejected`.

### Scenario 2: Reason is mandatory
- **Given** I am dispositioning a candidate
- **When** I attempt to confirm without selecting a reason
- **Then** the system blocks the action until a reason is chosen.

### Scenario 3: Candidate withdraws
- **Given** a candidate chooses to withdraw
- **When** the withdrawal is recorded
- **Then** the system sets `Application.stage = Withdrawn` and emits `application.withdrawn`.

## Notes / dependencies
- Depends on UC-CAND-01 / [apply-to-a-job](apply-to-a-job.md).
- Rejected/silver-medalist candidates may be added to a talent pool (UC-CAND-11, P1) with extended-retention consent.
- Decision reason retained for audit.
