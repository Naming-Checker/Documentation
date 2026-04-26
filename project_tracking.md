# Project Tracking — NamingChecker

## Purpose
This document defines how the team tracks progress, tasks, milestones, and deviations during the NamingChecker project. It complements the tactical plan and roadmap with day-to-day monitoring practices.

## Tracking Artifacts
- **GitHub Issues / Projects board** – all tasks, bugs, spikes, and reviews are tracked as issues with labels (phase, component, priority).
- **Roadmap.md** – high-level milestones and deadlines.
- **Tactical Plan** – detailed bi‑weekly sprint plan.
- **Weekly Status Notes** – short bulletins summarising completed work, blockers, and next steps (stored in `docs/weekly-reports/`).

## Cadence
| Activity | Frequency | Owner | Audience |
|----------|-----------|-------|----------|
| Daily stand‑up (async) | Weekdays | – | Team chat |
| Sprint planning | Every 2 weeks | Daria | Whole team |
| Backlog refinement | Weekly | Daria + all | Whole team |
| Milestone review / demo | At each phase gate | Daria | Stakeholders + team |
| Retrospective | End of each month | Daria | Team |

## Progress Metrics
- **Burndown** of open issues per sprint.
- **Lead time** from issue assignment to merge.
- **CI pass rate** over the last 7 days.
- **Test coverage** trend.
- **Model accuracy** and latency baselines (tracked per evaluation run).

## Reporting
- **Weekly digest** prepared by Daria, covering:
  - Completed tasks vs. plan
  - Blockers and risks
  - Key decisions
  - Upcoming priorities
- **Phase gate checklist** verified by the entire team before progressing to the next phase.

## Deviation Handling
- If a task is delayed beyond its sprint, it is flagged with a `blocked` or `at‑risk` label.
- Root cause is discussed in the next retrospective.
- The roadmap and tactical plan are updated only with team consensus.

## Tooling
- GitHub Projects for task board and tracking.
- GitHub Milestones for phase grouping.
- CI/CD dashboard for build and test status.
