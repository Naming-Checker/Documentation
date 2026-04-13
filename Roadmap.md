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

## 3. Assumptions and Risks

### Assumptions
- NVIDIA A100 80GB GPU is available for experiments and deployment.
- Access to the PostgreSQL trademark database is available.
- Initial visual model experiments are already completed and a baseline exists.

### Key Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Quality metrics are not formalized, no strict accuracy definition | High | Run M10 in first two weeks of May: align with legal experts on similarity criteria, labeled dataset, and target metrics |
| Low visual model accuracy | High | Early testing on real data and iterative architecture tuning |
| Unpredictable external data formats | Medium | Iterative parser improvement |

## 4. Roadmap

### May 2026

**Focus: visual model + data preprocessing + test dataset and metrics**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **M10**: Formalize quality metrics - define with experts what is considered "similar", which metrics are used (accuracy/precision/recall/F1), and target thresholds | ML + Legal | Metrics and thresholds specification document |
| Weeks 1-2 | **M10**: Build labeled test dataset - logo and naming pairs with expert labels (similar / not similar / borderline) | ML | Test dataset v1 (minimum for visual model validation) |
| Weeks 1-2 | **M1**: Improve visual model - select final architecture and benchmark on test dataset | ML | Baseline with metrics on new dataset |
| Weeks 1-2 | **M2**: Analyze DB data and implement naming preprocessing parser | Backend | Parser v1 + data quality statistics |
| Weeks 3-4 | **M10**: Extend test dataset - add text naming pairs for phonetic/semantic validation | ML | Test dataset v2 (text + images) |
| Weeks 3-4 | **M1**: Fine-tune visual model and validate on DB data | ML | Model with accuracy >= 80% on test set |
| Weeks 3-4 | **M2**: Improve parser - remove numbers, abbreviations, and non-protectable elements (`mark_disclaimer`) | Backend | Parser v2 with primary edge case coverage |

**Milestone:** test dataset is ready and labeled, metrics are formalized, visual model reaches target test accuracy, and preprocessing is stable.

### June 2026

**Focus: three text similarity modules + visual model integration with search**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **M3**: Phonetic similarity - algorithm, transliteration, spelling distortion handling | ML/NLP | Phonetic similarity module v1 |
| Weeks 1-2 | **M4**: Semantic similarity - model and multilingual support | ML/NLP | Semantic similarity module v1 |
| Weeks 1-2 | **M9**: Visual model integration - API for comparing two logos | ML + Backend | Working logo infringement endpoint |
| Weeks 3-4 | **M5**: Text metrics (string similarity, prefix containment) | Backend | Text metrics module v1 |
| Weeks 3-4 | **M6**: Final aggregation formula (phonetic + semantic + text) | ML/NLP | Unified text similarity metric v1 |
| Weeks 3-4 | **M7**: PostgreSQL search - MKTU filtering, top-200 output | Backend | End-to-end DB search is operational |

**Milestone (end of June):** text naming pipeline works end-to-end (input -> top-200 with similarity score), and visual model is integrated into API.

### July 2026

**Focus: module consolidation, quality testing, and non-functional targets**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **M8**: Text infringement check - compare with one target naming | Backend | Working text infringement endpoint |
| Weeks 1-2 | **M12**: Dockerization and deployment setup for A100 | DevOps/Backend | Docker image and CI/CD pipeline |
| Weeks 1-2 | Quality testing of all modules on real data | Whole team | Accuracy report and improvement plan |
| Weeks 3-4 | Model refinement based on test results | ML | Target accuracy across modules |
| Weeks 3-4 | **M11**: Web interface - minimal UI for result delivery | Backend | Working UI for text and logos |
| Weeks 3-4 | Response-time optimization (< 2 min) | Backend + ML | Latency measurements and optimizations |

**Milestone (end of July):** MVP is ready - all Must Have tasks are implemented, target accuracy is reached, response time is below 2 minutes, Docker image is built, and UI is operational.

### August 2026

**Focus: external sources, documentation, and stabilization**

| Week | Tasks | Owners | Result |
|------|-------|--------|--------|
| Weeks 1-2 | **S1**: External source parsing (RAO, Ministry of Culture, Roskomnadzor, Kinopoisk, Yandex, etc.) | Backend | External source parser v1 |
| Weeks 1-2 | **S2**: Graphic similarity for word marks (font, case, color) | ML/Backend | Word-mark graphic similarity module v1 |
| Weeks 1-2 | Load testing and bug fixing | Whole team | Stable build |
| Weeks 1-3 | Buffer for improvements, edge cases, final stabilization | Whole team | Release candidate |

**Milestone (mid-August):** full release with external sources, word-mark graphic similarity, and stabilized production version.

## 5. Role Allocation

| Role | Focus | Allocation |
|------|-------|------------|
| ML Engineer #1 | Logo visual model (M1, M9), test dataset (M10) | Full load in May, then support and optimization |
| ML/NLP Engineer #2 | Phonetics, semantics, final formula (M3, M4, M6) | Full load in June, refinement in July |
| Backend Engineer #3 | Preprocessing, text metrics, DB search, API (M2, M5, M7, M8) | Continuous from May to August |
| Backend Engineer #4 | UI (M11), external parsers (S1), word-mark graphics (S2) | July to August |
| DevOps / Backend #5 | Docker, deployment, CI/CD, monitoring (M12) | July to August |

## 6. Checkpoints

| Date | Event | Success Criteria |
|------|-------|------------------|
| End of May | Test dataset ready + visual model demo | Labeled dataset (logos + text); visual model accuracy >= 80% |
| End of June | Text naming demo | End-to-end flow: input -> top-200 matches |
| End of July | **MVP** | All Must Have items (M1-M12) completed, target accuracy, <2 min latency, Docker, UI |
| Mid-August | **Full Release** | Plus external sources (S1), word-mark graphics (S2), stabilization |
