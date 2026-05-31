# Close, pause, or cancel a requisition

> **Use case:** UC-REQ-07 · **Domain:** Requisitions & Job Posting · **Priority:** P0

## Story
As a **Recruiter**, I want **to put a requisition on hold, close it, or cancel it** so that **postings stop accepting applications when a role is filled, frozen, or withdrawn and the funnel reflects reality**.

## INVEST justification
- **Independent:** Lifecycle management acts on an existing posting and delivers value on its own (stops inbound applications, keeps reporting accurate).
- **Negotiable:** Confirmation UX, reason capture, and unpublish timing within the SLA are open; the story fixes the state transitions and the automatic unpublish behavior.
- **Valuable:** Prevents wasted candidate effort and stale postings, and keeps headcount/analytics trustworthy.
- **Estimable:** Bounded to status transitions plus the downstream unpublish action.
- **Small:** A set of related state transitions on one entity, completable within a sprint.
- **Testable:** Verifiable by status change, board/career-site unpublish, and emitted events.

## Acceptance criteria

### Scenario 1: Close a filled requisition
- **Given** I own an `Open` requisition
- **When** I close it
- **Then** the status becomes `Closed`, the posting is unpublished from the career site and all boards within 24h, and a `requisition.closed` event is emitted.

### Scenario 2: Put a requisition on hold
- **Given** I own an `Open` requisition
- **When** I place it `On Hold`
- **Then** the posting stops accepting new applications while existing applications and pipeline data are preserved.

### Scenario 3: Cancel a requisition
- **Given** I own a requisition that should not be filled
- **When** I cancel it
- **Then** the status becomes `Cancelled`, the posting is unpublished everywhere, and a `requisition.cancelled` event is emitted.

## Notes / dependencies
- Depends on UC-REQ-03 / [publish-job-to-career-site](publish-job-to-career-site.md).
- Closing/cancelling triggers the distribution service to unpublish from boards (board distribution itself is P1).
- Reopen (UC-REQ-08) is P1 and out of scope here.
