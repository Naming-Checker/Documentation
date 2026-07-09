# Project Tracking — NamingChecker

## Purpose
This document defines how the team tracks progress, tasks, milestones, and deviations during the **NamingChecker** project. It complements the tactical plan and roadmap with day‑to‑day monitoring practices, aligned with our weekly sprint cadence and retrospective rhythm.

---

## Tracking Artifacts
- **GitHub Issues / Projects board** – all tasks, bugs, spikes, and reviews are tracked as issues with labels (phase, component, priority).
- **Roadmap.md** – high‑level milestones and deadlines (phase gates).
- **Tactical Plan** – detailed bi‑weekly sprint plan (though sprints themselves are weekly).
- **Weekly Status Notes** – short bulletins summarising completed work, blockers, and next steps (stored in `docs/weekly-reports/`).

> All tasks are assigned to specific team members and must be moved through `To Do` → `In Progress` → `Review` → `Approval` → `Closed` according to the [Ticket Closure Regulation](./ticket-closure-regulation.md).

---

## Cadence
| Activity | Frequency | Owner | Audience |
|----------|-----------|-------|----------|
| Daily stand‑up (async) | Weekdays (Mon–Sun) | Team | Team chat |
| Sprint planning | Every Monday (start of sprint) | Daria | Whole team |
| Backlog refinement | Weekly (usually Wednesday) | Daria + all | Whole team |
| Sprint review / demo | Every Friday | Daria | Stakeholders + team |
| Retrospective | **Every Sunday** (immediately after each sprint) | Daria | Team |

**Note:** Since each sprint lasts exactly one week, the retrospective is also held weekly to capture immediate lessons and adjust the next sprint’s plan.

---

## Progress Metrics
We track the following key indicators to ensure we stay on course:

- **Burndown** – remaining effort (in ideal hours) per sprint, updated daily.
- **Lead time** – from issue assignment to merge/closure, measured per ticket.
- **CI pass rate** – over the last 7 days (build and test status).
- **Test coverage** – trend (unit + integration).
- **Model accuracy & latency** – baselines tracked per evaluation run (for ML tasks).

For Sprint 5, the burndown starts at 94 hours; we monitor progress daily to catch any deviations early.

---

## Reporting
- **Weekly digest** prepared by Daria every Friday, covering:
  - Completed tasks vs. plan (including the sprint goal)
  - Blockers and risks (e.g., tasks stuck in `In Progress` for more than 2 days)
  - Key decisions made during the sprint
  - Upcoming priorities for the next sprint
- **Phase gate checklist** – verified by the entire team before progressing to the next project phase (e.g., from Discovery to MVP).

All reports are stored in `docs/weekly-reports/` and linked from the main repository.

---

## Deviation Handling
- If a task is delayed beyond its sprint, it is flagged with a `blocked` or `at‑risk` label.
- The root cause is discussed in the **weekly retrospective** (held every Friday).
- The roadmap and tactical plan are updated **only with team consensus** (typically during the sprint planning meeting on Monday).
- For critical blockers, an ad‑hoc sync is called immediately.

---

## Tooling
- **GitHub Projects** – for task board and tracking (we use the board view to visualise the current sprint).
- **GitHub Milestones** – for phase grouping (e.g., “Alpha”, “Beta”).
- **CI/CD dashboard** – for build and test status (integrated with GitHub Actions).
- **Shared Google Sheets** – for time logging and effort tracking (hours logged per ticket).



| Version | Date | Changes |
|---------|------|---------|
| 1.0     | Jul 06, 2026 | Initial version based on Sprint 5 snapshot and weekly cadence |
