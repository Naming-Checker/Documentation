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

