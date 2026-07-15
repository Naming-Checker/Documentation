# Strategic Plan — June–July 2026

**Planning horizon:** 1 June–26 July 2026  
**Status date:** 15 July 2026  
**Execution board:** [GitHub Project — Tasks](https://github.com/orgs/Naming-Checker/projects/3)  
**Product scope:** [MoSCoW](../MoSCoW.md)  
**High-level roadmap:** [Roadmap](../Roadmap.md)  
**Tracking rules:** [Project Tracking](../project_tracking.md)

## 1. Why this plan was created

The original roadmap described June and July at a monthly level. Once weekly iterations started, the actual order changed: observability and scrapers came first, while load testing and final model tuning moved to July. This document records the plan the team is using for those iterations and keeps it tied to the Tasks board.

The dates and estimates below come from the board, not from a reconstructed ideal schedule. As of 15 July, Sprints 1–5 are finished, Sprint 6 is in progress, and Sprint 7 remains the plan for 20–26 July.

## 2. What we need to have by 26 July

- The backend, frontend, text model, visual model, monitoring, and scrapers work together on the test stand.
- Model changes are checked on repeatable datasets; reports include measured results rather than only implementation status.
- The team completes the load-test sequence: goals, environment, scenarios, baseline, bottleneck analysis, changes, and a repeated run.
- Final materials describe what was delivered, what did not fit, and which measurements support the conclusions.
- Issues planned for the period have a final status. Completed issues also have actual `Effort` on the board.

## 3. Milestone Overview

| Milestone | Period | Sprints | Planned effort | Main outcome |
|-----------|--------|---------|----------------|--------------|
| MS1 — Foundation and observability | 1–20 June | 1–2 | 197 h | Observable test stand, preprocessing, initial model and scraper capabilities |
| MS2 — Integrated product demo | 21–28 June | 3 | 90 h | Integrated frontend and services, metrics, model improvements, stakeholder demo |
| MS3 — Quality and performance readiness | 29 June–12 July | 4–5 | 182 h | Quality extensions, resilient scraping, alerting, and load-test readiness |
| MS4 — Optimization and release readiness | 13–26 July | 6–7 | 192 h | Measured baseline, optimized models and scraping, final reporting | 
| **Total** | **1 June–26 July** | **1–7** | **661 h** | **Release-ready increment with measured results** |

## 4. How the sprints are grouped

We grouped the seven board iterations into four milestones. The grouping follows dependencies in the work: first make the stand observable, then demonstrate an integrated flow, prepare quality and load testing, and only after that measure and optimize.

### MS1 — Foundation and Observability

**Period:** 1–20 June

During the first two sprints we needed enough infrastructure to see what the services were doing and enough data work for the model teams to proceed. This included:

- deploy ELK logging, application logs, APM traces, indices, retention, Prometheus, and Grafana;
- implement initial Yandex scrapers and webhook integration;
- prepare text datasets, preprocessing, and candidate algorithms;
- establish a visual-similarity evaluation dataset and begin fine-tuning;
- define sprint workload and issue-management rules.

We considered MS1 closed when the services were observable on the stand, scraper execution worked through the backend, model inputs could be reproduced, and all 20 planned issues were closed. This was completed by 20 June.

### MS2 — Integrated Product Demo

**Period:** 21–28 June

Sprint 3 was deliberately kept as a separate milestone: it ended with the MoSP presentation and therefore had to produce something that could be shown as one system. The work was:

- expose unified metrics and provision Grafana dashboards as code;
- integrate scraper results with the frontend;
- package the text model and add the LaBSE semantic encoder;
- complete the second visual-model fine-tuning stage;
- groom the backlog and prepare the MoSP presentation.

MS2 was closed after all 9 issues were finished and the frontend flow, service metrics, dashboards, and model updates could be demonstrated. This was completed by 28 June.

### MS3 — Quality and Performance Readiness

**Period:** 29 June–12 July

Sprints 4 and 5 moved the focus from basic integration to quality. At the same time, we prepared load testing before trying to optimize anything. The work included:

- configure service and infrastructure alerting;
- add YouTube scraping and improve resilience of Yandex scrapers;
- extend visual datasets and introduce font and color analysis;
- improve text-result ranking;
- define load-testing goals, infrastructure, and executable scenarios;
- incorporate presentation feedback and synchronize tactical planning.

MS3 was closed after all 13 issues were finished and the team could launch the documented load-test scenarios against the prepared environment. This was completed by 12 July.

### MS4 — Optimization and Release Readiness

**Period:** 13–26 July

The last two sprints depend on the preparation done in Sprint 5. We first capture a baseline and identify bottlenecks, then make targeted changes and repeat the measurements. Model and scraper work follows the same pattern: investigate a concrete quality problem before the final optimization. Planned work:

- run baseline and repeated load tests, identify bottlenecks, and compare results;
- implement Google Books scraping and improve overall scraping quality;
- fine-tune and combine visual, font, and color channels;
- identify text-ranking noise and optimize the text model;
- prepare final project reporting and presentation.

MS4 closes on 26 July if Sprint 6–7 work is complete and the final materials link to performance reports, model evaluations, and issue results. If something does not fit, the report must name the owner, reason, impact, and revised date instead of silently moving the work. Sprint 6 is currently active; Sprint 7 is still a forecast.

## 5. Sprint Baseline and Results

### Sprint 1 — 1–13 June

**Objective:** logging and tracing foundation, initial datasets, model research, and scraper coverage.  
**Planned effort:** 104 h. **Status:** Completed.

| Area | Planned issues | Expected and actual result |
|------|----------------|----------------------------|
| Backend | [#49](https://github.com/Naming-Checker/Backend/issues/49), [#50](https://github.com/Naming-Checker/Backend/issues/50), [#51](https://github.com/Naming-Checker/Backend/issues/51), [#52](https://github.com/Naming-Checker/Backend/issues/52), [#53](https://github.com/Naming-Checker/Backend/issues/53), [#55](https://github.com/Naming-Checker/Backend/issues/55) | Yandex Video/Music scrapers and ELK/APM observability delivered |
| Text model | [#7](https://github.com/Naming-Checker/TextModel/issues/7), [#9](https://github.com/Naming-Checker/TextModel/issues/9) | Approaches reviewed and test dataset prepared |
| Visual model | [#12](https://github.com/Naming-Checker/VisualModel/issues/12) | Evaluation dataset labeled |
| Project management | [#5](https://github.com/Naming-Checker/Documentation/issues/5) | Sprint workload planned and balanced |

**Exit evidence:** all 10 issues are `Done`.

### Sprint 2 — 14–20 June

**Objective:** operational monitoring, data preprocessing, scraper integration, and model fine-tuning.  
**Planned effort:** 93 h. **Status:** Completed.

| Area | Planned issues | Expected and actual result |
|------|----------------|----------------------------|
| Backend | [#56](https://github.com/Naming-Checker/Backend/issues/56), [#57](https://github.com/Naming-Checker/Backend/issues/57), [#58](https://github.com/Naming-Checker/Backend/issues/58), [#64](https://github.com/Naming-Checker/Backend/issues/64) | Indices, retention, Grafana, and scraper webhook delivered |
| Text model | [#10](https://github.com/Naming-Checker/TextModel/issues/10), [#11](https://github.com/Naming-Checker/TextModel/issues/11), [#12](https://github.com/Naming-Checker/TextModel/issues/12) | Candidate methods, extraction, and preprocessing implemented |
| Visual model | [#14](https://github.com/Naming-Checker/VisualModel/issues/14), [#17](https://github.com/Naming-Checker/VisualModel/issues/17) | Quality evaluated and fine-tuning stage 1 completed |
| Project management | [#6](https://github.com/Naming-Checker/Documentation/issues/6) | Issue-management process documented |

**Exit evidence:** all 10 issues are `Done`.

### Sprint 3 — 21–28 June

**Objective:** integrated demo, unified monitoring, and model improvements.  
**Planned effort:** 90 h. **Status:** Completed.

| Area | Planned issues | Expected and actual result |
|------|----------------|----------------------------|
| Product and backend | [Backend #25](https://github.com/Naming-Checker/Backend/issues/25), [Backend #59](https://github.com/Naming-Checker/Backend/issues/59), [Frontend #2](https://github.com/Naming-Checker/Frontend/issues/2) | Unified metrics, provisioned dashboards, and frontend integration delivered |
| Models | [TextModel #13](https://github.com/Naming-Checker/TextModel/issues/13), [TextModel #15](https://github.com/Naming-Checker/TextModel/issues/15), [VisualModel #18](https://github.com/Naming-Checker/VisualModel/issues/18) | Installable text package, LaBSE encoder, and visual fine-tuning stage 2 delivered |
| Project management | [#4](https://github.com/Naming-Checker/Documentation/issues/4), [#7](https://github.com/Naming-Checker/Documentation/issues/7), [#8](https://github.com/Naming-Checker/Documentation/issues/8) | Meeting decisions, grooming, MoSP presentation and rehearsal completed |

**Exit evidence:** all 9 issues are `Done`.

### Sprint 4 — 29 June–5 July

**Objective:** alerting, source expansion, visual-quality experiments, and feedback processing.  
**Planned effort:** 90 h. **Status:** Completed.

| Area | Planned issues | Expected and actual result |
|------|----------------|----------------------------|
| Backend | [#60](https://github.com/Naming-Checker/Backend/issues/60), [#80](https://github.com/Naming-Checker/Backend/issues/80) | Operational alerts and YouTube scraper delivered |
| Visual model | [#16](https://github.com/Naming-Checker/VisualModel/issues/16), [#21](https://github.com/Naming-Checker/VisualModel/issues/21), [#23](https://github.com/Naming-Checker/VisualModel/issues/23) | Font datasets analyzed, color channel implemented, dataset extended |
| Project management | [#9](https://github.com/Naming-Checker/Documentation/issues/9) | Presentation feedback analyzed |

**Exit evidence:** all 6 issues are `Done`.

### Sprint 5 — 6–12 July

**Objective:** load-test readiness, ranking quality, resilient scraping, and visual color comparison.  
**Planned effort:** 92 h. **Status:** Completed.

| Area | Planned issues | Expected and actual result |
|------|----------------|----------------------------|
| Backend | [#73](https://github.com/Naming-Checker/Backend/issues/73), [#74](https://github.com/Naming-Checker/Backend/issues/74), [#75](https://github.com/Naming-Checker/Backend/issues/75), [#81](https://github.com/Naming-Checker/Backend/issues/81) | Goals, environment, scenarios, and resilient Yandex scraping delivered |
| Models | [TextModel #18](https://github.com/Naming-Checker/TextModel/issues/18), [VisualModel #22](https://github.com/Naming-Checker/VisualModel/issues/22) | Ranking and color-based logo comparison improved |
| Project management | [#10](https://github.com/Naming-Checker/Documentation/issues/10) | Tactical plan and sprint consistency reviewed |

**Exit evidence:** all 7 issues are `Done`. Missing `Effort` values remain a tracking-data action, not a delivery-status change.

### Sprint 6 — 13–19 July

**Objective:** establish the performance baseline and consolidate text, visual, and scraping quality work.  
**Planned effort:** 98 h. **Status:** In progress on 15 July.

| Area | Planned issues | Expected result | Status |
|------|----------------|-----------------|--------|
| Performance | [Backend #76](https://github.com/Naming-Checker/Backend/issues/76), [Backend #77](https://github.com/Naming-Checker/Backend/issues/77) | Baseline report and prioritized bottlenecks | In progress / To Do |
| Scraping | [Backend #83](https://github.com/Naming-Checker/Backend/issues/83) | Google Books scraper integrated | In progress |
| Text model | [#17](https://github.com/Naming-Checker/TextModel/issues/17) | Main sources of ranking noise identified | To Do |
| Visual model | [#13](https://github.com/Naming-Checker/VisualModel/issues/13), [#24](https://github.com/Naming-Checker/VisualModel/issues/24), [#29](https://github.com/Naming-Checker/VisualModel/issues/29) | Font integration, fine-tuned model, combined color channel | In progress / To Do |
| Project management | [#11](https://github.com/Naming-Checker/Documentation/issues/11) | Plan, customer feedback, and backlog synchronized | In progress |

**Exit criterion:** all evidence is attached by 19 July; incomplete work is explicitly moved or marked `at-risk`.

### Sprint 7 — 20–26 July

**Objective:** validate improvements and prepare final delivery materials.  
**Planned effort:** 94 h. **Status:** Forecast.

| Area | Planned issues | Expected result |
|------|----------------|-----------------|
| Performance and scraping | [Backend #78](https://github.com/Naming-Checker/Backend/issues/78), [Backend #82](https://github.com/Naming-Checker/Backend/issues/82) | Comparative load-test report and improved scraping quality |
| Text model | [#19](https://github.com/Naming-Checker/TextModel/issues/19) | Optimized model with final evaluation |
| Visual model | [#26](https://github.com/Naming-Checker/VisualModel/issues/26) | Balanced combined-model weights with measured quality |
| Project reporting | [#12](https://github.com/Naming-Checker/Documentation/issues/12) | Final presentation, report, and linked evidence |

**Exit criterion:** all 5 issues satisfy their Definition of Done by 26 July, or an approved deviation is recorded.

## 6. Dependencies and Critical Path

1. Sprint 5 load-test goals, infrastructure, and scenarios unblock the Sprint 6 baseline.
2. The baseline unblocks bottleneck analysis and Sprint 7 repeated testing.
3. Text noise analysis unblocks final text-model optimization.
4. Visual fine-tuning and channel integration unblock final weight balancing.
5. Sprint 6 technical evidence unblocks accurate final reporting.

Work on the critical path is not replaced by unplanned scope unless the PM records the trade-off and confirms that the 26 July exit criteria remain achievable.

## 7. Tracking and Deviation Rules

- The Tasks board is the source of truth for issue status, Sprint, Assignee, `Ideal Hours`, and `Effort`.
- This document is the source of truth for milestone intent, dates, expected results, and exit criteria.
- An issue is part of the baseline only when it appears in both its board sprint and the corresponding table above.
- Scope added after sprint start must identify the affected milestone and capacity trade-off.
- `Done` requires the issue Definition of Done, linked evidence, and actual `Effort`.
- A delayed issue is marked `at-risk` or `blocked`; the weekly digest records cause, impact, owner, and recovery action.
- Moving work between sprints requires team agreement and updates to this plan and the board in the same review cycle.
- Milestone status is based on exit criteria, not only on the number of closed issues.

## 8. Reporting

The weekly status note must contain:

1. milestone and sprint;
2. planned versus completed issues and hours;
3. delivered results with links;
4. blockers, risks, and deviations;
5. recovery action and owner;
6. forecast for the next sprint and the 26 July deadline.

The final report must trace each strategic result to its GitHub issue, technical artifact, metric, test report, or demonstration evidence.
