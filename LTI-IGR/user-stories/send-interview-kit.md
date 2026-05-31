# Send an interview kit to interviewers

> **Use case:** UC-INT-03 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As an **Interviewer**, I want **to automatically receive an interview kit when I am scheduled** so that **I arrive prepared with the candidate's context, the rubric, and suggested questions for a structured, fair interview**.

## INVEST justification
- **Independent:** Kit assembly and delivery is a discrete step triggered by scheduling and tested on its own.
- **Negotiable:** Kit contents layout, delivery channel (email vs. in-app), and prior-scorecard visibility rules are open; the story fixes that each interviewer receives a kit with rubric and context.
- **Valuable:** Structured-hiring preparation directly improves quality-of-hire and interviewer consistency.
- **Estimable:** Bounded to assembling kit contents and delivering them to each panel member.
- **Small:** A focused generation-and-delivery step, completable within a sprint.
- **Testable:** Verifiable by each interviewer receiving a kit and `interview.kit.sent` being emitted.

## Acceptance criteria

### Scenario 1: Kit delivered on scheduling
- **Given** an interview has been scheduled with a panel
- **When** the schedule is confirmed
- **Then** the system sends each interviewer a kit containing the candidate CV, JD snapshot, rubric pre-loaded, and suggested questions, and emits `interview.kit.sent`.

### Scenario 2: Anti-bias gating of prior scorecards
- **Given** the tenant's anti-bias policy restricts visibility of previous-stage scorecards
- **When** the kit is assembled
- **Then** prior scorecards are included only if permitted by that policy.

### Scenario 3: Kit regenerated on reschedule
- **Given** a scheduled interview is rescheduled
- **When** the new slot is confirmed
- **Then** the system regenerates and re-sends the interview kit.

## Notes / dependencies
- Depends on UC-INT-01 / [schedule-interview-calendar-sync](schedule-interview-calendar-sync.md).
- Kit rubric/question bank come from the interview-kit library (UC-INT-10, P1, falls back to stage defaults for MVP).
