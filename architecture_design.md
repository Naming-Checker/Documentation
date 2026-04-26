# Architecture Design — NamingChecker

## Purpose
This document provides a high‑level architectural overview of the NamingChecker service, its components, and key design decisions, aligned with the C4 model. It serves as the reference for development and integration.

## System Context
NamingChecker is an internal MTS service that allows users to check new naming (text) and logos against:
- Internal trademark database (PostgreSQL)
- External sources (11 internet registries) aggregated offline
The service is deployed on an NVIDIA A100 within the corporate network, with **no runtime internet access**.

## Containers & Components

### 1. Backend API (FastAPI)
- **Responsibilities:** Accept user requests, orchestrate text similarity checks, logo similarity checks, and external data aggregation.
- **Endpoints:**
  - `/check-registration` – full registration check (text + optional logo)
  - `/check-infringement-text` – compare a text against a given trademark text
  - `/check-infringement-logo` – compare a logo against a given trademark logo
- **Integrations:** Preprocessing service, ML scoring modules, DB query layer, external aggregation service.

### 2. Text Preprocessing Service
- Cleans and normalises raw trademark descriptions (removes digits, disclaimers, generic terms).
- Embedded in the same FastAPI process for simplicity; uses a shared library.

### 3. ML Scoring Modules
- **Text Similarity Engine:** Combines phonetic (Metaphone + Levenshtein), semantic (RoSBERTa embeddings), and text metrics (inclusion, Damerau‑Levenshtein, Jaro‑Winkler) with configurable weights.
- **Logo Similarity Engine:** Extracts CNN embeddings (VGG16) and computes cosine similarity.
- Both are Python packages loaded by the backend.

### 4. Data Layer
- **PostgreSQL:** Stores pre‑processed trademark metadata, embeddings, and pre‑computed similarity indexes.
- **ClickHouse:** Used for fast analytical queries on large similarity ranking datasets (optional, based on performance needs).
- **Offline data store:** External source results are parsed, aggregated, and loaded periodically (not at runtime) into the database.

### 5. External Aggregation Service
- Dedicated microservice (internal) that manages periodic scraping/crawling of 11 external sources.
- Exposes an API for the backend to retrieve the top‑200 most relevant names for a given query.
- All internet access happens exclusively in this service, strictly offline for the rest of the system.

## Deployment View
- All components (backend, aggregation service) are containerised (Docker).
- The system runs on a single GPU node (NVIDIA A100) within MTS internal network.
- CI/CD (GitHub Actions) builds images, runs tests, and pushes artifacts to an internal registry.

## Key Design Decisions
- **Accuracy‑first scoring:** The weighted combination of phonetic, semantic, and text metrics was chosen to align with Rospatent guidelines.
- **Offline external data:** To meet the no‑internet requirement, external data is refreshed offline by a separate process.
- **Single GPU deployment:** Models are optimized for inference on A100; embeddings are computed in batches.
- **C4 diagrams:** Detailed component diagrams are available in `docs/c4/components/`.

## References
- [Tactical Plan](tactical_plan.md)
- [Requirements](requirements.md)
- [Quality Plan](quality_plan.md)
