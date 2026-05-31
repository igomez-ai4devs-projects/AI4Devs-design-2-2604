# Create a requisition from a template

> **Use case:** UC-REQ-01 · **Domain:** Requisitions & Job Posting · **Priority:** P0

## Story
As a **Hiring Manager**, I want **to open a new requisition from a job-description template and submit it for approval** so that **I can request headcount quickly with a consistent, compliant job profile instead of writing one from scratch**.

## INVEST justification
- **Independent:** Requisition intake stands alone; it does not require publication, screening, or interviews to deliver value (a submitted requisition is itself a deliverable).
- **Negotiable:** Defines that a requisition is created from a template and submitted — the exact field set, template library UX, and validation messaging are open for refinement with the team.
- **Valuable:** Removes the blank-page problem and standardizes intake, the origin of the entire hiring funnel.
- **Estimable:** Bounded to a creation form, template selection, headcount validation, and a state transition to `Pending Approval`.
- **Small:** A single create-and-submit flow, completable within a sprint.
- **Testable:** Clear pass/fail on field validation, headcount checks, and the resulting `Pending Approval` status.

## Acceptance criteria

### Scenario 1: Create and submit a requisition from a template
- **Given** I am an authenticated Hiring Manager assigned to a team with open headcount
- **When** I select a JD template, complete the required fields (title, department, location, employment type, level, salary band, hiring team, target start date, business justification) and submit
- **Then** the system creates a `Requisition` with status `Pending Approval`, references the cost center and hiring manager, and notifies the first approver in the resolved approval chain.

### Scenario 2: Start from a blank requisition
- **Given** I am creating a new requisition
- **When** I choose "start blank" instead of a template
- **Then** the system presents an empty form with the same required fields and the same validation before allowing submission.

### Scenario 3: Headcount plan exceeded
- **Given** my team has no open seats remaining against the headcount plan
- **When** I attempt to submit the requisition
- **Then** the system blocks submission and surfaces a link to the budget owner.

### Scenario 4: Missing required field
- **Given** I have left a required field (e.g., business justification) empty
- **When** I attempt to submit
- **Then** the system prevents submission and highlights the missing field.

## Notes / dependencies
- Requires JD templates and an approval chain to exist (see UC-REQ-10 / [configure-approval-chain](configure-approval-chain.md)).
- Approval chain is **resolved and snapshotted at submission time** so later org changes do not break in-flight requisitions.
- Emits `requisition.created`. Feeds UC-REQ-02 / [approve-or-reject-requisition](approve-or-reject-requisition.md).
