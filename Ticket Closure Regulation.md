# Ticket Management Regulation (Creation & Closure)

## 1. Purpose
To standardise how tickets (tasks, bugs, feature requests) are **created** and **closed** in the project. This ensures that every ticket is clearly defined before work starts and thoroughly peer‑reviewed before it is finalised.

## 2. Team and Roles

| Name | Role | Responsibility in this process |
|------|------|--------------------------------|
| **Daniel** | ML Engineer | Performs ML tasks; peer‑reviews ML and code tickets |
| **Alexandr** | ML Engineer | Performs ML tasks; peer‑reviews ML and code tickets |
| **Ilya** | Developer | Performs backend/frontend tasks; peer‑reviews code and parser tickets |
| **Vladimir** | Developer | Performs backend/frontend tasks; peer‑reviews code and parser tickets |
| **Daria** | Manager | Business approver; final decision‑maker; resolves disputes; ensures process compliance |

> **Key rule:** Since we do not have a team lead or senior engineer, **every technical ticket must be peer‑reviewed by one of the other three engineers/developers** (the reviewer cannot be the assignee). We encourage rotating reviewers across sprints to distribute knowledge and avoid bias.

---

## 3. Ticket Creation Criteria (Definition of Ready – DoR)

Before a ticket is placed in the backlog or assigned to a sprint, it **must** meet the following entry criteria. If any item is missing, the ticket should be returned to the creator for refinement.

