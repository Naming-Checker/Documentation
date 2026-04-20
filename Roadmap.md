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

**Focus: three text similarity modules + visual model integration with search**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **M3**: Phonetic / semantic similarity | Daniel | Similarity module |
| Weeks 1-2 | **M9**: Visual model integration - API for comparing two logos | Alex + Ilya | Working logo infringement endpoint |
| Weeks 3-4 | **M6**: Final aggregation formula (phonetic + semantic + text) | Daniel | Unified text similarity metric |
| Weeks 3-4 | **M7**: PostgreSQL search - MKTU filtering, top-200 output | Ilya | End-to-end DB search is operational |

**Milestone (end of June):** text naming pipeline works end-to-end (input -> top-200 with similarity score), and visual model is integrated into API.

### July 2026

**Focus: module consolidation, quality testing, and non-functional targets**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **M8**: Text infringement check - compare with one target naming | Vladimir | Working text infringement endpoint |
| Weeks 1-2 | **M12**: Dockerization and deployment setup for A100 | Vladimir (lead) + Ilya | Docker image and CI/CD pipeline |
| Weeks 1-2 | Quality testing of all modules on real data | Ilya, Vladimir (lead, backend), Daniel (text models), Alex (visual), Daria (product review) | Accuracy report and improvement plan |
| Weeks 3-4 | Model refinement based on test results | Daniel (text), Alex (visual) | Target accuracy across modules |
| Weeks 3-4 | **M11**: Web interface - minimal UI for result delivery | Vladimir | Working UI for text and logos |
| Weeks 3-4 | Response-time optimization (< 2 min) | Ilya | Latency measurements and optimizations |

**Milestone (end of July):** MVP is ready - all Must Have tasks are implemented, target accuracy is reached, response time is below 2 minutes, Docker image is built, and UI is operational.

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
| End of June | Text naming demo | End-to-end flow: input -> top-200 matches |
| End of July | **MVP** | All Must Have items (M1-M12) completed, target accuracy, <2 min latency, Docker, UI |
| Mid-August | **Full Release** | Plus external sources (S1), word-mark graphics (S2), stabilization |
