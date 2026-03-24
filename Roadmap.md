# NamingChecker Project Roadmap

**Current Date:** March 24, 2026  
**Phonetic & Graphic Models:** Already implemented

---

## Introduction

This roadmap outlines the remaining work for the NamingChecker project, a trademark and brand name verification system. The timeline begins on March 24, 2026, leveraging existing phonetic and graphic similarity models. The plan follows the milestones from the project documentation, adjusted for current progress.

---

## Roadmap Overview

| Phase | Tasks | Start | End | Deliverable |
|-------|-------|-------|-----|-------------|
| **1. Data Preparation** *(partially complete)* | - Extract and clean internal trademark registry (PostgreSQL)<br>- Build ETL pipelines for external sources (app stores, media registries)<br>- Preprocess core names, generate embeddings for fastText/LaBSE<br>- Store processed data in ClickHouse with vector indexes | *in progress* | Apr 6, 2026 | Cleaned internal dataset (≥50k names) + first external index (Google Play, RAO) |
| **2. Similarity Engine – Finalization** | - Finalize semantic similarity module (fastText/LaBSE, translation)<br>- Combine phonetics (existing) + graphics (existing) into weighted score<br>- Implement logo matcher (perceptual hash + ResNet-50)<br>- Tune weights on a small validation set | Mar 24, 2026 | Apr 20, 2026 | Fully functional similarity engine (semantic+phonetic+graphic) with logo comparison |
| **3. Orchestrator & API** | - Build orchestrator (candidate retrieval, scoring, ranking)<br>- Develop REST API (FastAPI) with authentication<br>- Implement caching (Redis) and request queueing<br>- Integrate external searcher (pre-indexed data) | Apr 21, 2026 | May 12, 2026 | Deployable API with all endpoints documented |
| **4. Frontend (Streamlit)** | - Create user interface for name queries, logo uploads<br>- Visualise results with similarity breakdowns<br>- Add filters (MKTU classes, threshold, max results)<br>- Connect to backend API | May 13, 2026 | May 27, 2026 | Interactive demo ready for internal testing |
| **5. Testing & Validation** | - Accuracy testing: 500 query names annotated by legal experts → measure Precision@200, Recall<br>- Performance testing: simulate 10 concurrent users, measure 95th percentile response time (<2 min)<br>- Regression testing: ensure no degradation after changes | May 28, 2026 | Jun 15, 2026 | Test report + final similarity weights (≥85% precision) |
| **6. Deployment & Documentation** | - Containerize all components (Docker)<br>- Prepare Kubernetes manifests<br>- Set up monitoring (Prometheus/Grafana) and logging (ELK)<br>- Write user manual + technical docs | Jun 16, 2026 | Jun 30, 2026 | Production-ready system deployed on internal GPU cluster |

---

## Key Assumptions & Dependencies

- **Data availability**: Internal trademark database is accessible and has been partially preprocessed.
- **External sources**: Initial scraping of app stores and media registries is underway; final indexing will be completed by early April.
- **Legal expert time**: Availability for annotating test queries is confirmed for the testing phase.
- **GPU resources**: NVIDIA A100 server is ready and accessible for training/inference.

---

## Risk Mitigation

- **Accuracy below target**: Reserve two weeks for iterative weight tuning and ensemble testing.
- **Performance bottlenecks**: Use FAISS in ClickHouse for vector search; implement query caching.
- **External data changes**: Build resilient parsers with fallbacks; schedule monthly refreshes.

---

## Immediate Actions (March 24 – April 6)

1. Finalise data pipeline – complete extraction for all external sources.
2. Integrate existing phonetics & graphics models into a unified scoring class.
3. Start semantic similarity implementation – load pre-trained LaBSE and fastText models.
