# Search and filter the talent database

> **Use case:** UC-CAND-07 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Recruiter**, I want **to search and filter the talent database by full text and structured attributes** so that **I can quickly surface qualified candidates for an open requisition**.

## INVEST justification
- **Independent:** Search operates over already-indexed candidate data and delivers value independently of pipeline actions.
- **Negotiable:** Filter set, ranking, and saved-search behavior are open; the story fixes full-text plus structured filtering over the talent database.
- **Valuable:** Turns the candidate database into a reusable talent asset rather than a write-only inbox.
- **Estimable:** Bounded to a query interface against the search index with the defined filter facets.
- **Small:** A focused search-and-results screen, completable within a sprint.
- **Testable:** Verifiable by queries returning the expected candidates for given filter combinations.

## Acceptance criteria

### Scenario 1: Full-text search
- **Given** parsed candidate profiles exist in the talent database
- **When** I enter free-text keywords (e.g., a skill or job title)
- **Then** the system returns matching candidates ranked by relevance.

### Scenario 2: Structured filtering
- **Given** I am viewing the talent database
- **When** I apply structured filters (skills, location, experience, stage, source, tags)
- **Then** the system returns only candidates matching all selected filters.

### Scenario 3: Tenant isolation
- **Given** I am searching within my organization
- **When** I run any query
- **Then** results never include candidates from other tenants.

## Notes / dependencies
- Depends on UC-CAND-02 / [auto-parse-cv](auto-parse-cv.md) for indexed structured data.
- Backed by full-text search (OpenSearch) plus structured filters.
- Filtering by AI fit score becomes available once AI matching (UC-CAND-04, P1) ships.
