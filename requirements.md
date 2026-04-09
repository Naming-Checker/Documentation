# Requirements

## Functional Requirements

- The service shall support two core flows: registration check for a new naming in Russia and text trademark misuse check.
- The service shall perform semantic, linguistic, and phonetic matching for naming search.
- Registration flow shall consider Nice classes (MKTU) and prefilter candidates by matching classes.
- Registration flow shall return a ranked top-200 list of most similar/conflicting candidates with similarity percentage.
- Text infringement flow shall support pairwise comparison of protected naming and suspicious naming with similarity percentage.
- The API shall expose the following endpoints: `/api/v1/registration-check`, `/api/v1/text-infringement`, `/api/v1/logo-comparison`, `/api/v1/webhooks/stage2-results`.
- Stage 2 results shall be delivered via webhook, with partial results allowed and unordered delivery accepted.
- Input validation shall enforce at least one Nice class (`mktu_codes`) for relevant flows.

## Non-functional Requirements

- Quality target: accuracy shall be at least 85%.
- Response time target for full query: under 2 minutes.
- Latency/SLA targets for staged flow: Stage 1 internal response `P95 = 60s`, `P99 = 100s`; Stage 2 delivery `SLA <= 120s`.
- Availability target: 99.5%-99.9%.
- Async reliability requirements: up to 3 retries, exponential backoff, timeout 60s per external source.
- Async monitoring thresholds: delay alert 5 minutes, fail-rate alert 2%, DLQ control threshold 5 messages.

## Technical Constraints

- Runtime environment: internal corporate network deployment.
- Runtime network constraint: no external internet calls during service operation; models and dependencies must be preloaded.
- Required core stack: Python 3.10-3.11, FastAPI, PostgreSQL, ClickHouse, Docker.
- Target infrastructure: NVIDIA A100 PCIe 80GB GPU.
- Backend packaging/tooling constraints: `requires-python >=3.10,<3.12`, Ruff target `py311`, mypy `python_version = 3.11`.
- Container runtime baseline is pinned to Python 3.11.

## Requirements Management Strategy

- Maintain this file as the single approved baseline for product and system requirements.
- Accept requirement changes only after confirming a source artifact update (system analysis, API contracts, or architecture docs).
- Process updates through a fixed flow: `new input -> impact check -> wording update -> stakeholder review -> baseline refresh`.
- Keep requirement statements atomic and testable; avoid combined items that mix business behavior and implementation detail.
- Mark conflicting updates as `Pending Clarification` and do not merge them into baseline requirements until resolved.
- For each approved update, revise only affected requirement bullets and run a full consistency pass across all three sections.
