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

- The backend, frontend, text model, visual model, monitoring, and scrapers work together on the test stand. **[OWNER: Ilya, Vladimir, Daniel, Alexander]**
- Model changes are checked on repeatable datasets; reports include measured results rather than only implementation status. **[OWNER: Daniel, Alexander]**
- The team completes the load-test sequence: goals, environment, scenarios, baseline, bottleneck analysis, changes, and a repeated run. **[OWNER: Ilya, Daria]**
- Final materials describe what was delivered, what did not fit, and which measurements support the conclusions. **[OWNER: Daria]**
- Issues planned for the period have a final status. Completed issues also have actual `Effort` on the board. **[OWNER: All team members]**

---

## 3. Full Milestone Overview (Recalculated by Capacity)

| Phase | Milestone | Period | Days | Key Theme | Planned Effort |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Discovery** | **MS0 — Project Kick‑off & Research Baseline** | 14 Feb – 2 Mar | 17 | Project setup, baseline models, requirements | **146 h** |
| **Model Development** | **MS1 — Core Model Implementation** | 3 Mar – 13 Apr | 42 | Model prototypes and offline research | **360 h** |
| **Integration** | **MS2 — First Integrated Prototype** | 14 Apr – 31 May | 48 | Backend, API, parsers, and integrated demo | **411 h** |
| **Hardening** | **MS3 — Observability & Stakeholder Demo** | 1–28 Jun | 28 | Monitoring, logging, second integration, demo | **360 h** |
| **Optimisation** | **MS4 — Quality & Performance Readiness** | 29 Jun – 12 Jul | 14 | Quality extensions, resilient scraping, load‑test readiness | **180 h** |
| **Release** | **MS5 — Optimisation & Release Readiness** | 13–26 Jul | 14 | Baseline, optimisations, final reporting | **180 h** |
| **Total** | | **14 Feb – 26 Jul** | **163** | | **1,637 h** |

---

## 4. Detailed Milestone Breakdown

---

### MS0 — Project Kick‑off & Research Baseline (14 Feb – 2 Mar)

**Objective:** Establish the project foundation, validate the core idea, lay the research groundwork for text similarity, and produce the first visual-similarity prototype.

**Key Deliverables:**
- Project repository structure and documentation templates. **[OWNER: Daria]**
- Initial requirements and success criteria (what “good” similarity means). **[OWNER: Daria, Daniel, Alexander]**
- **Text Similarity Research (kick‑off):** **[OWNER: Daniel]**
  - Survey of candidate approaches started: phonetic algorithms and string metrics (Levenshtein and Jaro‑Winkler families).
  - Reference pair set collected from the Rospatent examination methodology (EUROPLEX/EUROFLEX, ТИГОТА/ДИКОТА, PROBI/ПРОБИМАКС, Arkline/Арклайн; counter‑example Лесное/Лесник) to serve as the qualitative validation set.
  - No committed prototype in this window — the first text‑model artifact landed on 13 Mar (MS1).
- **Baseline Visual Model (v0.1):** **[OWNER: Alexander]**
  - Embedding extraction using a pre-trained CNN (VGG16).
  - Similarity ranking between logo embeddings.
- Initial architecture sketch and technology selection (FastAPI, PostgreSQL, Docker). **[OWNER: Ilya, Daria]**
- Definition of external data sources to be parsed later (Yandex, Google Play, App Store, etc.). **[OWNER: Vladimir, Daria]**

**Model Status:**
- Text: Research only — no committed prototype, no measured accuracy.
- Visual: Raw embeddings, no fine-tuning, low accuracy (~55%).
- Integration: None – separate Jupyter notebooks.

**Exit Criteria:**
- The visual baseline produces measurable similarity scores. **[VERIFIED BY: Alexander]**
- The text-model reference pair set and candidate algorithm shortlist are agreed. **[VERIFIED BY: Daniel]**
- The team agrees on the acceptance criteria for “valid similarity”. **[VERIFIED BY: Daria + All team]**
- A clear plan exists for the next phase (preprocessing, feature engineering, and integration). **[OWNER: Daria]**

