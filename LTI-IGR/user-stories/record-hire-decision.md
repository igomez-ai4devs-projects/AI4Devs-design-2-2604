# Record the hire / no-hire decision

> **Use case:** UC-INT-08 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As a **Hiring Manager**, I want **to record the final hire / no-hire decision with justification after the debrief** so that **the candidate advances to an offer or is dispositioned and the decision is auditable**.

## INVEST justification
- **Independent:** Recording the decision is a discrete terminal action on the evaluation, distinct from the debrief that precedes it.
- **Negotiable:** Decision label set, justification length, and override permissions are open; the story fixes a permissioned, justified, audited decision that advances the application.
- **Valuable:** This is the conversion point of the funnel — applications become hires here.
- **Estimable:** Bounded to a decision capture, stage transition, and event emission.
- **Small:** A single decision-recording action, completable within a sprint.
- **Testable:** Verifiable by `Application.stage` advancing/dispositioning and `interview.decision.recorded` emission.

## Acceptance criteria

### Scenario 1: Advance to offer
- **Given** the debrief is complete
- **When** the Hiring Manager records `Advance` (to offer) with a justification
- **Then** the system updates `Application.stage`, emits `interview.decision.recorded`, and triggers the offers domain.

### Scenario 2: Reject after debrief
- **Given** the debrief is complete
- **When** the Hiring Manager records `Reject` with a justification
- **Then** the system dispositions the candidate and a templated dispositioning email is sent.

### Scenario 3: Decision authorization
- **Given** a user without hire-decision permission (not a Hiring Manager or senior Recruiter with override)
- **When** they attempt to record the decision
- **Then** the system blocks the action.

### Scenario 4: Split panel decision
- **Given** the panel recommendations diverge
- **When** the Hiring Manager records the final call
- **Then** a justification is mandatory and stored with the decision.

## Notes / dependencies
- Depends on UC-INT-07 / [collaborative-debrief](collaborative-debrief.md).
- Every decision is retained with author, timestamp, and justification for 7 years (audit/compliance).
- "Advance to offer" hands off to the Offers domain (UC-OFF-01, out of this MVP scope set).
