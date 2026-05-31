# Provision a video meeting for an interview

> **Use case:** UC-INT-05 · **Domain:** Interviews & Hire Decision · **Priority:** P0

## Story
As a **Recruiter**, I want **a video meeting link to be provisioned automatically and embedded in the interview invite** so that **candidates and interviewers can join without anyone manually creating and distributing a meeting link**.

## INVEST justification
- **Independent:** Video provisioning is a discrete integration step on a booked interview.
- **Negotiable:** Which provider, link-placement, and fallback behavior are open; the story fixes that a meeting link is created via the configured integration and embedded in the calendar event.
- **Valuable:** Removes manual link handling and reduces join friction and start delays for remote interviews.
- **Estimable:** Bounded to a provider API call and embedding the returned link.
- **Small:** A focused integration step, completable within a sprint.
- **Testable:** Verifiable by a `videoLink` stored on the `Interview` and present in the invite.

## Acceptance criteria

### Scenario 1: Provision a meeting link
- **Given** an interview is being scheduled and a video integration (Zoom / Meet / Teams) is configured
- **When** the schedule is confirmed
- **Then** the system provisions a meeting via the integration, stores the `videoLink` on the `Interview`, and embeds it in the calendar event for all attendees.

### Scenario 2: No video integration configured
- **Given** no video integration is configured for the tenant
- **When** the interview is scheduled
- **Then** the recruiter can enter a manual conferencing link, which is embedded in the invite.

### Scenario 3: Link regenerated on reschedule
- **Given** a scheduled interview is rescheduled
- **When** the new slot is confirmed
- **Then** the system re-provisions or updates the video link as needed.

## Notes / dependencies
- Depends on UC-INT-01 / [schedule-interview-calendar-sync](schedule-interview-calendar-sync.md).
- Requires a configured video integration; manual link is the fallback.
