# Quality Plan

## Purpose
This plan defines how quality is managed in NamingChecker: an internal MTS service for naming and logo similarity checks. It reflects the real project constraints: internal-only deployment, no runtime external internet access, A100 GPU target environment, FastAPI backend, PostgreSQL/ClickHouse storage, and ML-based ranking.

## 1. Activities
We use four practical quality activities:
- **Inspection** — requirements, API contracts, pull requests.
- **Testing** — preprocessing, similarity modules, API flows, end-to-end scenarios.
- **Analysis** — code quality, typing, coverage, latency, model metrics.
- **Demo** — milestone validation with stakeholders, especially legal/domain experts.

These activities fit the project because it combines backend logic, ML quality, and business-critical review.

## 2. Interactions
Quality is embedded into the normal workflow:
- source artifacts are updated first;
- implementation follows approved baseline only;
- work goes through feature branches and pull requests;
- CI gates run before merge and deployment;
- quality results are reviewed during planning, evaluation, and release decisions.

## 3. Artifacts
Quality activities cover:
- backend code;
- preprocessing logic;
- text and logo similarity modules;
- REST API endpoints;
- DB queries and ranking logic;
- requirements and roadmap artifacts;
- configuration and deployment files;
- test datasets and evaluation scripts.

## 4. Timing
Quality activities happen continuously:
- **Before implementation** — review requirements and acceptance logic.
- **During implementation** — PR review, local checks, unit/integration tests.
- **Before merge** — CI checks and required gates.
- **Before milestone demo/release** — end-to-end validation, metric review, latency check.
- **After major model/data changes** — regression checks on labeled datasets.

## 5. Responsibility
- **ML Engineer №1** — logo model quality and visual similarity evaluation.
- **ML/NLP Engineer №2** — phonetic, semantic, and final text-score quality.
- **Backend Engineer №1** — API, preprocessing, text metrics, DB search, integration quality.
- **Backend Engineer №2** — searching and parsing.
- **PM / Analyst** — requirements consistency, acceptance alignment, stakeholder validation.
- **Whole team** — review, regression prevention, release readiness.

## 6. Extent
We use risk-based coverage:
- unit tests for core backend and preprocessing logic;
- integration tests for API and DB-backed flows;
- end-to-end tests for registration check, text infringement, and logo comparison;
- labeled dataset evaluation for text and logo similarity;
- regression testing after changes in models, scoring, or preprocessing.

Critical modules must be tested directly.

## 7. Cost / Time
Quality effort is planned as part of delivery:
- PR review and local validation — part of every task;
- automated checks — part of every merge;
- dataset evaluation and tuning — part of model iterations;
- milestone demos and acceptance review — part of roadmap checkpoints.

The largest quality effort is allocated to preprocessing, similarity accuracy, and latency, because these are the main project risks.

## 8. Tools
Main tools:
- **Ruff** — linting;
- **mypy** — static typing;
- **pytest** — unit and integration tests;
- **pytest-cov** — coverage reporting;
- **FastAPI test client** — API checks;
- **custom evaluation scripts** — precision, accuracy, recall, F1, latency;
- **Docker / CI pipeline** — repeatable validation in target runtime.

Typical commands:
```bash
ruff check .
mypy .
pytest
pytest --cov=.
```

Project-specific evaluation also includes:
- text similarity quality on labeled naming pairs;
- logo similarity quality on labeled image pairs;
- latency measurement for the full query flow.

## 9. Training
The team needs working knowledge in:
- FastAPI and backend testing;
- PostgreSQL / ClickHouse query validation;
- ML evaluation metrics;
- handling labeled datasets;
- CI usage and debugging;
- project-specific legal meaning of “similar” vs “not similar”.

Calibration with legal experts is required because model quality depends on expert interpretation.

## 10. Blocking Rules
The following rules block merge or release:
- requirement changes are not synchronized with baseline artifacts;
- required CI checks fail;
- critical tests fail;
- API behavior conflicts with approved contracts;
- regression on agreed quality metrics is not explained and accepted;
- release candidate does not meet mandatory operational constraints.

## 11. Measurements
The project tracks:
- **Accuracy / Precision** for naming search;
- **recall / F1** where relevant for infringement evaluation;
- **latency** for full query flow and staged responses;
- **test pass rate**;
- **coverage trend**;
- **defect / regression count**;
- **data freshness** for offline-loaded external sources;
- **CI status** for every merge candidate.

## Quality Gates
Practical gates for NamingChecker:
- all required CI checks pass;
- no blocking defects in core flows;
- regression suite passes after changes in preprocessing, scoring, or models;
- quality metrics are reviewed against labeled dataset baselines;
- latency stays within agreed limits for the target environment.
