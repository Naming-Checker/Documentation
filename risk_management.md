# Risk Management — NamingChecker

## Purpose
This document identifies key project risks, their probability and impact, and the mitigation strategies for the NamingChecker project. It is a living document updated during sprint retrospectives and phase reviews.

## Risk Register

| ID | Risk | Probability | Impact | Mitigation | Owner |
|----|------|-------------|--------|------------|-------|
| R1 | Pre‑processing cannot handle the extreme noise in raw trademark data | Medium | High | Develop iterative cleaning rules; involve legal expert to validate preprocessing results early | Daniel |
| R2 | Semantic similarity model does not align with legal interpretation of “confusing similarity” | High | Critical | Calibrate with a labelled dataset curated with legal experts; plan multiple feedback loops | Daniel, Daria |
| R3 | Latency exceeds 2 minutes due to heavy model inference on CPU or GPU underutilization | Medium | High | Profile early; batch embeddings; use GPU‑optimized inference; consider model quantization | Vladimir, Alexander |
| R4 | External source parsing breaks due to website changes (structure or blocking) | High | Medium | Implement robust parsers with fallback; monitor freshness; schedule regular parser updates | Ilya |
| R5 | Team workload imbalance (e.g., ML tasks taking longer while backend idle) | Medium | Medium | Cross‑training sessions; transparent backlog; Daria to adjust assignments in planning | Daria |
| R6 | Accuracy target (≥85%) not reached even after calibration | Medium | Critical | Allow alternative models (e.g., cross‑encoder reranking); allocate extra tuning time in May | Alexander, Daniel |
| R7 | Internal network restrictions complicate model downloads and dependency management | Low | High | Pre‑download all models and dependencies; store in internal artifact repository | Vladimir |
| R8 | Data freshness of offline sources degrades over time, reducing result relevance | Medium | Medium | Schedule regular updates; implement monitoring for source availability and data volume | Ilya |

## Monitoring and Review
- Risk register is reviewed at each sprint retrospective.
- New risks are added immediately; probability and impact are adjusted based on latest information.
- High‑impact risks with probability > medium are escalated to stakeholders during milestone demos.

## Contingency
- If by mid‑May the accuracy target is not met, the team will fall back to a simpler heuristic‑based ranking (phonetic + text metrics) while the semantic model continues to be improved for a later release.
- If external parsing becomes unreliable, the scope of external sources may be reduced (by stakeholder decision).
