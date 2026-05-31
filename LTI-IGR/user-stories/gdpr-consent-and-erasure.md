# Manage GDPR consent and right-to-be-forgotten

> **Use case:** UC-CAND-12 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Candidate (and DPO)**, I want **to grant or withdraw consent for the processing of my data and request erasure** so that **my privacy rights under GDPR are respected and the organization stays compliant**.

## INVEST justification
- **Independent:** Consent capture and erasure handling are a discrete compliance capability over candidate data.
- **Negotiable:** Consent-version copy, the self-service vs. DPO-mediated erasure path, and retention defaults are open; the story fixes versioned consent and an enforceable erasure flow.
- **Valuable:** Mandatory legal compliance in the EU; failure carries regulatory and reputational risk.
- **Estimable:** Bounded to versioned consent persistence, a withdrawal/erasure request, and a data-lifecycle action.
- **Small:** A focused consent-and-erasure capability, completable within a sprint.
- **Testable:** Verifiable by stored consent version/timestamp, `candidate.consent.revoked` events, and anonymization/deletion on erasure.

## Acceptance criteria

### Scenario 1: Capture versioned consent at application
- **Given** a candidate applies from an EU jurisdiction
- **When** they grant GDPR consent
- **Then** the system persists the consent version, timestamp, and scope on the `Candidate` record.

### Scenario 2: Withdraw consent
- **Given** a candidate has previously granted consent
- **When** they withdraw it
- **Then** the system records the withdrawal and emits `candidate.consent.revoked` for the DPO and data-lifecycle worker.

### Scenario 3: Right-to-be-forgotten request
- **Given** a candidate or the DPO submits an erasure request
- **When** the request is processed
- **Then** the system anonymizes or deletes the candidate's PII per the consent/retention policy while preserving non-identifying audit records.

### Scenario 4: Retention expiry
- **Given** a candidate has been inactive beyond the configured retention period (default 24 months)
- **When** the data-lifecycle worker runs
- **Then** the candidate's data is anonymized/deleted unless extended-retention consent (e.g., talent pool) exists.

## Notes / dependencies
- Depends on UC-CAND-01 / [apply-to-a-job](apply-to-a-job.md).
- GDPR consent is mandatory in the EU and versioned. PII is encrypted at rest; voluntary EEO data is stored separately and never shown to hiring decision-makers.
