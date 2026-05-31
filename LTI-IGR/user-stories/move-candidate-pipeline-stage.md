# Move a candidate across pipeline stages

> **Use case:** UC-CAND-09 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Recruiter**, I want **to advance a candidate's application across pipeline stages on a Kanban board** so that **the hiring funnel reflects each candidate's true status and the right downstream actions are triggered**.

## INVEST justification
- **Independent:** Stage progression is a self-contained state change on an `Application`.
- **Negotiable:** Kanban interactions (drag-and-drop vs. dropdown), bulk moves, and which templates fire are open; the story fixes permissioned stage transitions with event emission.
- **Valuable:** Pipeline visibility and movement are the core daily workflow of a recruiter.
- **Estimable:** Bounded to permissioned stage transitions and the resulting events.
- **Small:** A focused stage-change interaction, completable within a sprint.
- **Testable:** Verifiable by `Application.stage` updating and `application.stage.changed` being emitted.

## Acceptance criteria

### Scenario 1: Advance a candidate to the next stage
- **Given** I have permission on a requisition's pipeline and a candidate at the `Screening` stage
- **When** I move the candidate to `Interview`
- **Then** the system updates `Application.stage`, emits `application.stage.changed`, and triggers the configured communication template and analytics events.

### Scenario 2: Permission enforcement
- **Given** I lack the permission to change pipeline stages on this requisition
- **When** I attempt to move a candidate
- **Then** the system blocks the action.

### Scenario 3: Standard pipeline stages respected
- **Given** the standard pipeline `New → Screening → Assessment → Interview → Offer → Hired`
- **When** I move a candidate between stages
- **Then** the move is recorded against the application's timeline for time-in-stage analytics.

## Notes / dependencies
- Depends on UC-CAND-01 / [apply-to-a-job](apply-to-a-job.md).
- Moving to the `Interview` stage enables UC-INT-01 / [schedule-interview-calendar-sync](schedule-interview-calendar-sync.md).
- Dispositioning/rejection is handled by UC-CAND-10 / [reject-candidate-with-reason](reject-candidate-with-reason.md).