| # | Criterion | Description |
|---|-----------|-------------|
| 1 | **Clear Title** | The title must be concise and self‑explanatory (e.g., "Fix login timeout on mobile", "Add new ML feature X"). |
| 2 | **Detailed Description** | Provides context: what is the problem or need, why is it important, and any relevant background information. |
| 3 | **Steps to Reproduce** (for bugs) | Exact steps, input data, environment, and actual vs. expected behaviour. Attach logs or screenshots if helpful. |
| 4 | **Acceptance Criteria (AC)** | A checklist of specific, measurable conditions that must be met for the ticket to be considered done (e.g., "User can upload file up to 10MB", "Inference latency < 200ms"). |
| 5 | **Definition of "Done"** | A clear statement of what the final deliverable looks like (e.g., a merged PR, a deployed model, updated docs). |
| 6 | **Assignee** | The ticket must be assigned to one specific person (Daniel, Alexandr, Ilya, or Vladimir). Unassigned tickets are not picked up. |
| 7 | **Sprint / Milestone** | The ticket must be linked to an active sprint or milestone (unless it's a backlog refinement item). |
| 8 | **Dependencies** | Clearly list any external dependencies (e.g., "Requires API endpoint from service X", "Depends on ticket #123"). If a dependency is missing, link to that ticket. |
| 9 | **Labels / Type** | Tag the ticket type: `Bug`, `Feature`, `Task`, `Research`, `DevOps`, `Documentation`. |

> **If the ticket does not meet these criteria**, the assignee has the right to reject it and send it back to the Manager (Daria) or the original reporter for refinement before starting work.

---

## 4. Definition of Ready for Closure (DoRC)

Before a ticket can be moved to the review stage, the assignee must ensure **all** of the following are satisfied:

- [ ] **Code / Artifact**  
  - Code follows project coding standards.  
  - All changes are committed to the correct branch.  
  - No placeholders, TODOs, or commented‑out code (except deliberate tech debt tracked separately).

- [ ] **Tests**  
  - For code: unit/integration tests are written and pass.  
  - For a bug: the failing scenario is reproduced – the fix is verified by an automated test or a manual checklist.  
  - For a feature: all specified usage scenarios have been tested.

- [ ] **Documentation**  
  - User documentation is updated (if required).  
  - Technical documentation (API, DB schema, architecture, model cards) is updated.  
  - Complex logic has inline code comments.

- [ ] **Ticket Comments & Description**  
  - The ticket contains a summary of the final solution.  
  - Links to PR/MR, test reports, or artifacts are included.  
  - If known limitations or follow‑up tasks exist, separate tickets are created and linked.

- [ ] **Self‑testing**  
  - The assignee has personally verified the fix/feature in a staging or test environment.

---

## 5. Step‑by‑Step Closure Process

| Step | Action | Responsible | Example Status |
|------|--------|-------------|----------------|
| **1** | Assignee completes the work and self‑checks against Section 4 (DoRC). | Assignee | `In Progress` → `Done` (or `Ready for Review`) |
| **2** | Assignee selects a **peer reviewer** from the other three technical team members (Daniel, Alexandr, Ilya, Vladimir – excluding themselves) and moves the ticket to `Review`. | Assignee | `Review` |
| **3** | Peer reviewer checks the ticket against Section 4 (DoRC). <br> • If **OK** → go to step 4.<br> • If **issues found** → return to assignee with clear comments (status `Rework`). | Peer Reviewer | `Review` → `Rework` (or back to `In Progress`) |
| **4** | After successful peer review, the reviewer moves the ticket to `Manager Approval`. | Peer Reviewer | `Review` → `Approval` |
| **5** | Daria (Manager) verifies that the delivered result meets the business need. <br> • If **satisfied** → move to `Closed`.<br> • If **not satisfied** → return with comments (`Rejected` or `Rework`). | Daria | `Approval` → `Closed` / `Rejected` |
| **6** | **Final closure** – the ticket is updated with: <br> • Actual time logged<br> • Closure date<br> • A final comment summarising the outcome and linking to any release/deployment. | Daria (or system) | `Closed` |

> **Note:** If Daria is the original ticket creator, she still performs step 5. The peer reviewer never acts as the business approver.

---

## 6. Who Reviews Whom (Peer Review Rules)

Since we have no team lead, the following guidelines apply for choosing a reviewer:

| Assignee | Suggested Reviewers |
|----------|----------------------|
| **Daniel** (ML) | Alexandr (ML) **or** Ilya / Vladimir (for code/integration parts) |
| **Alexandr** (ML) | Daniel (ML) **or** Ilya / Vladimir (for code/integration parts) |
| **Ilya** (Dev) | Vladimir (Dev) **or** Daniel / Alexandr (if ML/AI logic is involved) |
| **Vladimir** (Dev) | Ilya (Dev) **or** Daniel / Alexandr (if ML/AI logic is involved) |

- **Rotation principle:** To avoid overburdening one person, we strongly recommend rotating reviewers each sprint. For example, if Daniel reviews Alexandr's ticket in Sprint 1, Alexandr should review Daniel's in Sprint 2.
- **Conflict of interest:** The assignee must **never** review their own ticket.
- **If the ticket is purely ML/model‑related**, choose another ML engineer if available. If both ML engineers are busy, a developer can review for reproducibility and integration, but the final model validation should be signed off by the other ML engineer.

---

## 7. Comment Requirements on Closure

When closing a ticket, the Manager (Daria) or the final closer must leave a comment in this format:

> **Delivered:** [brief description of what was done]  
> **Peer‑reviewed by:** [reviewer name]  
> **Approved by (business):** [Daria / date]  
> **Artifacts:** [links to PR, test suite, model registry, documentation]  
> **Related tickets:** [EPIC, dependencies, created follow‑ups]  
> **Closure date:** YYYY-MM-DD

---

## 8. Exceptions and Special Cases

- **Duplicate ticket** – add a link to the original ticket and explain why it is a duplicate.
- **Won’t fix / Obsolete** – requires explicit approval from Daria, with a detailed reason. The peer reviewer must also agree on the technical justification.
- **Technical debt / Partial completion** – if a ticket is closed with known leftover work, this must be approved by Daria during a planning or retrospective meeting. A new follow‑up ticket must be created and linked immediately.

---

## 9. Accountability and SLAs

- **Violations** – closing a ticket without a peer review, without proper tests, or without the required comments will result in a warning. The ticket may be reopened, and the assignee must fix the gaps.
- **Review SLAs** – the peer reviewer must complete the review within **1 business day**. If they cannot, they must reassign or notify Daria.
- **Manager SLA** – Daria must provide business approval or feedback within **1 business day** of the ticket entering `Approval` status.
- **Audits** – Daria (or a delegated person) will perform random audits on closed tickets to ensure compliance with both the entry (DoR) and closure (DoRC) criteria.

---

**Effective date:** ________  
**Version:** 2.0  
**Document author:** ________
