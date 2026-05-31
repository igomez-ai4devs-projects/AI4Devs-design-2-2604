# LTI-IGR — Project Documentation Hub

> Central index linking the main project artifacts: **user stories**, the **product backlog**, and the **work tickets** (with their effort estimation).
> **System:** LTI-IGR — an AI-native Applicant Tracking System (ATS).

---

## 1. User Stories

**Objective.** The user stories decompose the product's core value loop — the hiring funnel — into deliverable, value-oriented increments. They cover the three core P0 domains (Requisitions, Candidates, Interviews): a role is **opened** (requisition → approval → published posting), **filled** with applicants (apply → CV parsing → knockout screening → talent database & pipeline), and **converted** into a hire (interview scheduling → structured scorecards → debrief → hire decision). Each story follows the standard *As a… I want… so that…* format, is validated against **INVEST**, and carries **Given/When/Then** acceptance criteria.

- **[User Stories — README / index](user-stories/README.md):** analysis summary, backlog summary table, domain coverage, and what is out of scope for the MVP.

### Requisitions & Job Posting
- **[Create a requisition from a template](user-stories/create-requisition-from-template.md):** fast, consistent, compliant headcount request — the funnel origin.
- **[Configure the requisition approval chain](user-stories/configure-approval-chain.md):** enables automatic, governed approval routing per department / cost center.
- **[Approve or reject a requisition](user-stories/approve-or-reject-requisition.md):** headcount-spend governance before any job goes live.
- **[Publish a job to the career site](user-stories/publish-job-to-career-site.md):** first candidate-facing artifact; opens the funnel.
- **[Close, pause, or cancel a requisition](user-stories/close-pause-cancel-requisition.md):** keeps postings and reporting accurate across the lifecycle.

### Candidate Application & Screening
- **[Apply to a job](user-stories/apply-to-a-job.md):** the funnel entry point — creates the application.
- **[Automatically parse CVs into structured fields](user-stories/auto-parse-cv.md):** eliminates manual data entry; enables search and screening.
- **[Evaluate knockout questions automatically](user-stories/evaluate-knockout-questions.md):** filters unqualified applicants without manual effort.
- **[Manually add a candidate](user-stories/manually-add-candidate.md):** brings sourced or referred talent into the pipeline.
- **[Search and filter the talent database](user-stories/search-talent-database.md):** turns the database into a reusable talent asset.
- **[Move a candidate across pipeline stages](user-stories/move-candidate-pipeline-stage.md):** the core daily workflow that keeps the funnel truthful.
- **[Disposition a candidate with a reason and email](user-stories/reject-candidate-with-reason.md):** consistent candidate communication with a compliant audit trail.
- **[Manage GDPR consent and right-to-be-forgotten](user-stories/gdpr-consent-and-erasure.md):** mandatory legal compliance for candidate data.

### Interviews & Hire Decision
- **[Schedule an interview with calendar sync](user-stories/schedule-interview-calendar-sync.md):** removes scheduling overhead; a lever on time-to-hire.
- **[Candidate self-schedules or reschedules](user-stories/candidate-self-schedule-interview.md):** reduces friction and candidate drop-off.
- **[Send an interview kit to interviewers](user-stories/send-interview-kit.md):** prepared, structured, fair interviews.
- **[Send automated interview reminders](user-stories/automated-interview-reminders.md):** lowers the no-show rate.
- **[Provision a video meeting for an interview](user-stories/provision-video-meeting.md):** frictionless remote interview access.
- **[Submit a structured scorecard](user-stories/submit-structured-scorecard.md):** consistent, comparable, bias-mitigated evidence.
- **[Run a collaborative debrief](user-stories/collaborative-debrief.md):** calibration that reduces bias and improves decision quality.
- **[Record the hire / no-hire decision](user-stories/record-hire-decision.md):** the funnel conversion point — applications become hires.

---

## 2. Backlog

**Objective.** The backlog turns the user stories into a single, fully ordered, value-driven delivery sequence. It scores every story against explicit prioritization factors (business value, urgency, dependencies, implementation cost, risk, user feedback, technological maturity), resolves ties with enabler-first logic, and groups the result into a recommended delivery roadmap. It is the team's prioritized "what comes next" view and is meant to be re-evaluated as the project evolves.

- **[Product Backlog](backlog.md):** analysis summary, prioritization criteria and technique, prioritization matrix, the fully ordered backlog table, and the recommended delivery order / roadmap.

---

## 3. Tickets — Configure the requisition approval chain

**Objective.** The tickets break the **[Configure the requisition approval chain](user-stories/configure-approval-chain.md)** user story (UC-REQ-10, a P0 enabler) into self-contained, actionable work items for the engineering team. Each ticket has a clear description, testable acceptance criteria with validation tests, priority, effort estimate, assignee, labels, and traceability back to the source story. Together they deliver the capability end to end — data model → API → rules → resolution engine → SLA config → admin UI → security & audit.

- **[Tickets — README / index](tickets/configure-approval-chain/README.md):** decomposition summary, tickets summary table, dependency order, and acceptance-criteria coverage map.
- **[Effort estimation](tickets/configure-approval-chain/estimate-effort.md):** Planning Poker on the Fibonacci scale (story points), cross-mapped to T-shirt sizes and an indicative hours range, with per-ticket rationale and a 2-sprint projection (37 points total).

### Tickets
- **[Data model & migrations for approval chains](tickets/configure-approval-chain/approval-chain-data-model.md)** *(Technical Task, Critical, 3 pts):* persistence foundation — `ApprovalChain`, `ApprovalChainStep`, and `ApprovalChainCondition` tables with tenant isolation and constraints.
- **[Backend API — Approval chain CRUD](tickets/configure-approval-chain/approval-chain-crud-api.md)** *(Feature, High, 5 pts):* create/read/update/list/deactivate chains scoped to a department or cost center.
- **[Conditional approval steps (predefined rules)](tickets/configure-approval-chain/conditional-step-rules.md)** *(Feature, High, 5 pts):* predefined conditions (LEVEL / SALARY_BAND / COST_CENTER) that add steps such as an executive approver for senior roles.
- **[Approval chain resolution & snapshot engine](tickets/configure-approval-chain/chain-resolution-engine.md)** *(Feature, Critical, 8 pts):* resolves a saved chain into an ordered approver sequence for a requisition and snapshots it at submission time — the core enabler.
- **[SLA per approval step (configuration)](tickets/configure-approval-chain/sla-per-step-config.md)** *(Feature, Medium, 3 pts):* stores and exposes a per-step SLA (runtime auto-escalation is owned by UC-REQ-02).
- **[Admin UI — Approval chain builder](tickets/configure-approval-chain/admin-chain-builder-ui.md)** *(Feature, High, 8 pts):* the admin-facing screen to build chains — scope, reorderable steps, conditional rules, and SLAs.
- **[RBAC & audit logging for chain configuration](tickets/configure-approval-chain/rbac-and-audit-logging.md)** *(Technical Task, High, 5 pts):* restricts configuration to Admin / Talent Ops and logs every change immutably (7-year retention).

---

## Related references

- **[PRD](README_PRD.md)** — product requirements document.
- **[Specs catalog](specs/README.md)** — domain specifications and high-level architecture ([design.md](specs/design.md)).