---

### MS1 — Core Model Implementation (3 Mar – 13 Apr)

**Objective:** Build and validate the first working similarity prototypes offline — text: phonetic and string metrics; visual: fine‑tuning and embedding pipeline.

**Key Deliverables:**

#### Text Model **[OWNER: Daniel]**
- **Phonetic similarity prototype** (committed 13 Mar, `phonetics_tests` notebook): transliteration of Cyrillic into a Latin phonetic form, Metaphone‑style phonetic‑group encoding (consonant classes, collapsed repeats), and a blended Jaro‑Winkler score over the raw and encoded strings (0.6/0.4).
- **Interactive Streamlit UI** for side‑by‑side pair testing (#1).
- **Transliteration experiments** for cross‑script pairs (#2).
- **String‑metric review and selection** — Levenshtein, Jaro‑Winkler, token‑sort via RapidFuzz (#3).
- **Review of existing phonetic algorithms** (#5) and **EDA of the RF trademark database** — structure, columns, МКТУ classes (#4).
- **Qualitative validation on the methodology pair set** (#6): e.g. EUROPLEX/EUROFLEX → 0.952, TIGOTA/DICOTA → 0.867; cross‑script pairs (Cellexin/СЕЛЕКСЕН) handled via transliteration.
- Deferred beyond MS1: semantic channel (first prototype 4 May, MS2), preprocessing pipeline (Jun), multi‑channel weighted formula (Jul), calibration and accuracy measurement (first benchmark: Jul).
- Tracking note: this work was logged retroactively as issues #1–#6 and closed on 26 Apr.

#### Visual Model **[OWNER: Alexander]**
- **Fine‑tuning stage 1:** VGG16 fine‑tuned using unsupervised contrastive learning method.
- **Feature extraction pipeline:** embed logos and store pre‑computed vectors.

#### Backend Preparation **[OWNER: Ilya]**
- FastAPI project skeleton.
- Dockerfile and basic CI/CD pipeline (GitHub Actions).
- PostgreSQL schema for storing embeddings and raw data.
- Pre‑processing service that calls Daniel’s pipeline.

#### Parser Research **[OWNER: Vladimir]**
- Investigate 11 external sources (Yandex, Google Play, App Store, RAO, MinCulture, etc.).
- Design a common parser interface.
- Build **unit tests** for each parser (mock responses).

**Model Status:**
- Text: research prototype (notebook + Streamlit demo) — phonetic and string channels validated qualitatively on the methodology pairs; no semantic channel, no packaged module, no measured accuracy yet.
- Visual: v1.0 – unsupervised fine‑tuning has failed, embedding pipeline ready.
- Integration: Components are separate but can be called from the backend.

**Exit Criteria:**
- Phonetic prototype validated qualitatively on the methodology pair set; string‑metric shortlist fixed. **[VERIFIED BY: Daniel]**
- Backend can load both models and serve similarity scores via a test endpoint. **[VERIFIED BY: Ilya]**
- Parser interfaces are defined and unit‑tested. **[VERIFIED BY: Vladimir]**

---

### MS2 — First Integrated Prototype (14 Apr – 31 May)

**Objective:** Integrate all components into a working system with an API, parsers, and a minimal frontend.

**Key Deliverables:**

#### Backend & API **[OWNER: Ilya]**
- Implement `/check‑registration` endpoint (text + logo flow).
- Implement `/check‑infringement` endpoints (text‑only, logo‑only).
- Integrate Daniel’s text pipeline and Alexander’s visual pipeline.
- Implement pre‑computed embedding storage (PostgreSQL/ClickHouse).
- Integration tests for all endpoints with a test database.
- Latency measurement: DB query + scoring must be < 2 minutes.

#### Text Model **[OWNER: Daniel]**
- **v0 semantic‑similarity prototype (4 May):** rubert‑tiny2 embeddings (312‑d, mean‑pooled, L2‑normalised) + cosine search over the trademark slice, with МКТУ‑class filtering; CLI and library interface; pre‑computed embedding store (`.pt`); structure mirrors `VisualModel/src`.
- Known limitations recorded: no preprocessing, phonetic/string channels not yet wired into one model, results not re‑ranked.

#### Parsers **[OWNER: Vladimir]**
- Build parsers for all 11 external sources.
- Aggregator service that returns top‑200 relevant names from a given query.
- Ensure offline data freshness (update mechanism without runtime internet access).
- Integration tests to verify parser robustness and response time.

#### Frontend (Minimal) **[OWNER: Ilya (with support from Daria for UI/UX)]**
- A simple UI that allows users to:
  - Enter a name and see similarity results.
  - Upload a logo and see visual matches.
- Connect to the backend API.

#### Integration **[OWNER: All team]**
- Docker‑compose the entire system (backend + frontend + models + parsers + DB).
- End‑to‑end tests for all three use cases (registration check, text infringement, logo infringement).
- Regression testing on the full labelled dataset after integration.

**Model Status:**
- Text: v0 – first semantic prototype (rubert‑tiny2 + cosine + МКТУ filter); phonetic/string research not yet merged into a single model.
- Visual: v1.1 – internal model for separating text from logos, embedding pipeline optimised for production.
- Integration: Full E2E flow works, albeit without monitoring or performance optimisation.

**Exit Criteria:**
- Full E2E suite passes. **[VERIFIED BY: Ilya]**
- Latency sustained < 2 minutes (measured informally). **[VERIFIED BY: Ilya]**
- No critical bugs in core flows. **[VERIFIED BY: All team]**
- The system can be demonstrated manually. **[OWNER: Daria]**

---

### MS3 — Observability & Stakeholder Demo (1–28 Jun)

**Objective:** Make the system observable, prepare for real‑world use, and deliver a stakeholder demo.

**Key Deliverables:**

#### Observability **[OWNER: Ilya]**
- Deploy ELK logging, application logs, APM traces, indices, and retention.
- Deploy Prometheus and Grafana.
- Expose unified metrics (request rates, error rates, latency percentiles, model inference times).
- Provision Grafana dashboards as code.

#### Model Improvements
- **Text:** semantic‑encoder bake‑off on translation / same‑root / random pair sets — LaBSE vs multilingual‑e5‑base vs paraphrase‑multilingual‑MiniLM‑L12 vs rubert‑tiny2; **LaBSE selected** (AUC translation‑vs‑random = 1.00, translation‑vs‑same‑root = 0.936), documented in `docs/models.md` with the comparative‑review notebook (#7, #9, #10 — closed 10–11 Jun). Trademark‑dump extraction (streaming SQL‑dump reader, no PostgreSQL required) and preprocessing modules (#11, #12 — closed 18 Jun). Production LaBSE encoder (#15) and installable‑package setup (#13) started in Sprint 3 and completed on 2 Jul. **[OWNER: Daniel]**
- **Visual:** Labelled test evaluation dataset and model fine‑tuning. **[OWNER: Alexander]**

#### Scrapers **[OWNER: Vladimir]**
- Implement initial Yandex scrapers and webhook integration.
- Ensure scrapers can run in production mode.

#### Demo Preparation **[OWNER: Daria + Team]**
- Groom the backlog and prepare the MoSP presentation.
- Rehearse the integrated demo (frontend flow, service metrics, dashboards, and model updates).

**Model Status:**
- Text: encoder selection finalised (LaBSE) and data pipeline in place (dump → parquet → aliases, preprocessing); production model implementation in progress — no end‑to‑end calibrated model yet.
- Visual: v1.2 – collected a labelled dataset and fine tuned the model to achieve the target accuracy.
- Integration: Full stack deployed on the test stand with monitoring.

**Exit Criteria:**
- Services are observable on the test stand (logs, traces, metrics, dashboards). **[VERIFIED BY: Ilya]**
- Visual: accuracy ≥ 85% on the labelled dataset. **[VERIFIED BY: Alexander]**
- Text: encoder choice validated on the translation / same‑root / random pair sets; end‑to‑end accuracy measurement deferred to the full‑index benchmark (MS5). **[VERIFIED BY: Daniel]**
- Scraper execution works through the backend. **[VERIFIED BY: Vladimir]**
- The MoSP presentation is delivered and well received. **[VERIFIED BY: Daria]**
- All planned issues (Sprints 1–3) are closed; text items #13 and #15 of Sprint 3 spilled over and closed on 2 Jul. **[VERIFIED BY: Daria]**

---

### MS4 — Quality & Performance Readiness (29 Jun – 12 Jul)

**Objective:** Shift focus from basic integration to quality, while preparing for load testing.

**Key Deliverables:**

#### Alerting & Hardening
- Configure service and infrastructure alerting (Prometheus Alertmanager). **[OWNER: Ilya]**
- Improve Yandex scraper resilience (proxy rotation, user‑agent strategies, retries). **[OWNER: Vladimir]**
- Add YouTube scraping. **[OWNER: Vladimir]**

#### Model Quality (Text) **[OWNER: Daniel]**
- **Production model shipped (`namecheck` 0.1.0; #14, #16 closed 2 Jul, code landed 3 Jul):** preprocessing pipeline; phonetic channel via G2P → IPA → articulatory‑feature alignment (epitran `rus-Cyrl` for Cyrillic; g2p_en plus letter‑by‑letter reading for Latin; onset‑weighted substitution costs); LaBSE semantic channel; string channel (normalised Levenshtein, length‑damped Jaro‑Winkler, token‑sort — maximum of the three); dedicated containment channel (full scores only for prefixes, suffixes, and whole tokens).
- **Final formula:** `score = α·max(channels) + (1−α)·Σ Wᵢ·channelᵢ`, with α = 0.80 and weights string 0.35 / phonetic 0.30 / containment 0.25 / semantic 0.10; dual‑form queries (original + transliterated, per‑channel maximum).
- **Two‑stage search** (per‑channel top‑k candidate pool → exact re‑scoring, top‑200) over the full base: 1,462,274 marks → 2,709,911 aliases; FastAPI service + indexing pipeline; Streamlit test app; full index built and swapped in on 10 Jul.
- **Ranking order (#18, Sprint 5 — closed 9 Jul, 16 h actual):** deterministic tie‑breaking (alias‑kind priority, then length closeness of display name and alias to the query); fixes exact‑match queries being buried under superstrings, with zero hit@200 risk (only equal scores reorder).
- **Garbage identification (#17, opened 3 Jul — in progress, Sprint 6):** main noise source identified — superstrings with containment = 1.0 enter at a ~80% score floor at α = 0.8; candidate filters (containment length discount, short‑alias penalty) deferred to the #19 grid search because they change scores and need a benchmark run to prove safe.
- Metrics note: ranking quality is tracked as hit@K and MRR (Precision@K is not used); weight/α recalibration deferred to #19 (MS5).

#### Model Quality (Visual) **[OWNER: Alexander]**
- **Color analysis (#22):** implement color histogram comparison as an additional feature.
- **Font analysis (`FontModel` repo, 5 Jul):** **[OWNER: Daniel]** font‑identification prototype implemented — synthetic training data rendered from Google Fonts (593 families used; only ~15% of Google Fonts cover Cyrillic), embedding‑based retrieval models trained (Latin‑only and mixed Latin+Cyrillic; frozen‑ResNet18 baseline ruled out; fixed‑list font classification rejected; AdobeVFR unusable for licensing reasons).
- Extend the evaluation dataset with more examples.
- Target: combined visual score (VGG16 + color) improves accuracy.

#### Load Testing Preparation **[OWNER: Ilya + Daria]**
- Define load‑testing goals, key metrics (#73): RPS, latency percentiles, error rates, resource utilisation.
- Prepare infrastructure (#74): test environment, monitoring stacks, data seeding.
- Implement executable load‑test scenarios (#75).

**Model Status:**
- Text: `namecheck` 0.1.0 — production 4‑channel model, packaged, API‑served, full 2.7 M‑alias index, deterministic tie‑breaking; garbage filtering not yet shipped (#17 in progress).
- Visual: v1.3 – dataset extended, color analysis integrated, accuracy improved; font‑identification prototype implemented (`FontModel`) but accuracy was judged too low for production — its integration into the visual pipeline was cancelled.
- Integration: Quality gates applied; ready for load testing.

**Exit Criteria:**
- All 13 issues (Sprints 4–5) are closed. **[VERIFIED BY: Daria]**
- The team can launch the documented load‑test scenarios against the prepared environment. **[VERIFIED BY: Ilya]**
- The Yandex scraper runs stably with < 5% failure rate. **[VERIFIED BY: Vladimir]**

---

### MS5 — Optimisation & Release Readiness (13–26 Jul)

**Objective:** Measure baseline performance, optimise models and scraping, and prepare final reporting.

**Key Deliverables:**

#### Performance Validation **[OWNER: Ilya]**
- Run baseline load tests (#76) and record metrics.
- Identify bottlenecks (#77).
- Make targeted improvements (caching, query optimisation, model batching).
- Run repeated load tests (#78) and compare results.

#### Model Final Optimisation
- **Text — benchmark & test report (delivered mid‑Jul):** constructed 7‑family perturbation benchmark (duplicates, word reorder, 1 and 2 phonetic edits, transliteration, affixes, translation pairs), 1,400 queries over the full 2.7 M‑alias index. **accuracy@200 = 92.6%** against the contractual ТЗ threshold ≥ 85% — **met**; hit@10 = 71.0%, MRR = 0.556; weakest family — translation pairs (65% hit@200, carried by the semantic channel alone). Methodology pairs score 93–98% versus a 47.5% mean for random cross‑class pairs; latency median 3.2 s / p95 9.9 s against the 120 s SLA; 105 unit tests green, preprocessing QA 99.0%, offline mode verified. **[OWNER: Daniel]**
- **Text optimisation (#19, Sprint 7, 20–26 Jul — To Do, 18 h planned):** restore the eval runner (script not preserved in the repo; the 1,400‑query benchmark file survives), one instrumented benchmark run dumping per‑channel candidate scores, then offline re‑ranking grid search (~20–50 k configurations: α, the four channel weights, semantic thresholds, containment length discount, short‑alias penalty). Objective: raise hit@10 / MRR under hard constraints — hit@200 ≥ 92.6% overall and translation family ≥ 65% — followed by a confirming live run and config/docs update. Estimated 2–3 working days. **[OWNER: Daniel]**
- **Visual (#26):** extra fine-tuning, combine VGG16 + color with balanced weights. Target: visual similarity accuracy@200 ≥ 0.85. **[OWNER: Alexander]**
- **Garbage sources (#17, Sprint 6 — in progress):** final analysis and mitigation; filtering rules land through the #19 grid search. **[OWNER: Daniel]**

#### Scraping Improvements
- Implement Google Books scraping (#83). **[OWNER: Vladimir]**
- Improve overall scraping quality (#82) – retry logic, error handling, data validation. **[OWNER: Vladimir]**

#### Final Reporting **[OWNER: Daria]**
- Prepare final presentation and report (#12).
- Link each strategic result to its GitHub issue, technical artifact, metric, test report, or demonstration evidence.
- Document what was delivered, what did not fit, and why.

**Model Status:**
- Text: `namecheck` 0.1.0 with documented benchmark metrics (accuracy@200 = 92.6%); #19 grid‑search optimisation of hit@10 / MRR scheduled for Sprint 7 (20–26 Jul).
- Visual: v2.0 – final combined model with documented metrics.
- Integration: Production‑ready, measured, and documented.

**Exit Criteria:**
- All 5 Sprint 7 issues satisfy their Definition of Done by 26 July, or an approved deviation is recorded. **[VERIFIED BY: Daria]**
- Load test results meet defined thresholds (P95 latency < 2 min, success rate > 95%). **[VERIFIED BY: Ilya]**
- Final report is complete and archived in the repository. **[VERIFIED BY: Daria]**

---

## 5. How the Model Evolved (Summary)

| Phase | Period | Text Model | Visual Model | Integration Status |
| :--- | :--- | :--- | :--- | :--- |
| **MS0** | 14 Feb – 2 Mar | Research kick‑off: methodology pair set, algorithm survey — no prototype yet **[OWNER: Daniel]** | Baseline: VGG16 embeddings (accuracy ~55%) **[OWNER: Alexander]** | Separate notebooks |
| **MS1** | 3 Mar – 13 Apr | Phonetic + string‑metric prototype (notebook + Streamlit demo, 13 Mar) **[OWNER: Daniel]** | Fine‑tuning stage 1 + embedding pipeline (accuracy measured) **[OWNER: Alexander]** | Components built, separate modules |
| **MS2** | 14 Apr – 31 May | v0 – rubert‑tiny2 embeddings + cosine search with МКТУ filter (4 May) **[OWNER: Daniel]** | v1.1 – embedding pipeline optimised **[OWNER: Alexander]** | Full E2E integration (Docker, API, frontend) **[OWNER: Ilya, Vladimir]** |
| **MS3** | 1–28 Jun | Encoder bake‑off → LaBSE selected; dump extraction + preprocessing modules **[OWNER: Daniel]** | v1.2 – fine‑tuning stage completed **[OWNER: Alexander]** | Integrated, observable, demoed **[OWNER: Ilya, Daria]** |
| **MS4** | 29 Jun – 12 Jul | `namecheck` 0.1.0 – 4‑channel formula, two‑stage search over 2.7 M aliases, API; tie‑break ranking fix (#18) **[OWNER: Daniel]** | v1.3 – color analysis **[OWNER: Alexander]**; font‑ID prototype built but not integrated (low accuracy) **[OWNER: Daniel]** | Quality gates applied, load‑test ready **[OWNER: Ilya, Vladimir]** |
| **MS5** | 13–26 Jul | Benchmarked: accuracy@200 = 92.6% (ТЗ ≥ 85% met); #19 grid search (hit@10 / MRR) planned for Sprint 7 **[OWNER: Daniel]** | v2.0 – combined model (accuracy@200 ≥ 0.85) **[OWNER: Alexander]** | Production‑ready, measured, documented **[OWNER: Ilya, Daria]** |

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
| **ML Models** | Text similarity — `namecheck` package: string + phonetic (G2P → IPA articulatory alignment) + containment + semantic (LaBSE) channels, two‑stage search over 2.7 M aliases with deterministic tie‑breaking; benchmarked at 92.6% accuracy@200; grid‑search calibration and garbage filtering planned (#19, #17). **[OWNER: Daniel]** Visual similarity (VGG16 + color, fine‑tuned, combined). **[OWNER: Alexander]** Font identification — research prototype (`FontModel`, embedding‑based retrieval); accuracy below the production bar, integration cancelled. **[OWNER: Alexander, Daniel]** |
| **Backend** | FastAPI, PostgreSQL/ClickHouse, Docker, CI/CD (GitHub Actions). **[OWNER: Ilya]** |
| **Parsers** | 11 external sources (Yandex, Google Play, App Store, RAO, MinCulture, YouTube, Google Books, etc.), with resilience and health checks. **[OWNER: Vladimir]** |
| **Frontend** | Minimal UI for registration and infringement checks. **[OWNER: Ilya]** |
| **Observability** | ELK + Prometheus + Grafana, application logs, APM traces, alerting. **[OWNER: Ilya]** |
| **Performance** | Load‑test scenarios, baseline and optimised metrics, bottleneck analysis. **[OWNER: Ilya, Daria]** |
| **Documentation** | Requirements, architecture, tactical plan, strategic plan, user manual, similarity formula, final report. **[OWNER: Daria]** |
