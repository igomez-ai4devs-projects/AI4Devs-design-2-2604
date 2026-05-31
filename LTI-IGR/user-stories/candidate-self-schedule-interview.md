# Candidate self-schedules or reschedules an interview

> **Use case:** UC-INT-02 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As a **Candidate**, I want **to pick or change my interview slot from the available times via a self-scheduling link** so that **I can choose a time that works for me without coordinating over email**.

## INVEST justification
- **Independent:** Self-scheduling consumes proposed slots and finalizes a booking; it is a discrete candidate-facing capability.
- **Negotiable:** Slot-picker design, hold-tentative duration, and SMS confirmation are open; the story fixes a time-zone-aware self-service slot selection that books across calendars.
- **Valuable:** Reduces scheduling friction and drop-off, accelerating time-to-hire and improving candidate experience.
- **Estimable:** Bounded to a slot-picker page, tentative holds, and confirmation booking.
- **Small:** A focused self-scheduling flow, completable within a sprint.
- **Testable:** Verifiable by the candidate's selection creating/updating calendar events and confirmations.

## Acceptance criteria

### Scenario 1: Candidate picks a slot
- **Given** I have received a self-scheduling link with available slots
- **When** I select a slot in my local time zone
- **Then** the system books the calendar events for the panel and me, confirms the booking, and releases any tentative holds on the other slots.

### Scenario 2: Tentative holds during selection
- **Given** I am choosing among proposed slots
- **When** I open the self-scheduling page
- **Then** the system places tentative holds on the relevant calendars so the slots are not taken while I decide.

### Scenario 3: Candidate reschedules
- **Given** I have a confirmed interview
- **When** I reschedule to a new available slot
- **Then** the system cancels the original event, books the new one, and regenerates kits and reminders.

## Notes / dependencies
- Depends on UC-INT-01 / [schedule-interview-calendar-sync](schedule-interview-calendar-sync.md) (recruiter proposes slots).
- The self-scheduling page must be mobile-first and WCAG 2.1 AA compliant; all times persisted in UTC.
- Rescheduling emits `interview.rescheduled`.
