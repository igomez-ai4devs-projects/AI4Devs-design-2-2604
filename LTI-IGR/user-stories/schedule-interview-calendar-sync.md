# Schedule an interview with calendar sync

> **Use case:** UC-INT-01 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As a **Recruiter**, I want **to schedule an interview by checking interviewers' calendar availability and booking a slot** so that **interviews are arranged quickly without double-bookings or back-and-forth emails**.

## INVEST justification
- **Independent:** Scheduling produces a persisted `Interview` and calendar event; kits, reminders, and video links are separate stories.
- **Negotiable:** Slot-proposal UX, working-hours policy details, and observer handling are open; the story fixes Free/Busy lookup and event creation across interviewer and candidate calendars.
- **Valuable:** Scheduling is the largest source of recruiter coordination overhead and a direct lever on time-to-hire.
- **Estimable:** Bounded to calendar Free/Busy lookup, slot selection, and event creation.
- **Small:** A focused scheduling flow, completable within a sprint.
- **Testable:** Verifiable by a created `Interview`, calendar events on attendees, and conflict prevention.

## Acceptance criteria

### Scenario 1: Book an interview from available slots
- **Given** an application at the `Interview` stage and interviewers with connected calendars
- **When** I select the interview type and panel, the system runs Free/Busy lookup and I confirm a compatible slot
- **Then** the system creates an `Interview`, books calendar events (`.ics`) on the interviewers and candidate honoring the candidate's time zone, and emits `interview.scheduled`.

### Scenario 2: Respect working hours and buffers
- **Given** an interviewer's configured working hours and a default 15-minute buffer
- **When** the system proposes slots
- **Then** no slot is proposed outside working hours or violating the mandatory buffer.

### Scenario 3: No common availability
- **Given** the panel has no overlapping free slots in the chosen window
- **When** I attempt to schedule
- **Then** the system lets me widen the window or add manual slots rather than booking a conflict.

## Notes / dependencies
- Requires interviewers to have connected calendars (Google / Microsoft OAuth).
- Reached when a candidate is moved to `Interview` (UC-CAND-09 / [move-candidate-pipeline-stage](move-candidate-pipeline-stage.md)).
- Triggers UC-INT-03 / [send-interview-kit](send-interview-kit.md), UC-INT-04 / [automated-interview-reminders](automated-interview-reminders.md), UC-INT-05 / [provision-video-meeting](provision-video-meeting.md).
