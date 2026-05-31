# Run a collaborative debrief

> **Use case:** UC-INT-07 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As a **Hiring Manager (with the interview panel)**, I want **to review all submitted scorecards together once they are complete** so that **the panel can surface disagreement, calibrate, and align before a hire decision is made**.

## INVEST justification
- **Independent:** The debrief is a discrete collaborative step gated on completed scorecards; it produces alignment, distinct from recording the decision.
- **Negotiable:** Debrief UI, calibration aids, and comment threading are open; the story fixes that cross-panel visibility unlocks only when all scorecards are in.
- **Valuable:** Calibration reduces individual bias and improves decision quality.
- **Estimable:** Bounded to the unlock gate, aggregated scorecard view, and debrief notification.
- **Small:** A focused review step, completable within a sprint.
- **Testable:** Verifiable by cross-panel visibility unlocking only after full submission and the HM being notified.

## Acceptance criteria

### Scenario 1: Debrief unlocks when all scorecards are in
- **Given** every panel member has submitted a locked scorecard
- **When** the last scorecard is submitted
- **Then** the system unlocks cross-panel visibility, notifies the Hiring Manager that the debrief is ready, and emits `interview.debrief.opened`.

### Scenario 2: Debrief blocked while scorecards are pending
- **Given** one or more panel members have not submitted
- **When** the Hiring Manager attempts to open the debrief
- **Then** the system keeps scorecards blind, shows who is pending, and sends a reminder to the pending interviewers.

### Scenario 3: Surface disagreement
- **Given** the debrief is open
- **When** the panel reviews the aggregated scorecards
- **Then** divergent recommendations are highlighted to focus calibration.

## Notes / dependencies
- Depends on UC-INT-06 / [submit-structured-scorecard](submit-structured-scorecard.md) (all panel scorecards required).
- A panel is "evaluated" only when **all** scorecards are submitted — no partial decisions.
- Feeds UC-INT-08 / [record-hire-decision](record-hire-decision.md).
