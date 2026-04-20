# Quality Plan

## Purpose
This plan defines how quality will be specified, checked, and controlled for NamingChecker during development and before release.

## Quality Goals
- Accuracy of core similarity results at target level agreed with stakeholders.
- Full query response time within project limits.
- Stable work inside the internal network with no runtime external calls.
- Reliable API and staged result delivery.
- Maintainable and testable implementation.

## Quality Scope
The plan covers:
- text naming preprocessing;
- phonetic, semantic, and text similarity modules;
- logo comparison;
- ranking and top-200 output;
- API and webhook delivery;
- deployment and monitoring.

## Approach
Quality is managed through:
- agreed quality attribute scenarios (QAS);
- measurable metrics;
- quality attribute scenario tests (QAST);
- automated checks in CI/CD where possible;
- regular review with stakeholders.

## Main Quality Attributes
- Correctness
- Performance
- Reliability
- Maintainability
- Operational safety

## Quality Activities
| Activity | Description | Owner | Frequency |
|---|---|---|---|
| Quality requirements review | Confirm metrics, thresholds, and acceptance criteria | PM + stakeholders | At baseline and on change |
| Test dataset maintenance | Keep labeled text and logo dataset актуальным | ML | Regularly |
| Module validation | Check preprocessing and similarity modules on agreed cases | ML / Backend | Each iteration |
| API and integration testing | Verify endpoints, contracts, and staged delivery | Backend | Each iteration |
| Performance testing | Measure latency and bottlenecks | Backend | Before milestones and release |
| Regression testing | Re-run fixed quality checks after changes | Whole team | Before merge/release |
| Release quality review | Final review of metrics and open risks | Whole team | Before release |

## Quality Control Points
- End of May: metrics and labeled dataset approved.
- End of June: end-to-end text and logo flows validated.
- End of July: MVP quality targets checked.
- Before release: full regression, performance, and deployment validation.

## Evidence
Quality status is confirmed by:
- test reports;
- metric results on labeled datasets;
- CI results;
- latency measurements;
- defect and issue logs;
- stakeholder review notes.

## Acceptance Basis
A release can be accepted only if:
- mandatory quality checks are completed;
- target metrics are reached or formally accepted with mitigation;
- critical defects are resolved or explicitly approved as residual risk.

## Change Management
If requirements, architecture, or metrics change, the quality plan must be updated together with the baseline requirements and related tests.
