# Publish a job to the career site

> **Use case:** UC-REQ-03 · **Domain:** Requisitions & Job Posting · **Priority:** P0

## Story
As a **Recruiter**, I want **to refine an approved requisition into a public job posting and publish it to the branded career site** so that **candidates can discover and apply to the role and the hiring funnel can begin filling**.

## INVEST justification
- **Independent:** Publication consumes an approved requisition and produces a live posting; it does not require board distribution or the apply flow to deliver value.
- **Negotiable:** The markdown editor, theme picker, and form-builder details are open; the story fixes only that an approved requisition becomes a live, public posting with a minted URL.
- **Valuable:** A live posting is the first candidate-facing artifact and the gate for every downstream application.
- **Estimable:** Bounded to JD editing, pipeline/knockout/theme configuration, and a publish transition to `Open`.
- **Small:** A single publish flow, completable within a sprint.
- **Testable:** Verifiable by the posting going live, a public URL being minted, status `Open`, and compliance-field enforcement.

## Acceptance criteria

### Scenario 1: Publish an approved requisition
- **Given** I own an `Approved` requisition
- **When** I refine the public-facing JD, configure pipeline stages and knockout questions, pick the career-site theme and application form, and click **Publish to career site**
- **Then** the posting goes live, the status becomes `Open`, a public URL is minted, and a `requisition.published` event is emitted.

### Scenario 2: Pay-transparency jurisdiction enforces salary range
- **Given** the posting location matches a regulated jurisdiction (e.g., CA, CO, NY, WA)
- **When** I attempt to publish without a salary range
- **Then** the system blocks publication until a salary range is provided.

### Scenario 3: EEO statement required
- **Given** I am about to publish a posting
- **When** the JD does not include the EEO statement
- **Then** the system prevents publication until the EEO statement is present.

## Notes / dependencies
- Depends on UC-REQ-02 / [approve-or-reject-requisition](approve-or-reject-requisition.md).
- Enables UC-CAND-01 / [apply-to-a-job](apply-to-a-job.md).
- Source-of-application tracking (UTM) is activated on publish for downstream attribution. Multi-board distribution (UC-REQ-04) is P1 and out of this story's scope.
