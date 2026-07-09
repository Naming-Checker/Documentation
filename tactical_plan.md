# NamingChecker Tactical Plan — July 6 – July 26, 2026

## 1. Current Sprint Snapshot (Sprint 5: July 6 – July 12)

| Task | ID | Owner | Status | Domain |
| :--- | :--- | :--- | :--- | :--- |
| Сделать скрапинг Yandex ресурсов более устойчивым к обнаружению | #81 | Vladimir | **In Progress** | Parsing |
| Сравнение логотипов по цветовому анализу | #22 | Alexander | **In Progress** | ML |
| Улучшить порядок ранжирования | #18 | Daniel | **In Progress** | ML |
| Доработка tactical plan, проверка спринта и задач | #10 | Daria | **In Progress** | PM |
| Реализовать сценарии нагрузочного тестирования | #75 | Ilya | **To Do** | Development |
| Определить цели и ключевые метрики нагрузочного тестирования | #73 | Daria | **In Progress** | CA |
| Определить источник мусора в выдаче | #17 | Daniel | **In Progress** | Research |
| Подготовить инфраструктуру для нагрузочного тестирования | #74 | Ilya | **To Do** | Development |

**Sprint period:** Jul 06 – Jul 12 | **Ideal Hours:** 94 | **Retrospective:** Jul 12 (Friday)

---

## 2. Team & Quality Ownership

| Team Member | Main Role | Quality Focus (per Quality Plan) |
| :--- | :--- | :--- |
| **Alexander** | Visual similarity / ML | Logo model quality, visual similarity, color analysis ranking |
| **Daniel** | Text similarity / ML | Phonetic/semantic scoring, ranking optimization, garbage identification |
| **Ilya** | Backend & infrastructure | API stability, load testing, CI/CD, infrastructure hardening |
| **Vladimir** | Integrations & parsing | Parser robustness (Yandex), data freshness, scraping stability |
| **Daria** | PM | Requirements consistency, tactical planning, sprint tracking, metric definition |

**Quality Gates (🛡️):** All work goes through feature branches → PR → CI gates (Ruff, mypy, pytests) → merge only if all checks pass.

---

## 3. Sprint 5: Foundation & Infrastructure Hardening (July 6 – July 12)

### Daria (PM) – Tasks #73 & #10
- **#73** – Finalize the load testing strategy: define key metrics (RPS, latency percentiles, error rates, resource utilization). Currently **In Progress**.
- **#10** – Update this tactical plan to align with current sprint goals.
- Prepare the weekly retrospective agenda for **July 12**.
- 🛡️ **Gate:** Load testing metrics defined and documented; tactical plan approved by the team.

### Ilya (Backend) – Tasks #74 & #75 (prep)
- **#74** – Prepare infrastructure for load testing: provisioning test environments, monitoring stacks, and data seeding. Currently **To Do**.
- Set up CI pipelines for performance benchmarks.
- 🛡️ **Gate:** Test environment mirrors production; monitoring dashboards are operational.

### Vladimir (Parsing) – Task #81
- **#81** – Refactor the Yandex scraping module to be more resistant to detection (anti-bot mechanisms, proxy rotation, user-agent strategies). Currently **In Progress**.
- Validate parser output quality against known datasets.
- 🛡️ **Gate:** Scraper runs stably for 100+ consecutive requests without blocking; regression tests pass.

### Daniel (Text ML) – Tasks #17 & #18 (research phase)
- **#17** – Identify the source of garbage in search results. Currently **In Progress**.
  - Analyze false positive cases in the current ranking output.
  - Categorize "garbage" (irrelevant phonetic matches, noisy text embeddings, malformed data).
  - Propose a filtering mechanism.
- 🛡️ **Gate:** Report delivered on garbage sources with actionable recommendations.

### Alexander (Visual ML) – Task #22
- **#22** – Compare logos using color analysis. Currently **In Progress**.
  - Implement color histogram comparison as an additional visual feature for logo ranking.
  - Evaluate the impact on visual similarity precision.
- 🛡️ **Gate:** Color analysis prototype passes offline evaluation; integration plan is ready for Sprint 6.

---

## 4. Sprint 6: Development & Optimization (July 13 – July 19)

### Ilya (Backend) – Task #75
- **#75** – Implement load testing scenarios. Currently **To Do** – must be started this sprint.
  - Write realistic load test scripts (simulating registration checks and infringement checks).
  - Execute baseline tests and record metrics against the targets defined in #73.
