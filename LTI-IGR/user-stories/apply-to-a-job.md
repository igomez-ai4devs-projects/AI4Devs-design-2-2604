# Apply to a job

> **Use case:** UC-CAND-01 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Candidate**, I want **to apply to a published job through the career site by submitting my details and CV** so that **I can be considered for the role and track the status of my application**.

## INVEST justification
- **Independent:** The apply flow produces a persisted `Application`; parsing, scoring, and screening are separate downstream stories.
- **Negotiable:** Form layout, "Apply with LinkedIn/Indeed" pre-fill, and success-page copy are open; the story fixes that a candidate can submit an application against a live posting.
- **Valuable:** This is the funnel entry point — no candidates exist in the system without it.
- **Estimable:** Bounded to rendering the apply form, server-side validation, persistence of `Candidate` + `Application`, CV upload, and a confirmation email.
- **Small:** A single submission flow, completable within a sprint.
- **Testable:** Verifiable by a created `Application(stage = NEW)`, stored CV, and confirmation email.

## Acceptance criteria

### Scenario 1: Successful application submission
- **Given** a job posting is live on the career site and not past its close date
- **When** I complete the required fields, upload a CV (PDF/DOCX, ≤10 MB), answer knockout questions, and submit
- **Then** the system creates/updates a `Candidate`, creates an `Application(stage = NEW, source = utm_source)`, stores the CV in encrypted storage, sends a confirmation email with a status-tracking link, and shows an "Application received" page.

### Scenario 2: Invalid CV file
- **Given** I am completing the apply form
- **When** I upload a file that is not PDF/DOCX or exceeds 10 MB
- **Then** the system rejects the upload server-side and prompts me to provide a valid file.

### Scenario 3: Missing GDPR consent (EU)
- **Given** I am applying from a jurisdiction requiring GDPR consent
- **When** I submit without checking the consent box
- **Then** the system blocks submission with an explanation.

### Scenario 4: Apply with LinkedIn / Indeed pre-fill
- **Given** I choose "Apply with LinkedIn" or "Apply with Indeed"
- **When** I authorize via OAuth
- **Then** the system pre-fills my profile from the provider, and CV upload becomes optional.

## Notes / dependencies
- Depends on UC-REQ-03 / [publish-job-to-career-site](publish-job-to-career-site.md).
- Triggers UC-CAND-02 / [auto-parse-cv](auto-parse-cv.md) and UC-CAND-03 / [evaluate-knockout-questions](evaluate-knockout-questions.md) asynchronously.
- Emits `application.created`. Email uniqueness is enforced per candidate within a tenant.
