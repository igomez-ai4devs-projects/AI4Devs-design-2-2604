# Manually add a candidate

> **Use case:** UC-CAND-06 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Recruiter**, I want **to manually add a candidate and attach them to a requisition** so that **sourced, referred, or offline candidates enter the same pipeline as inbound applicants**.

## INVEST justification
- **Independent:** Manual creation is a self-contained entry path that does not depend on the public apply flow.
- **Negotiable:** The intake form, CV-on-create behavior, and duplicate-warning UX are open; the story fixes that a recruiter can create a `Candidate` + `Application` directly.
- **Valuable:** Lets recruiters capture sourced and referred talent, not only inbound applicants — essential for real hiring.
- **Estimable:** Bounded to a create form, optional CV upload triggering parsing, and `Application` creation against a chosen requisition.
- **Small:** A single create flow, completable within a sprint.
- **Testable:** Verifiable by a created `Candidate` and `Application` linked to the selected requisition.

## Acceptance criteria

### Scenario 1: Add a candidate to a requisition
- **Given** I am a Recruiter on an open requisition
- **When** I enter the candidate's details, optionally upload a CV, and save
- **Then** the system creates a `Candidate` and an `Application(stage = NEW, source = manual)` linked to that requisition.

### Scenario 2: CV parsing on manual add
- **Given** I attach a CV while manually adding a candidate
- **When** I save
- **Then** the system enqueues CV parsing so the candidate's structured data becomes searchable.

### Scenario 3: Duplicate candidate detected
- **Given** a candidate with the same email already exists in the tenant
- **When** I save the new candidate
- **Then** the system surfaces the existing profile and offers to link the new application rather than create a duplicate.

## Notes / dependencies
- Reuses parsing from UC-CAND-02 / [auto-parse-cv](auto-parse-cv.md) when a CV is attached.
- Email uniqueness per candidate within a tenant is enforced; cross-tenant isolation applies.
- Deduplication/merge logic (UC-CAND-05) is P1.
