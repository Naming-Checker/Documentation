# Project Tracking — NamingChecker

## Purpose

We use this document to keep the plan and the GitHub board consistent. The strategic plan explains why a block of work matters and when it should finish; the board shows the issues the team is actually working on.

## Documents and tools we use

- [GitHub Project — Tasks](https://github.com/orgs/Naming-Checker/projects/3): issues, owners, sprint assignment, status, `Ideal Hours`, and `Effort`.
- [Roadmap](Roadmap.md): the overall direction and key dates.
- [June–July 2026 Strategic Plan](Strategic/Strategic_Plan_June-July_2026.md): the agreed Sprint 1–7 baseline and milestone results for 1 June–26 July.
- [MoSCoW](MoSCoW.md): product scope and priority.
- The tactical plan: implementation details and quality gates.
- Weekly notes: a short comparison of the board with the active plan.

## Where to look

| Question | Use |
|----------|-----|
| Why and by when is the work required? | Roadmap and active strategic plan |
| What result closes a milestone? | Strategic-plan exit criteria |
| Which issue is being executed and what is its status? | Tasks board and linked GitHub issue |
| What is included in product scope? | MoSCoW and requirements |
| What evidence proves completion? | Pull request, test/model report, dashboard, documentation, or demo linked from the issue |

The sprint in the plan and the iteration on the board should match. If they do not, we treat that as a planning deviation and resolve it during refinement instead of keeping two different versions.

## Cadence

| Activity | Frequency | Owner | Audience |
|----------|-----------|-------|----------|
| Daily stand-up (async) | Weekdays | — | Team chat |
| Sprint planning | Before each board iteration | Daria | Whole team |
| Backlog refinement | Weekly | Daria + all | Whole team |
| Tracking-data review | Before sprint close | Daria + issue owners | Whole team |
| Milestone review / demo | At each strategic-plan exit date | Daria | Stakeholders + team |
| Retrospective | At milestone close | Daria | Team |

For the 1 June–26 July baseline, the iterations are:

| Sprint | Dates | Strategic milestone |
|--------|-------|---------------------|
| Sprint 1 | 1–13 June | MS1 — Foundation and observability |
| Sprint 2 | 14–20 June | MS1 — Foundation and observability |
| Sprint 3 | 21–28 June | MS2 — Integrated product demo |
| Sprint 4 | 29 June–5 July | MS3 — Quality and performance readiness |
| Sprint 5 | 6–12 July | MS3 — Quality and performance readiness |
| Sprint 6 | 13–19 July | MS4 — Optimization and release readiness |
| Sprint 7 | 20–26 July | MS4 — Optimization and release readiness |

## What we check

- Open and completed issues in the current sprint.
- Planned `Ideal Hours` versus completed hours.
- Estimate error (`Effort - Ideal Hours`) for issues where both values are filled in.
- Model quality from the evaluation run linked to the issue.
- Latency, throughput, and error rate from the load-test report.
- Milestone exit criteria and the evidence that supports them.

## Reporting

The weekly note is prepared by Daria and answers six practical questions:

1. Which milestone and sprint are we in?
2. What did we plan and what was actually completed?
3. What result can we show, and where is the evidence?
4. What is blocked or at risk?
5. If the plan changed, what is the impact and who owns the recovery action?
6. Do we still expect to meet the milestone date?

At milestone close, the team checks the exit criteria from the strategic plan. A status note links to the relevant milestone and issues. The final report uses the same links so that its conclusions can be checked.

## Required Task Data

Before we put an issue into an active sprint, it needs:

- a repository issue with acceptance criteria or a Definition of Done;
- an assignee;
- a Sprint;
- a Status;
- `Ideal Hours`;
- a clear relationship to a strategic milestone.

Before we accept it as `Done`, it needs:

- completion evidence linked from the issue;
- actual `Effort`;
- satisfied acceptance criteria or Definition of Done;
- no unresolved blocker affecting the claimed result.

## Deviation Handling

- A delayed issue is marked `blocked` or `at-risk`.
- The weekly note records the reason, effect on the milestone, owner, next action, and proposed date.
- Moving work to another sprint requires team agreement. We update the board and the active plan during the same review.
- New work added after sprint start must state what planned work or capacity it replaces.
- Closed issues alone do not close a milestone; we also check the agreed result and evidence.
- We do not rewrite earlier status reports. Finished sprints show actual results, the current sprint shows its current state, and later sprints remain forecasts.

## Naming in reports

We use the milestone identifiers `MS1`–`MS4` from the strategic plan in weekly notes and final reporting. Issue links identify the actual work; report and dashboard links provide the measurements.