- Begin integrating Daniel's ranking improvements (if ready) into the API.
- 🛡️ **Gate:** Load test scripts are merged; baseline latency and throughput are recorded.

### Vladimir (Parsing)
- Apply Yandex scraper improvements (#81) to other external sources (if applicable).
- Optimize parser aggregation time and implement health checks.
- 🛡️ **Gate:** Parser average response time < 2 seconds; failure rate < 5%.

### Daniel (Text ML) – Task #18
- **#18** – Improve the ranking order. Currently **In Progress**.
  - Implement garbage-filtering rules identified in #17 (e.g., exclude domain-specific noise, adjust phonetic threshold).
  - Re-calibrate the `W1, W2, W3` weights to prioritize semantic matches over phonetics.
  - Run regression against the labelled dataset (target: +5% precision@10).
- 🛡️ **Gate:** Offline metrics show improvement; no degradation in recall for high-priority targets.

### Alexander (Visual ML)
- Finalize the color similarity module (#22) and integrate it with the main visual pipeline.
- Test the combined visual score (VGG16 + color histogram) on the logo dataset.
- 🛡️ **Gate:** Combined model accuracy improves over the baseline VGG-only model by at least 3%.

### Daria (PM)
- Track Sprint 6 burndown.
- Prepare the internal demo for the week's achievements (parsing robustness, load test setup, ranking prototypes).
- 🛡️ **Gate:** Weekly progress report delivered; backlog refined for Sprint 7.

---

## 5. Sprint 7: Integration, Validation & Handover (July 20 – July 26)

### Whole Team – Integration & Polish
- **Ranking & Filtering Integration** (Daniel + Ilya):
  - Merge the new ranking logic (with garbage filtering) into the main backend service.
  - Update API responses to include new confidence scores (if applicable).
- **Visual Pipeline Integration** (Alexander + Ilya):
  - Deploy the color-augmented visual model into the Docker-composed service.
  - Ensure the end-to-end flow for logo checks works seamlessly.
- **Load Testing Execution** (Ilya + Vladimir):
  - Run full-scale load tests on the integrated system.
  - Validate that latency targets (< 2 minutes for full query) are met under peak load.
- **Parser Maintenance** (Vladimir):
  - Schedule automated weekly updates for all external sources.
  - Implement health checks for each parser.
- 🛡️ **Gate:** Full E2E regression suite passes; load test results meet defined thresholds; all external source integrations are healthy.

### Daria (PM)
- Finalize the tactical plan handover and archive it in the repository.
- Prepare the Sprint 7 release notes.
- Collect feedback from the team for the **monthly retrospective** (scheduled for **July 26**).
- 🛡️ **Gate:** Release notes approved; all documentation updated.

---

## 6. Final Quality Gates (by end of July 26)

- ☑ All required CI checks pass (Ruff, mypy, pytests).
- ☑ No blocking defects in core registration and infringement flows.
- ☑ Load test scenarios run successfully without critical failures (>95% success rate under target RPS).
- ☑ Ranking precision (Precision@10) improved by at least 5% compared to the previous production version.
- ☑ Yandex parser is operational with less than 5% failure rate per batch.
- ☑ Color analysis is successfully integrated and tested in staging.
- ☑ Sprint Retrospective (July 26) captures actionable improvements for the next cycle.

---

## 7. Cadence & Meetings (July 2026)

| Activity | Date | Owner | Audience |
| :--- | :--- | :--- | :--- |
| Sprint Planning (Sprint 6) | Jul 13 (Mon) | Daria | Team |
| Sprint Review / Demo (Sprint 5) | Jul 12 (Fri) | Daria | Stakeholders + team |
| Retrospective (Sprint 5) | Jul 12 (Fri) | Daria | Team |
| Sprint Review / Demo (Sprint 6) | Jul 19 (Fri) | Daria | Stakeholders + team |
| Retrospective (Sprint 6) | Jul 19 (Fri) | Daria | Team |
| Sprint Planning (Sprint 7) | Jul 20 (Mon) | Daria | Team |
| Sprint Review / Demo (Sprint 7) | Jul 26 (Fri) | Daria | Stakeholders + team |
| Monthly Retrospective | Jul 26 (Fri) | Daria | Team |
