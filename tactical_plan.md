# NamingChecker Tactical Plan: April – May 2026

## Team and Roles
- **Alexander** — visual similarity (logos)
- **Daniel** — text similarity (semantics, phonetics, metrics)
- **Vladimir** — backend (FastAPI, DB, CI/CD)
- **Ilya** — integrations (parsing external sources)
- **Daria** — documentation, context coordination

---

## Phase I: Foundation and Documentation (April 1–15)

### Daria
- **Task:** Complete detailed description of all requirements (#28) and use cases (#11)
- **Deliverable:** `docs/requirements.md` — approved team reference

### Daniel, Alexander, Vladimir, Ilya
- **Task:** Architecture analysis, finalize API contracts
- **Deliverable:** `docs/architecture.md` with component descriptions and interactions

---

## Phase II: Development and Integration (April 15 – May 15)

### Daniel
- Implement and train semantic and phonetic similarity models
- Quality testing (accuracy ≥ 85%)
- Code in `ml-models`, inference scripts

### Alexander
- Develop and train visual logo comparison model
- Same testing and code placement in `ml-models`

### Vladimir
- Backend: FastAPI application, business logic, all endpoints
- Design and set up PostgreSQL and ClickHouse databases
- Configure CI/CD, Docker containerization

### Ilya
- Parsers for 11 external sources (Google Play, YouTube, Kinopoisk, etc.)
- Data aggregation → list of 200 most relevant names within <2 min
- Integration microservice

---

## Phase III: Testing and Deployment (May 15–31)

### Daria, Vladimir
- Final documentation: similarity calculation formulas, user manual
- Deployment on GPU NVIDIA A100 in the internal network

### Entire Team
- Final accuracy testing of all models
- Report: `docs/testing_report.md`
