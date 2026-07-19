# Strategic Plan — Full Cycle (14 February – 26 July 2026)

**Planning horizon:** 14 February – 26 July 2026  
**Status date:** 15 July 2026  
**Execution board:** [GitHub Project — Tasks](https://github.com/orgs/Naming-Checker/projects/3)  
**Product scope:** [MoSCoW](../MoSCoW.md)  
**High-level roadmap:** [Roadmap](../Roadmap.md)  
**Tracking rules:** [Project Tracking](../project_tracking.md)

---

## 1. Why This Plan Was Created

The project started on **14 February 2026** as a research initiative. Over 5.5 months, we evolved from isolated model experiments into a fully integrated, observable, and performance-tested product.

This document records the **complete strategic trajectory** — from the first baseline models to the release-ready increment planned for 26 July. It shows how each phase builds on the previous one, with clear milestones, model evolution, and integration checkpoints.

---

## 2. What We Need to Have by 26 July

- The backend, frontend, text model, visual model, monitoring, and scrapers work together on the test stand.
- Model changes are checked on repeatable datasets; reports include measured results rather than only implementation status.
- The team completes the load-test sequence: goals, environment, scenarios, baseline, bottleneck analysis, changes, and a repeated run.
- Final materials describe what was delivered, what did not fit, and which measurements support the conclusions.
- Issues planned for the period have a final status. Completed issues also have actual `Effort` on the board.

---

## 3. Full Milestone Overview

| Phase | Milestone | Period | Key Theme | Planned Effort |
| :--- | :--- | :--- | :--- | :--- |
| **Discovery** | **MS0 — Project Kick‑off & Research Baseline** | 14 Feb – 2 Mar | Project setup, baseline models, requirements | 80 h |
| **Model Development** | **MS1 — Core Model Implementation** | 3 Mar – 13 Apr | Text & visual models built and validated offline | 240 h |
| **Integration** | **MS2 — First Integrated Prototype** | 14 Apr – 31 May | Backend, API, parsers, and integrated demo | 260 h |
| **Hardening** | **MS3 — Observability & Stakeholder Demo** | 1–28 Jun | Monitoring, logging, second integration, demo | 197 h |
| **Optimisation** | **MS4 — Quality & Performance Readiness** | 29 Jun – 12 Jul | Quality extensions, resilient scraping, load-test readiness | 182 h |
| **Release** | **MS5 — Optimisation & Release Readiness** | 13–26 Jul | Baseline, optimisations, final reporting | 192 h |
| **Total** | | **14 Feb – 26 Jul** | | **1,151 h** |

---

## 4. Detailed Milestone Breakdown

---

### MS0 — Project Kick‑off & Research Baseline (14 Feb – 2 Mar)

**Objective:** Establish the project foundation, validate the core idea, and produce the first working prototypes of text and visual similarity.

**Key Deliverables:**
- Project repository structure and documentation templates.
- Initial requirements and success criteria (what “good” similarity means).
- **Baseline Text Model (v0.1):**
  - Phonetic similarity (Metaphone + Levenshtein).
  - Simple lexical matching (exact and partial matches).
  - Evaluation on a small hand-labelled dataset (~30 pairs).
- **Baseline Visual Model (v0.1):**
  - Embedding extraction using a pre-trained CNN (VGG16).
  - Cosine similarity between logo embeddings.
  - Evaluation on a small logo dataset (~20 pairs).
- Initial architecture sketch and technology selection (FastAPI, PostgreSQL, Docker).
- Definition of external data sources to be parsed later (Yandex, Google Play, App Store, etc.).

**Model Status:**
- Text: Raw prototypes, no preprocessing, low accuracy (~60%).
- Visual: Raw embeddings, no fine-tuning, low accuracy (~55%).
- Integration: None – separate Jupyter notebooks.

**Exit Criteria:**
- Both baseline models produce measurable similarity scores.
- The team agrees on the acceptance criteria for “valid similarity”.
- A clear plan exists for the next phase (preprocessing, feature engineering, and integration).

---

### MS1 — Core Model Implementation (3 Mar – 13 Apr)

**Objective:** Build production‑ready versions of both similarity models with proper preprocessing, evaluation, and offline validation.

**Key Deliverables:**

#### Text Model (Daniel)
- **Preprocessing pipeline:** normalisation, digit/abbreviation removal, disclaimer handling, tokenisation.
- **Phonetic similarity:** Russian Metaphone + Levenshtein distance (unit‑tested).
- **Semantic similarity:** RoSBERTa embeddings + cosine similarity (unit‑tested).
- **Lexical/text similarity:** inclusion score, Damerau‑Levenshtein, Jaro‑Winkler (unit‑tested).
- **Weighted formula:** `W1*SemanticSim + W2*PhoneticSim + W3*TextSim`.
- **Calibration:** weights tuned on a labelled dataset (≥50 pairs) to reach **accuracy ≥ 85%**.
- **Evaluation script:** automated regression against the validation set.

#### Visual Model (Alexander)
- **Fine‑tuning stage 1:** VGG16 fine‑tuned on the internal logo dataset.
- **Evaluation:** accuracy measured on a held‑out test set; baseline established.
- **Feature extraction pipeline:** embed logos and store pre‑computed vectors.

#### Backend Preparation (Ilya)
- FastAPI project skeleton.
- Dockerfile and basic CI/CD pipeline (GitHub Actions).
- PostgreSQL schema for storing embeddings and raw data.
- Pre‑processing service that calls Daniel’s pipeline.

#### Parser Research (Vladimir)
- Investigate 11 external sources (Yandex, Google Play, App Store, RAO, MinCulture, etc.).
- Design a common parser interface.
- Build **unit tests** for each parser (mock responses).

**Model Status:**
- Text: v1.0 – calibrated, accuracy ≥ 85%, packaged as a Python module.
- Visual: v1.0 – fine‑tuned, accuracy measured, embedding pipeline ready.
- Integration: Components are separate but can be called from the backend.

**Exit Criteria:**
- Text model passes offline evaluation with ≥ 85% accuracy.
- Visual model passes offline evaluation with documented accuracy.
- Backend can load both models and serve similarity scores via a test endpoint.
- Parser interfaces are defined and unit‑tested.

---

### MS2 — First Integrated Prototype (14 Apr – 31 May)

**Objective:** Integrate all components into a working system with an API, parsers, and a minimal frontend.

**Key Deliverables:**

#### Backend & API (Ilya)
- Implement `/check‑registration` endpoint (text + logo flow).
- Implement `/check‑infringement` endpoints (text‑only, logo‑only).
- Integrate Daniel’s text pipeline and Alexander’s visual pipeline.
- Implement pre‑computed embedding storage (PostgreSQL/ClickHouse).
- Integration tests for all endpoints with a test database.
- Latency measurement: DB query + scoring must be < 2 minutes.

#### Parsers (Vladimir)
- Build parsers for all 11 external sources.
- Aggregator service that returns top‑200 relevant names from a given query.
- Ensure offline data freshness (update mechanism without runtime internet access).
- Integration tests to verify parser robustness and response time.

#### Frontend (Minimal)
- A simple UI (React or Flask) that allows users to:
  - Enter a name and see similarity results.
  - Upload a logo and see visual matches.
- Connect to the backend API.

#### Integration (Whole Team)
- Docker‑compose the entire system (backend + frontend + models + parsers + DB).
- End‑to‑end tests for all three use cases (registration check, text infringement, logo infringement).
- Regression testing on the full labelled dataset after integration.

**Model Status:**
- Text: v1.1 – minor tweaks based on integration feedback.
- Visual: v1.1 – embedding pipeline optimised for production.
- Integration: Full E2E flow works, albeit without monitoring or performance optimisation.

**Exit Criteria:**
- Full E2E suite passes.
- Accuracy ≥ 85% on labelled dataset (unchanged from MS1).
- Latency sustained < 2 minutes (measured informally).
- No critical bugs in core flows.
- The system can be demonstrated manually.

---

### MS3 — Observability & Stakeholder Demo (1–28 Jun)


**Objective:** Make the system observable, prepare for real‑world use, and deliver a stakeholder demo.

**Key Deliverables:**

#### Observability (Ilya)
- Deploy ELK logging, application logs, APM traces, indices, and retention.
- Deploy Prometheus and Grafana.
- Expose unified metrics (request rates, error rates, latency percentiles, model inference times).
- Provision Grafana dashboards as code.

#### Model Improvements
- **Text:** Add LaBSE semantic encoder (better multilingual support). Package the model as an installable module.
- **Visual:** Complete fine‑tuning stage 2 on an extended dataset.
- **Ranking:** Begin work on garbage identification and ranking improvements (carried over to MS4).

#### Scrapers
- Implement initial Yandex scrapers and webhook integration.
- Ensure scrapers can run in production mode.

#### Demo Preparation (Daria + Team)
- Groom the backlog and prepare the MoSP presentation.
- Rehearse the integrated demo (frontend flow, service metrics, dashboards, and model updates).

**Model Status:**
- Text: v1.2 – LaBSE added, calibration re‑run.
- Visual: v1.2 – second fine‑tuning stage completed.
- Integration: Full stack deployed on the test stand with monitoring.

**Exit Criteria:**
- Services are observable on the test stand (logs, traces, metrics, dashboards).
- Scraper execution works through the backend.
- The MoSP presentation is delivered and well received.
- All planned issues (Sprints 1–3) are closed.

---

### MS4 — Quality & Performance Readiness (29 Jun – 12 Jul)


**Objective:** Shift focus from basic integration to quality, while preparing for load testing.

**Key Deliverables:**

#### Alerting & Hardening
- Configure service and infrastructure alerting (Prometheus Alertmanager).
- Improve Yandex scraper resilience (proxy rotation, user‑agent strategies, retries).
- Add YouTube scraping.

#### Model Quality (Text – Daniel)
- **Garbage identification (#17):** analyse false positives, categorise noise, propose filtering rules.
- **Ranking optimisation (#18):** recalibrate weights to prioritise semantic matches.
- Target: Precision@10 improvement ≥ 5% on the validation set.

#### Model Quality (Visual – Alexander)
- **Color analysis (#22):** implement color histogram comparison as an additional feature.
- **Font analysis:** analyse font datasets for logo similarity.
- Extend the logo dataset with more examples.
- Target: combined visual score (VGG16 + color + font) improves accuracy ≥ 3%.

#### Load Testing Preparation (Ilya + Daria)
- Define load‑testing goals, key metrics (#73): RPS, latency percentiles, error rates, resource utilisation.
- Prepare infrastructure (#74): test environment, monitoring stacks, data seeding.
- Implement executable load‑test scenarios (#75).

**Model Status:**
- Text: v1.3 – garbage filtering added, ranking optimised, precision improved.
- Visual: v1.3 – color and font analysis integrated, accuracy improved.
- Integration: Quality gates applied; ready for load testing.

**Exit Criteria:**
- All 13 issues (Sprints 4–5) are closed.
- The team can launch the documented load‑test scenarios against the prepared environment.
- The Yandex scraper runs stably with < 5% failure rate.

---

### MS5 — Optimisation & Release Readiness (13–26 Jul)


**Objective:** Measure baseline performance, optimise models and scraping, and prepare final reporting.

**Key Deliverables:**

#### Performance Validation (Ilya)
- Run baseline load tests (#76) and record metrics.
- Identify bottlenecks (#77).
- Make targeted improvements (caching, query optimisation, model batching).
- Run repeated load tests (#78) and compare results.

#### Model Final Optimisation
- **Text (#19):** apply final filtering rules, adjust weights, run regression. Target: Precision@10 ≥ 0.85, NDCG@10 ≥ 0.80.
- **Visual (#26):** combine VGG16 + color + font with balanced weights. Target: visual similarity accuracy ≥ 0.90.
- **Garbage sources (#17, completed in Sprint 6):** final analysis and mitigation.

#### Scraping Improvements
- Implement Google Books scraping (#83).
- Improve overall scraping quality (#82) – retry logic, error handling, data validation.

#### Final Reporting (Daria)
- Prepare final presentation and report (#12).
- Link each strategic result to its GitHub issue, technical artifact, metric, test report, or demonstration evidence.
- Document what was delivered, what did not fit, and why.

**Model Status:**
- Text: v2.0 – final optimised model with documented metrics.
- Visual: v2.0 – final combined model with documented metrics.
- Integration: Production‑ready, measured, and documented.

**Exit Criteria:**
- All 5 Sprint 7 issues satisfy their Definition of Done by 26 July, or an approved deviation is recorded.
- Load test results meet defined thresholds (P95 latency < 2 min, success rate > 95%).
- Final report is complete and archived in the repository.

---

## 5. How the Model Evolved (Summary)

| Phase | Period | Text Model | Visual Model | Integration Status |
| :--- | :--- | :--- | :--- | :--- |
| **MS0** | 14 Feb – 2 Mar | Baseline: phonetic + lexical (accuracy ~60%) | Baseline: VGG16 embeddings (accuracy ~55%) | Separate notebooks |
| **MS1** | 3 Mar – 13 Apr | Preprocessing + 3 similarity types + calibrated formula (accuracy ≥ 85%) | Fine‑tuning stage 1 + embedding pipeline (accuracy measured) | Components built, separate modules |
| **MS2** | 14 Apr – 31 May | v1.1 – minor tweaks, packaged module | v1.1 – embedding pipeline optimised | Full E2E integration (Docker, API, frontend) |
| **MS3** | 1–28 Jun | v1.2 – LaBSE added, re‑calibrated | v1.2 – fine‑tuning stage 2 completed | Integrated, observable, demoed |
| **MS4** | 29 Jun – 12 Jul | v1.3 – garbage filtering + ranking (+5% precision) | v1.3 – color + font analysis (+3% accuracy) | Quality gates applied, load‑test ready |
| **MS5** | 13–26 Jul | v2.0 – final optimisation (Precision@10 ≥ 0.85) | v2.0 – combined model (accuracy ≥ 0.90) | Production‑ready, measured, documented |

---

## 6. Dependencies and Critical Path

1. **MS0 (Feb)** – Baseline models and requirements unblock MS1.
2. **MS1 (Mar–Apr)** – Core models unblock MS2 (integration).
3. **MS2 (Apr–May)** – Integration unblocks MS3 (observability and demo).
4. **MS3 (Jun)** – Observability and demo unblock MS4 (quality and load testing).
5. **MS4 (Jul 1–12)** – Load‑test readiness and quality improvements unblock MS5 (optimisation and release).
6. **MS5 (Jul 13–26)** – Baseline measurement and optimisation unblock final release.

Work on the critical path is not replaced by unplanned scope unless the PM records the trade‑off and confirms that the 26 July exit criteria remain achievable.

---

## 7. Tracking and Deviation Rules

- The Tasks board is the source of truth for issue status, Sprint, Assignee, `Ideal Hours`, and `Effort`.
- This document is the source of truth for milestone intent, dates, expected results, and exit criteria.
- An issue is part of the baseline only when it appears in both its board sprint and the corresponding table above.
- Scope added after sprint start must identify the affected milestone and capacity trade‑off.
- `Done` requires the issue Definition of Done, linked evidence, and actual `Effort`.
- A delayed issue is marked `at‑risk` or `blocked`; the weekly digest records cause, impact, owner, and recovery action.
- Moving work between sprints requires team agreement and updates to this plan and the board in the same review cycle.
- Milestone status is based on exit criteria, not only on the number of closed issues.

---

## 8. Reporting

The weekly status note must contain:

1. milestone and sprint;
2. planned versus completed issues and hours;
3. delivered results with links;
4. blockers, risks, and deviations;
5. recovery action and owner;
6. forecast for the next sprint and the 26 July deadline.

The final report (due by 26 July) must trace each strategic result to its GitHub issue, technical artifact, metric, test report, or demonstration evidence.

---

## 9. Summary of What Was Built (End‑to‑End)

| Layer | Components |
| :--- | :--- |
| **ML Models** | Text similarity (phonetic + semantic + lexical, calibrated, with garbage filtering). Visual similarity (VGG16 + color + font, fine‑tuned, combined). |
| **Backend** | FastAPI, PostgreSQL/ClickHouse, Docker, CI/CD (GitHub Actions). |
| **Parsers** | 11 external sources (Yandex, Google Play, App Store, RAO, MinCulture, YouTube, Google Books, etc.), with resilience and health checks. |
| **Frontend** | Minimal UI for registration and infringement checks. |
| **Observability** | ELK + Prometheus + Grafana, application logs, APM traces, alerting. |
| **Performance** | Load‑test scenarios, baseline and optimised metrics, bottleneck analysis. |
| **Documentation** | Requirements, architecture, tactical plan, strategic plan, user manual, similarity formula, final report. |

---
