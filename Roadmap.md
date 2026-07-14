# Strategic Plan and Roadmap

## 1. Strategic Goal

Build an internal MTS service for automated similarity checks of names and logos against registered trademarks. The service must run fully inside the internal network.

## 2. Key Directions

| Direction | Description | Priority |
|-----------|-------------|----------|
| Logo visual similarity | Image-to-image ML model for logo comparison | Highest |
| Text naming similarity | Phonetics + semantics + text metrics for word marks | High |
| Data preprocessing | Normalization of naming records from the database | High (blocks text pipeline) |
| External source parsing | RAO / Ministry of Culture / Roskomnadzor registries, search and media sources | Low |
| Web interface | Minimal UI for presenting results | High (Must Have) |

## 3. Key Risks

Probability is assessed on a three-level scale (Low / Medium / High) based on current team experience and available information. Each risk has an explicit owner who is responsible for monitoring the risk, triggering the mitigation plan, and escalating to the PM if the situation changes.

| Risk | Probability | Impact | Owner | Mitigation |
|------|-------------|--------|-------|------------|
| Quality metrics are not formalized, no strict accuracy definition | High | High | Daria (PM) | Run M10 as highest priority |
| Low visual model accuracy | Medium | High | Alex | Early testing on real data; try existing solutions. If all fails, document and postpone |
| Low text similarity quality (phonetics / semantics) | Medium | High | Daniel | Benchmark several algorithms, tune early on real data |
| Unpredictable external data formats | High | Medium | Vladimir, Ilya | Iterative parser; isolate behind adapters |
| Backend architecture / integration issues (DB, API, services) | Medium | High | Ilya | Early architecture review, integration tests with the DB |
| Delay of dev environment with GPUs and DB | High | High | Daria (PM) | Escalate early |

## 4. Roadmap

