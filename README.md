# NamingChecker

**NamingChecker** is an internal service for automated trademark and brand name verification. It helps reduce the legal department’s workload by checking proposed names for conflicts with existing trademarks, products, tariffs, and publicly available names (app stores, media registries, etc.). The service also detects potential trademark misuse by comparing logos and textual names against a comprehensive database of protected marks.

## Features

- **Semantic, Phonetic, and Graphic Similarity** – Multi‑dimensional comparison based on Russian trademark guidelines (FIPS).
- **Top‑200 Results** – Returns the 200 most similar names with similarity percentages.
- **Logo Comparison** – Image‑based similarity using deep learning feature extraction.
- **External Source Integration** – Pre‑loaded indexes from app stores, media registries, and internet sources (no live external calls at runtime).
- **High Accuracy** – Precision ≥85% on the top 200 results.
- **Fast Response** – Complete query in under 2 minutes on NVIDIA A100 GPU.
- **Fully Self‑contained** – Runs inside the corporate network; all models and data are pre‑loaded.

## Tech Stack

- **Backend**: Python 3.10–3.11, FastAPI
- **Databases**: PostgreSQL (metadata), ClickHouse (vector similarity search)
- **Machine Learning**: PyTorch, Transformers, FAISS, OpenCV
- **Infrastructure**: Docker, NVIDIA A100 GPU, internal network

## Test stand integration note

On the test stand, similarity search for logos and text runs through separate CPU sidecars:

- `visual-model-service` for `POST /api/v1/logo-similarity/search`
- `text-model-service` for `POST /api/v1/text-similarity/search`

Both sidecars use precomputed artifacts mounted from host directories and are reached internally by the backend over Docker network. The production target architecture with GPU and data stores remains documented in the broader architecture materials.

