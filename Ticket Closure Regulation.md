# Ticket Closure Regulation (Project Task)

## 1. Purpose
To ensure consistency, quality control, and transparency when completing work on a ticket (task/bug/feature request) before it is finally closed.

## 2. Roles and Responsibilities

| Role | Responsibility in the closure process |
|------|----------------------------------------|
| **Assignee** (Developer, Tester, Analyst) | Performs the task, provides results, initiates closure. |
| **Senior Tech Lead** | Reviews technical correctness, code quality, architecture compliance. |
| **Manager** | Acts as business approver – confirms the result meets the business need (if no dedicated PO). Also resolves disputes and ensures process compliance. |
| **Ticket Initiator** (Manager, Analyst, or any stakeholder) | Defines the original request; may participate in acceptance. |

> **Note:** The Manager can delegate acceptance to another stakeholder (e.g., a business user), but remains accountable for the final closure.

## 3. Definition of Ready for Closure (DoRC)

Before moving the ticket to “Ready for Review” or “Closure”, the assignee must ensure **all** of the following are satisfied:

- [ ] **Code / Artifact**  
  - Code follows project coding standards.  
  - All changes are committed to the correct branch.  
  - No placeholders, TODOs, or commented-out code (except deliberate tech debt tracked in separate tickets).

- [ ] **Tests**  
  - For code: unit/integration tests are written and pass.  
  - For a bug: the failing scenario is reproduced – the fix is verified by an automated test or checklist.  
  - For a feature: all specified usage scenarios have been tested.

- [ ] **Documentation**  
  - User documentation is updated (if required).  
  - Technical documentation (API, DB schema, architecture) is updated.  
  - Complex logic has inline code comments.

- [ ] **Ticket Comments & Description**  
  - The ticket contains a summary of the final solution.  
  - Links to PR/MR, test reports, artifacts are included.  
  - If there are known limitations or follow‑up tasks, separate tickets are created and linked.

- [ ] **QA Validation**  
  - For functional changes: the ticket has passed manual/automated QA testing.  
  - For a bug: verified that the defect no longer occurs.

## 4. Step‑by‑Step Closure Process

| Step | Action | Responsible | Example Status |
|------|--------|-------------|----------------|
| **1** | Assignee completes the work and self‑checks against Section 3. | Assignee | `In Progress` → `Done` (or `Ready for Review`) |
| **2** | Assignee assigns the **Senior Tech Lead** as reviewer and moves the ticket to `Review`. | Assignee | `Review` |
| **3** | Senior Tech Lead reviews the ticket against Section 3. <br> • If **OK** → go to step 4.<br> • If **issues found** → return to assignee with comments (status `Rework`). | Senior Tech Lead | `Review` → `Rework` (or back to `In Progress`) |
| **4** | After successful technical review, the Senior Tech Lead moves the ticket to `Manager Approval`. | Senior Tech Lead | `Review` → `Approval` |
| **5** | Manager (or delegated stakeholder) verifies that the delivered result solves the original business need. <br> • If **satisfied** → move to `Closed`.<br> • If **not satisfied** → return with comments (`Rejected` or `Rework`). | Manager | `Approval` → `Closed` / `Rejected` |
| **6** | **Final closure** – the ticket is updated (manually or automatically) with: <br> • Actual effort logged (time tracking)<br> • Closure date<br> • Result summary (optionally with release/deploy reference) | Manager or system | `Closed` |

> **Note:** If the Manager is also the ticket initiator, they perform step 5 directly. The Senior Tech Lead never acts as the business approver unless explicitly delegated by the Manager.

## 5. Who Reviews and Who Closes (by Ticket Type)

| Ticket Type | Reviewer | Final Closer |
|-------------|----------|---------------|
| **Code / Technical task** | Senior Tech Lead | Manager (after tech approval) |
| **Bug** | QA engineer (verification) + Senior Tech Lead (code) | Manager or QA lead (as delegated) |
| **Analytics / Research task** | Senior Tech Lead or Lead Analyst | Manager |
| **Documentation change** | Senior Tech Lead or a peer | Manager |
| **DevOps / Configuration** | Senior Tech Lead or Security engineer | Manager |

## 6. Comment Requirements on Closure

When closing a ticket, you MUST leave a comment in the following format:

> **Delivered:** [brief description]  
> **Verified by (tech):** [Senior Tech Lead name, date]  
> **Approved by (business):** [Manager name, date]  
> **Artifacts:** [links to PR, test suite, documentation]  
> **Related tickets:** [EPIC, dependencies, created follow‑ups]  
> **Closure date:** YYYY-MM-DD

## 7. Exceptions and Special Cases

- **Ticket closed as duplicate** – add a link to the primary ticket and a justification comment.
- **Ticket closed as won’t fix / obsolete** – requires approval from the Manager (and optionally Senior Tech Lead for technical impact), with a detailed reason.
- **Technical debt** – if a task is partially completed but closed by agreement, it must be explicitly approved by the Manager during a retrospective or planning meeting, and a follow‑up ticket must be created.

## 8. Accountability

- Violations of this regulation (closing without review, without tests, without comments) → assignee receives a warning; the ticket may be reopened.
- The Senior Tech Lead must complete the technical review within **1 business day** (adjustable per project).
- The Manager must provide business approval or feedback within **1 business day** (adjustable).
- The Manager (or delegated person) performs random audits of closed tickets for compliance.

---

**Effective date:** ________  
**Version:** 1.0  
**Document author:** ________