The detailed execution baseline for 1 June–26 July is maintained in the [June–July 2026 Strategic Plan](Strategic/Strategic_Plan_June-July_2026.md). GitHub issues, current statuses, estimates, and actual effort are tracked on the [Tasks board](https://github.com/orgs/Naming-Checker/projects/3).

### May 2026

**Focus: visual model + data preprocessing + test dataset and metrics**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **M10**: Formalize quality metrics - define with experts what is considered "similar", which metrics are used (accuracy/precision/recall/F1), and target thresholds | Daria | Metrics and thresholds specification document |
| Weeks 1-2 | **M10**: Build labeled test dataset - logo and naming pairs with expert labels (similar / not similar / borderline) | Daniel (text), Alex (logos) | Test dataset v1 (minimum for visual model validation) |
| Weeks 1-2 | **M1**: Improve visual model - select final architecture and benchmark on test dataset | Alex | Baseline with metrics on new dataset |
| Weeks 1-2 | **M2**: Analyze DB data and implement naming preprocessing parser | Ilya | Parser v1 + data quality statistics |
| Weeks 3-4 | **M1**: Fine-tune visual model and validate on DB data | Alex | Model with accuracy >= 80% on test set |
| Weeks 3-4 | **M2**: Improve parser - remove numbers, abbreviations, and non-protectable elements (`mark_disclaimer`) | Ilya | Parser v2 with primary edge case coverage |

**Milestone:** test dataset is ready and labeled, metrics are formalized, visual model reaches target test accuracy, and preprocessing is stable.

### June 2026

**Focus: technical foundation, observability, model development, and integrated product demo**

| Period | Sprint / milestone | Main tasks | Result |
|--------|--------------------|------------|--------|
| 1–13 June | Sprint 1 / MS1 | ELK, application logging, APM, Yandex Video/Music scrapers, text research and datasets, visual evaluation dataset | Observable services, initial source coverage, and reproducible model inputs |
| 14–20 June | Sprint 2 / MS1 | Indices and retention, Grafana, scraper webhook, text extraction and preprocessing, visual evaluation and fine-tuning | Operational monitoring, integrated scraper execution, and model baseline |
| 21–28 June | Sprint 3 / MS2 | Unified service metrics, dashboards as code, frontend integration, LaBSE, visual fine-tuning, MoSP demo | Integrated and demonstrable product increment |
| 29–30 June | Sprint 4 / MS3 begins | Alerting, source expansion, and visual quality experiments | Quality and performance-readiness work started |

**Milestone (28 June):** MS1 and MS2 are complete: the test stand is observable, scraper and frontend flows are integrated, model increments are measurable, and the product increment has been demonstrated.

### July 2026

**Focus: quality, performance validation, model optimization, and release readiness**

| Period | Sprint / milestone | Main tasks | Result |
|--------|--------------------|------------|--------|
| 1–5 July | Sprint 4 / MS3 | Alerting, YouTube scraper, font and color research, dataset expansion, stakeholder feedback | Broader source coverage and measurable visual-quality inputs |
| 6–12 July | Sprint 5 / MS3 | Load-test goals, infrastructure and scenarios, resilient Yandex scraping, ranking and color-comparison improvements | Reproducible load-test setup and quality improvements |
| 13–19 July | Sprint 6 / MS4 | Baseline load test, bottleneck analysis, Google Books, text-noise analysis, visual fine-tuning and channel integration | Performance baseline and prioritized optimization work |
| 20–26 July | Sprint 7 / MS4 | Repeated load test, scraping quality, text optimization, visual weight balancing, final reporting | Comparative metrics and release-ready project materials |

**Milestone (26 July):** MS3 and MS4 are complete: model and scraper quality improvements are measured, baseline and repeated load-test reports are available, bottlenecks are addressed or documented, and final delivery materials trace results to evidence.

### August 2026

**Focus: external sources, documentation, and stabilization**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **S1**: External source parsing (RAO, Ministry of Culture, Roskomnadzor, Kinopoisk, Yandex, etc.) | Vladimir + Ilya | External source parser v1 |
| Weeks 1-2 | **S2**: Graphic similarity for word marks (font, case, color) | Alex + Ilya | Word-mark graphic similarity module v1 |
| Weeks 1-2 | Load testing and bug fixing | Vladimir (lead), whole team for bug fixing | Stable build |
| Weeks 1-3 | Buffer for improvements, edge cases, final stabilization | Daria (review) | Release candidate |

**Milestone (mid-August):** full release with external sources, word-mark graphic similarity, and stabilized production version.

## 5. Role Allocation

The team consists of five people. Each person has a primary area of responsibility plus secondary duties. Documentation and quality/testing are explicit roles assigned to specific team members so that these activities are not forgotten.

| Person | Primary role | Areas of responsibility | Allocation |
|--------|--------------|-------------------------|------------|
| Daria | Project Manager | Project management and planning; overall documentation ownership (structure, completeness, review); evaluation of product state and progress against the roadmap; risk monitoring; communication with legal experts and stakeholders | Continuous from May to August |
| Daniel | ML/NLP Engineer + Documentation | Phonetic and text similarity (M3, M5, M6); model evaluation and metric definition (M10, test datasets); reviewing documentation | Full load in May (metrics and datasets) and June (text pipeline), refinement in July |
| Alex | ML Engineer (Visual) | Logo visual similarity model (M1), visual infringement API (M9), word-mark graphic similarity (S2) | Full load in May, then support, optimization and S2 in August |
| Ilya | Backend Engineer + Architecture | Backend architecture and integration decisions; data preprocessing (M2); PostgreSQL search (M7); API design; architecture of the documentation (structure of repos, ADRs, how docs are organized) | Continuous from May to August |
| Vladimir | Backend Engineer + Quality | Backend implementation (M8, M11, S1); quality assurance: test planning, writing and running integration/load tests, bug triage; Dockerization and CI/CD (M12) | Continuous from May to August |

### Cross-cutting responsibilities

| Responsibility | Lead | Support |
|----------------|------|---------|
| Documentation (content) | Daria | Daniel (review, structure), all team members (their own modules) |
| Documentation (architecture, repo layout) | Ilya | Daria |
| Product state evaluation | Daria | Daniel (model metrics), Vladimir (quality reports) |
| Testing of models (accuracy, metrics) | Alex, Daniel | Alex (visual), Daniel (text), Daria (expert validation) |
| Testing of backend and end-to-end (integration, load, UI) | Ilya | Vladimir |
| Risk monitoring | Daria (PM) | Each risk owner |

## 6. Checkpoints

| Date | Event | Success Criteria |
|------|-------|------------------|
| End of May | Test dataset ready + visual model demo | Labeled dataset (logos + text); visual model accuracy >= 80% |
| 20 June | **MS1 — Foundation and observability** | Observable services, model datasets and preprocessing, integrated scraper execution |
| 28 June | **MS2 — Integrated product demo** | Frontend and services integrated, unified monitoring available, model increment demonstrated |
| 12 July | **MS3 — Quality and performance readiness** | Alerting and quality extensions delivered; documented load-test environment and scenarios runnable |
| 26 July | **MS4 — Optimization and release readiness** | Baseline and repeated measurements, final model and scraping improvements, report and presentation ready |
| Mid-August | **Full Release** | Plus external sources (S1), word-mark graphics (S2), stabilization |
