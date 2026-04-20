# Quality Management

## Purpose

This document defines how quality is managed in **NamingChecker**.

For this project, quality means **fitness for purpose under constraints**. It must be defined with stakeholders, measured, and checked throughout the project.

## Principles

- Quality is based on stakeholder needs, not generic templates.
- Quality requirements must be measurable.
- Quality must be clarified early, not only at final acceptance.
- Architecture, planning, and risks must reflect quality goals.
- Quality must be validated continuously.

## Main Quality Attributes

For NamingChecker, the key quality attributes are:

- **Result quality** — relevance of returned names and logos.
- **Performance** — speed of full checks.
- **Reliability** — stable request processing and delivery.
- **Usability** — results are understandable and useful.
- **Maintainability** — safe updates of models, rules, and APIs.
- **Operational compliance** — full work inside internal infrastructure.

## Quality Objectives

- Accuracy target: **>= 85%** on the agreed evaluation method.
- Full response time: **< 2 minutes**.
- Stage 1 latency: **P95 = 60s**, **P99 = 100s**.
- Stage 2 delivery: **<= 120s**.
- Availability: **99.5%–99.9%**.
- No runtime external internet access.
- Deployment on **NVIDIA A100 PCIe 80GB**.

## Quality Attribute Scenarios

### QAS-1. Text result quality
A legal specialist submits a naming with MKTU classes. The system returns top-200 similar candidates with similarity scores. The measured relevance must meet the agreed threshold.

### QAS-2. Logo comparison quality
A user submits a logo for comparison. The system returns similar logos with visual similarity scores. The model must meet the agreed quality threshold on labeled data.

### QAS-3. Performance
A user runs a full check. The system completes preprocessing, search, scoring, and aggregation in under 2 minutes.

### QAS-4. Operational compliance
The service runs in the internal MTS network and processes requests without runtime calls to external internet resources.

### QAS-5. Change safety
After approved requirement or logic changes, the system passes CI, consistency checks, and regression tests before merge.

## QAS Tests

- **Text quality test** — run expert-labeled naming scenarios and measure precision/accuracy.
- **Logo quality test** — run labeled logo pairs and compare model versions.
- **Latency test** — run end-to-end requests and measure total response time.
- **Isolation test** — verify that all dependencies are preloaded and no runtime external calls occur.
- **Regression test** — rerun fixed validation suites after meaningful changes.

## Quality Metrics

| Area | Metric | Target |
|---|---|---:|
| Text quality | Accuracy / Precision | >= 85% |
| Logo quality | Accuracy / Precision / Recall / F1 | Agreed threshold |
| Full latency | End-to-end time | < 2 min |
| Stage 1 latency | P95 / P99 | 60s / 100s |
| Stage 2 delivery | SLA | <= 120s |
| Availability | Uptime | 99.5%–99.9% |
| External freshness | Time since source refresh | <= 1 month |

## Quality Management Activities

- define quality expectations early;
- convert them into measurable scenarios and tests;
- include quality tasks in planning;
- evaluate models on labeled datasets;
- run latency, regression, and deployment checks;
- update requirements and tests when quality expectations change.

## Acceptance Rule

The project must not rely only on final subjective acceptance.
A feature is quality-ready only if:

- its quality requirement is defined;
- the related test is executed;
- the result is compared with the target threshold.

## Summary

For NamingChecker, quality is stakeholder-driven, measurable, and continuously validated. It is managed through concrete metrics, repeated tests, and explicit alignment with architecture, planning, and risks.
