# NamingChecker Tactical Plan (with Quality Gates) — April–May 2026

## Team & Quality Ownership
| Team Member     | Main Role                 | Quality Focus (per Quality Plan)                         |
|-----------------|---------------------------|----------------------------------------------------------|
| Alexander       | Visual similarity model   | Logo model quality & visual similarity evaluation        |
| Daniel          | Text similarity model     | Phonetic, semantic & final text‑score quality            |
| Vladimir        | Backend & infrastructure  | API, preprocessing, text metrics, DB search, CI/CD       |
| Ilya            | Integrations & parsing    | External‑source parsing quality & data freshness         |
| Daria           | Documentation & PM        | Requirements consistency, acceptance alignment, stakeholder demos |

## Quality Activities Embedded in the Plan
Based on the project’s Quality Plan, every task includes:
- **Inspection** – requirements / API contracts / pull request reviews  
- **Testing** – unit, integration, end‑to‑end, and model evaluation  
- **Analysis** – linting (Ruff), static typing (mypy), coverage, latency, model metrics  
- **Demo** – milestone demonstrations with legal/domain experts  

All work goes through feature branches → PR → CI gates → merge only if all checks pass.  
Quality gates are marked 🛡️.

---

## Phase 0: Foundation & Quality Baseline (1–7 April)

### Daria (PM / Analyst)
- Finalise `requirements.md` (including all similarity rules, non‑functional constraints, and external sources)  
- Define acceptance criteria for “valid similarity” together with legal experts  
🛡️ **Gate:** Requirements signed off by legal stakeholder; no un‑clarified ambiguity.

### All team members
- Review and align `architecture.md` (API contracts, data flows, component boundaries)  
- Agree on test‑dataset format and initial labeling guidelines  
🛡️ **Gate:** Architecture baseline approved; initial test dataset prepared (≥50 labelled pairs).

---

## Phase I: Core Development & Continuous Quality (8 April – 7 May)

### Daniel – Text Similarity Module
1. Build preprocessing pipeline (normalisation, digit/abbreviation removal, disclaimer handling)  
2. Implement phonetic similarity (Russian Metaphone + Levenshtein) – **unit tested**  
3. Implement semantic similarity (RoSBERTa embeddings + cosine) – **unit tested**  
4. Implement aggregated text metric (inclusion, Damerau‑Levenshtein, Jaro‑Winkler) – **unit tested**  
5. Combine into weighted formula `W1*SemanticSim + W2*PhoneticSim + W3*TextSim`  
6. Calibrate weights on labelled dataset to reach accuracy ≥ 85% – **evaluation script**  
🛡️ **Gates per subtask:** PR reviewed, CI green (Ruff, mypy, pytests pass), metric evaluation shows no regression.

### Alexander – Visual Similarity Module
1. Set up CNN‑based embedding extraction (VGG16)  
2. Implement logo‑comparison scoring  
3. Train / fine‑tune on internal logo dataset (if available)  
4. Evaluate accuracy on labelled logo pairs  
🛡️ **Gates:** Same CI + evaluation gates as text module; model metrics reviewed against baseline.

### Vladimir – Backend Core
1. FastAPI project skeleton, Dockerfile, CI/CD pipeline  
2. PostgreSQL / ClickHouse schema for pre‑computed embeddings and raw data  
3. Implement `/check‑registration` endpoint (text + logo flow)  
4. Implement `/check‑infringement` endpoints (text‑only, logo‑only)  
5. Pre‑processing service for raw trademark fields (use Daniel’s pipeline)  
6. Integration tests for all endpoints with test database  
🛡️ **Gates:** All API contracts must match approved architecture; integration tests cover both success and error paths; latency of DB query + scoring measured and kept < 2 min.

### Ilya – External Source Integration
1. Build parsers for 11 external sources (Google Play, App Store, RAO, MinCulture, etc.) – **unit tests per parser**  
2. Aggregator service that returns top‑200 relevant names from a given query  
3. Ensure offline data freshness (update mechanism without runtime internet access)  
4. Integration tests to verify parser robustness and response time  
🛡️ **Gates:** Parser regression tests; aggregated latency < 2 min for full query; data freshness check automated.

---

## Phase II: Integration & Quality Hardening (8–21 May)

### Whole Team
1. Integrate text similarity module + visual module + backend into single Docker‑composed service  
2. End‑to‑end tests for all three use cases (registration check, text infringement, logo infringement)  
3. Performance testing under A100 target environment  
4. Regression testing on full labelled dataset after integration  
🛡️ **Gate:** Full E2E suite passes; accuracy ≥ 85% on labelled dataset; latency sustained < 2 minutes; no critical bugs in core flows.

### Daria
- Prepare internal user manual (how to use the service, interpretation of similarity scores)  
- Prepare detailed documentation of similarity formula, weights, and calibration results  
🛡️ **Gate:** Documentation reviewed by legal and development team for correctness.

---

## Phase III: Final Validation & Release (22–31 May)

### All Team Members
- Milestone demo with stakeholders (legal department, potential users) – collect feedback  
- Final polishing based on demo feedback  
- Final regression run on the most recent dataset  
🛡️ **Gate:** Stakeholder sign‑off; all quality measurements (accuracy, latency, coverage) meet thresholds.

### Daria
- Tidy up `README.md`, `configuration_management.md`, and roadmaps  
- Archive final reports (testing report, metric baselines, demo feedback)  

### Vladimir
- Final deployment on internal A100 GPU, network‑isolated environment  

### Final Quality Gates
☑ All required CI checks pass  
☑ No blocking defects in core flows  
☑ Regression suite passes after any last changes  
☑ Quality metrics (accuracy, latency) verified against baselines  
☑ Documentation synchronised with final implementation  
☑ Release candidate container ready for production use

---

## Appendix: Similarity Calculation Summary
Included in documentation; key points:

- **PhoneticSim** = 1 − norm_levenshtein(Metaphone(w1), Metaphone(w2))  
- **SemanticSim** = cosine(embed(w1), embed(w2))  
- **TextSim** = max(inclusion_score, 0.5*DamerauLevenshtein_norm + 0.5*JaroWinkler)  
- **Overall Text Similarity** = W1·SemanticSim + W2·PhoneticSim + W3·TextSim  
  (weights calibrated on labelled data; W1+W2+W3 = 1.0)  
- **Visual Similarity** (independent) = cosine(VGG16_embed(img1), VGG16_embed(img2))

Calibration details, baselines, and examples are in `docs/similarity_formula.md`.
