# LTI-IGR — Principal User Stories (MVP)

> **Source PRD:** [`../README_PRD.md`](../README_PRD.md) · **Use-case catalog:** [`../specs/README.md`](../specs/README.md)
> **Scope:** the three core funnel domains — Requisitions, Candidates, Interviews · **Priority:** P0 (must-have for MVP)
> **Format:** standard User Story + INVEST + Given/When/Then acceptance criteria

---

## 1. Analysis summary

**Product goal.** LTI-IGR is an AI-native Applicant Tracking System (ATS). Its core value loop is the hiring funnel: a role is **opened** (requisition → approval → published job posting), **filled** with applicants (apply → CV parsing → knockout screening → talent database & pipeline), and **converted** into a hire (interview scheduling → structured scorecards → debrief → hire decision). These three domains gate every downstream capability, so they are where the principal user stories live. Per the agreed scope, this backlog covers only the **P0 must-have** use cases of these three domains; P1 differentiators (AI candidate-job matching, multi-board distribution, talent pools, deduplication) and other domains (Auth, Offers, Analytics, Sourcing) are deliberately out of scope here.

**Actors covered.** Drawn from the role catalog (R1–R9): **Hiring Manager** (requisition intake, hire decision), **Approver** (requisition governance), **Recruiter** (publication, pipeline, scheduling — the operational owner), **Admin / Talent Ops** (approval-chain configuration), **Candidate** (apply, self-schedule, consent), **Interviewer** (scorecards), **DPO** (GDPR erasure), and the **System / AI agent** as the actor behind automations (CV parsing, knockout evaluation, reminders, kit and video provisioning). Where a use case is a system automation, the story is framed around the human who receives the value.

**Features covered.** 21 stories across three domains: requisition creation, approval, publication, lifecycle and approval-chain setup (Requisitions); apply flow, CV parsing, knockout screening, manual add, talent search, pipeline movement, dispositioning and GDPR consent/erasure (Candidates); interview scheduling, candidate self-scheduling, interview kits, reminders, video provisioning, structured scorecards, collaborative debrief and the hire decision (Interviews). Cross-cutting compliance rules (pay transparency, EEO statement, GDPR, blind scorecards, 7-year audit retention, AI-as-decision-support-only) are embedded as acceptance criteria where they bind.

---

## 2. Backlog summary table

| # | UC ID | Story | Actor | Value | Priority |
|---|---|---|---|---|---|
| 1 | UC-REQ-01 | [Create a requisition from a template](create-requisition-from-template.md) | Hiring Manager | Fast, consistent, compliant headcount request — funnel origin | High |
| 2 | UC-REQ-10 | [Configure the requisition approval chain](configure-approval-chain.md) | Admin / Talent Ops | Enables automatic, governed approval routing | High |
| 3 | UC-REQ-02 | [Approve or reject a requisition](approve-or-reject-requisition.md) | Approver | Headcount-spend governance before any job goes live | High |
| 4 | UC-REQ-03 | [Publish a job to the career site](publish-job-to-career-site.md) | Recruiter | First candidate-facing artifact; opens the funnel | High |
| 5 | UC-REQ-07 | [Close, pause, or cancel a requisition](close-pause-cancel-requisition.md) | Recruiter | Keeps postings and reporting accurate | High |
| 6 | UC-CAND-01 | [Apply to a job](apply-to-a-job.md) | Candidate | Funnel entry point — creates the application | High |
| 7 | UC-CAND-02 | [Automatically parse CVs into structured fields](auto-parse-cv.md) | Recruiter (System) | Eliminates manual data entry; enables search/screening | High |
| 8 | UC-CAND-03 | [Evaluate knockout questions automatically](evaluate-knockout-questions.md) | Recruiter (System) | Filters unqualified applicants without manual effort | High |
| 9 | UC-CAND-06 | [Manually add a candidate](manually-add-candidate.md) | Recruiter | Brings sourced/referred talent into the pipeline | High |
| 10 | UC-CAND-07 | [Search and filter the talent database](search-talent-database.md) | Recruiter | Turns the database into a reusable talent asset | High |
| 11 | UC-CAND-09 | [Move a candidate across pipeline stages](move-candidate-pipeline-stage.md) | Recruiter | Core daily workflow; keeps the funnel truthful | High |
| 12 | UC-CAND-10 | [Disposition a candidate with a reason and email](reject-candidate-with-reason.md) | Recruiter | Consistent candidate comms; compliant audit trail | High |
| 13 | UC-CAND-12 | [Manage GDPR consent and right-to-be-forgotten](gdpr-consent-and-erasure.md) | Candidate / DPO | Mandatory legal compliance | High |
| 14 | UC-INT-01 | [Schedule an interview with calendar sync](schedule-interview-calendar-sync.md) | Recruiter | Removes scheduling overhead; lever on time-to-hire | High |
| 15 | UC-INT-02 | [Candidate self-schedules or reschedules](candidate-self-schedule-interview.md) | Candidate | Reduces friction and drop-off | High |
| 16 | UC-INT-03 | [Send an interview kit to interviewers](send-interview-kit.md) | Interviewer (System) | Prepared, structured, fair interviews | High |
| 17 | UC-INT-04 | [Send automated interview reminders](automated-interview-reminders.md) | Recruiter (System) | Lowers no-show rate | High |
| 18 | UC-INT-05 | [Provision a video meeting for an interview](provision-video-meeting.md) | Recruiter (System) | Frictionless remote interview access | High |
| 19 | UC-INT-06 | [Submit a structured scorecard](submit-structured-scorecard.md) | Interviewer | Consistent, comparable, bias-mitigated evidence | High |
| 20 | UC-INT-07 | [Run a collaborative debrief](collaborative-debrief.md) | Hiring Manager + Panel | Calibration reduces bias, improves decision quality | High |
| 21 | UC-INT-08 | [Record the hire / no-hire decision](record-hire-decision.md) | Hiring Manager | Funnel conversion point — applications become hires | High |

> All 21 stories are **P0**, hence uniformly High priority. Within the funnel they should be delivered roughly top-to-bottom: requisition setup (1–5) → application & screening (6–13) → interviews & decision (14–21), respecting the dependencies noted in each story.

---

## 3. Domain coverage

| Domain | P0 stories | Spec |
|---|---|---|
| Requisitions & Job Posting | 5 (UC-REQ-01, 02, 03, 07, 10) | [`../specs/requisitions/spec.md`](../specs/requisitions/spec.md) |
| Candidate Application & Screening | 8 (UC-CAND-01, 02, 03, 06, 07, 09, 10, 12) | [`../specs/candidates/spec.md`](../specs/candidates/spec.md) |
| Interviews & Hire Decision | 8 (UC-INT-01…08) | [`../specs/interviews/spec.md`](../specs/interviews/spec.md) |

## 4. Out of scope (this backlog)

- **P1 differentiators:** AI candidate-job match scoring (UC-CAND-04), deduplication/merge (UC-CAND-05), tag/segment (UC-CAND-08), talent pools (UC-CAND-11), multi-board distribution (UC-REQ-04), social/internal posting (UC-REQ-05/06), reopen (UC-REQ-08), JD template library management (UC-REQ-09), interviewer-side cancel/reschedule (UC-INT-09), kit/rubric library management (UC-INT-10).
- **Other domains:** Auth & Access, Offers & Onboarding, Analytics & Compliance, Sourcing, Assessments, Communications.
