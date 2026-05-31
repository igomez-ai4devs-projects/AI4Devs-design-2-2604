# Send automated interview reminders

> **Use case:** UC-INT-04 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As a **Recruiter**, I want **the system to send automated reminders to candidates and interviewers before each interview** so that **no-show rates drop and interviews start on time**.

## INVEST justification
- **Independent:** Reminder scheduling and delivery is a discrete, testable step on a booked interview.
- **Negotiable:** Reminder cadence beyond the defaults, channel (email/SMS), and copy are open; the story fixes mandatory 24h and 1h reminders to all attendees.
- **Valuable:** Reducing no-shows directly protects interviewer time and time-to-hire.
- **Estimable:** Bounded to scheduling timed notifications and sending them.
- **Small:** A focused notification step, completable within a sprint.
- **Testable:** Verifiable by reminders firing at 24h and 1h and `interview.reminder.sent` being emitted.

## Acceptance criteria

### Scenario 1: Default reminders fire
- **Given** an interview is scheduled
- **When** the 24h and 1h thresholds before the start time are reached
- **Then** the system sends reminders to all attendees (candidate and interviewers) and emits `interview.reminder.sent`.

### Scenario 2: Optional SMS to candidate
- **Given** SMS reminders are enabled for the candidate
- **When** a reminder fires
- **Then** the candidate also receives an SMS reminder.

### Scenario 3: Reminders rescheduled on change
- **Given** an interview is rescheduled or cancelled
- **When** the change is confirmed
- **Then** pending reminders are regenerated for the new time or cancelled accordingly.

## Notes / dependencies
- Depends on UC-INT-01 / [schedule-interview-calendar-sync](schedule-interview-calendar-sync.md).
- Reminders are mandatory and non-opt-out (policy) to reduce no-show rate.
