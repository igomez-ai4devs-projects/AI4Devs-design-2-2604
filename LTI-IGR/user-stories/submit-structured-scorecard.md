# Submit a structured scorecard

> **Use case:** UC-INT-06 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As an **Interviewer**, I want **to submit a structured scorecard with rubric ratings and an overall recommendation after the interview** so that **the hiring decision is based on consistent, comparable, bias-mitigated evidence**.

## INVEST justification
- **Independent:** Scorecard capture is a self-contained action tied to a completed interview.
- **Negotiable:** Rubric anchors, competency set, and required-field specifics are open; the story fixes structured per-competency ratings plus a locked recommendation.
- **Valuable:** Structured scorecards are the core of quality-of-hire and fair, defensible decisions.
- **Estimable:** Bounded to a scorecard form, persistence, locking, and the blind-visibility rule.
- **Small:** A focused submission flow, completable within a sprint.
- **Testable:** Verifiable by a persisted, locked `Scorecard` and `interview.scorecard.submitted` emission.

## Acceptance criteria

### Scenario 1: Submit and lock a scorecard
- **Given** I conducted a scheduled interview
- **When** I rate each competency (1–5 with anchors + comments), select an overall recommendation (`Strong Hire` / `Hire` / `No Hire` / `Strong No Hire`), fill required strengths/concerns, and submit
- **Then** the system persists and **locks** the scorecard (no further edits) and emits `interview.scorecard.submitted`.

### Scenario 2: Required fields enforced
- **Given** I have not completed the required strengths/concerns or a competency rating
- **When** I attempt to submit
- **Then** the system blocks submission until all required fields are complete.

### Scenario 3: Blind scorecard until all panel submits
- **Given** other panel members have submitted their scorecards
- **When** I view the interview before all panel members have submitted
- **Then** I cannot see peers' scorecards (anti-anchoring), per the blind-scorecard policy.

## Notes / dependencies
- Depends on UC-INT-01 / [schedule-interview-calendar-sync](schedule-interview-calendar-sync.md).
- Late scorecards (>48h) escalate to the Hiring Manager and block the decision until complete.
- Feeds UC-INT-07 / [collaborative-debrief](collaborative-debrief.md).
