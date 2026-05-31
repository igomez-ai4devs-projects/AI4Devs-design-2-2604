# Automatically parse CVs into structured fields

> **Use case:** UC-CAND-02 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Recruiter**, I want **uploaded CVs to be parsed automatically into structured fields** so that **I can search, filter, and screen candidates instantly without manually re-keying their data**.

## INVEST justification
- **Independent:** Parsing operates on a stored CV and writes structured data; it can be delivered and tested independently of matching or pipeline progression.
- **Negotiable:** Parser engine, field coverage, and multi-language support depth are open; the story fixes that an uploaded CV yields indexed, structured candidate data.
- **Valuable:** Structured CV data is the recruiter's biggest productivity win and the prerequisite for search and AI matching.
- **Estimable:** Bounded to an asynchronous parsing worker producing a `Resume.parsedJson`.
- **Small:** A single async pipeline step, completable within a sprint.
- **Testable:** Verifiable by `parsedJson` populated with expected fields and `parseStatus` reflecting success or failure.

## Acceptance criteria

### Scenario 1: Successful CV parse
- **Given** a candidate has submitted an application with a CV
- **When** the parser worker processes the file
- **Then** the system extracts structured fields (contact, work history, skills, education, certifications, locations), stores them on `Resume.parsedJson`, sets `parseStatus = success`, and emits `application.parsed`.

### Scenario 2: Unreadable CV / parser failure
- **Given** a CV that cannot be parsed (corrupt or unsupported content)
- **When** the parser worker fails
- **Then** the system flags "Parser failed — review manually" on the recruiter UI and **does not** block the application.

### Scenario 3: Parsed data indexed for search
- **Given** a successfully parsed CV
- **When** parsing completes
- **Then** the structured fields are indexed so the candidate is discoverable in the talent database search.

## Notes / dependencies
- Depends on UC-CAND-01 / [apply-to-a-job](apply-to-a-job.md).
- Runs asynchronously after submit; feeds UC-CAND-07 / [search-talent-database](search-talent-database.md) and (P1) AI candidate-job matching.
- CVs are stored encrypted at rest (AES-256); logs must never contain PII.
