# Evaluate knockout questions automatically

> **Use case:** UC-CAND-03 · **Domain:** Candidate Application & Screening · **Priority:** P0

## Story
As a **Recruiter**, I want **knockout questions to be evaluated automatically against each application** so that **applicants who fail mandatory requirements are filtered out without manual screening effort**.

## INVEST justification
- **Independent:** Knockout evaluation is a discrete rule-engine step on an application; it delivers screening value on its own.
- **Negotiable:** Question types, scoring thresholds, and rejection-email templates are open; the story fixes server-side evaluation and the auto-disposition behavior.
- **Valuable:** Removes clearly unqualified applicants from the recruiter's queue, focusing attention on viable candidates.
- **Estimable:** Bounded to synchronous evaluation at submit plus a post-parse re-evaluation pass.
- **Small:** A focused evaluation step, completable within a sprint.
- **Testable:** Verifiable by pass/fail outcomes, `AUTO_REJECTED` stage on failure, and the templated rejection email.

## Acceptance criteria

### Scenario 1: Application passes knockout
- **Given** an application with knockout answers that satisfy all mandatory criteria
- **When** the system evaluates them server-side at submission
- **Then** the application proceeds to `stage = NEW` and continues through the pipeline.

### Scenario 2: Application fails knockout at submission
- **Given** an application with a knockout answer that fails a mandatory criterion
- **When** the system evaluates it synchronously
- **Then** the application is set to `stage = AUTO_REJECTED` and a templated rejection email is sent with the reason.

### Scenario 3: Post-parse re-evaluation
- **Given** a knockout rule references parsed CV data (e.g., "minimum 5 years X experience")
- **When** the CV finishes parsing
- **Then** the knockout engine re-evaluates against the parsed data and updates the application's pass/fail outcome.

## Notes / dependencies
- Depends on UC-CAND-01 / [apply-to-a-job](apply-to-a-job.md); the post-parse pass depends on UC-CAND-02 / [auto-parse-cv](auto-parse-cv.md).
- Knockout questions are **always evaluated server-side** — never trust the client.
- Distinct from AI fit scoring, which is decision support and never auto-rejects (P1).
