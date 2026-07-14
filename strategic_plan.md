# NamingChecker Strategic Plan — July 6 – July 26, 2026

## 1. Strategic Context

This 3‑week window marks the transition from MVP functionality to **production‑ready hardening**. The core system works, but we have identified critical gaps that directly impact user trust and system viability:

- **Ranking quality** suffers from "garbage" in search results, reducing precision.
- **External parsers** (especially Yandex) are fragile and prone to detection/blocking.
- **Performance & scalability** have not been formally validated under realistic load.
- **Visual similarity** lacks advanced features (color analysis) needed for logo comparisons.
- **Load testing** infrastructure and metrics are not yet defined, making performance targets speculative.

The strategic goal for this period is to **close these gaps** so that the system can safely move into a pilot phase with real users (Phase 3).

---

## 2. Strategic Objectives (July 6 – July 26)

| # | Objective | Why It Matters |
| :--- | :--- | :--- |
| **O1** | Achieve measurable improvement in ranking precision (≥ +5% Precision@10) by eliminating garbage sources and recalibrating weights. | Directly improves user trust and reduces false positives in legal/commercial contexts. |
| **O2** | Ensure parser robustness – Yandex scraper must operate with < 5% failure rate under sustained daily runs. | Data freshness and coverage are core value propositions; brittle parsers kill reliability. |
| **O3** | Establish a baseline for system performance under load (latency, throughput, error rates) with defined metrics and a reproducible test suite. | Without baselines, we cannot commit to SLAs or detect regressions. |
| **O4** | Integrate color analysis into the visual pipeline and validate its added value. | Differentiates our visual offering from pure text‑based tools and improves logo matching. |
| **O5** | Maintain team alignment through weekly retrospectives and transparent tracking. | Ensures we adapt quickly to blockers and retain focus on the highest‑impact work. |

---

## 3. Strategic Priorities by Domain

### ML & Research (Daniel & Alexander)
- **Ranking & Garbage (Daniel)**
  - Identify the root causes of garbage in the top‑10 results (#17).
  - Deploy a filtering mechanism and recalibrate the similarity formula (#18).
  - **Outcome:** A new ranking version validated offline with clear metric improvements.

- **Visual & Color Analysis (Alexander)**
  - Implement and test color histogram comparison (#22).
  - Determine if the combined score (VGG16 + color) outperforms the baseline.
  - **Outcome:** A production‑ready visual module with at least 3% accuracy gain, ready for integration.

### Parsing & Integration (Vladimir)
- **Yandex Scraper Hardening (#81)**
  - Implement proxy rotation, user‑agent strategies, and retry logic.
  - Validate stability over 100+ consecutive requests.
  - **Outcome:** A scraper that survives anti‑bot measures and reliably delivers data.

### Backend & Infrastructure (Ilya)
- **Load Testing Foundation (#73, #74, #75)**
  - Define key metrics (RPS, latency percentiles, error rates).
  - Provision a staging environment that mirrors production.
  - Implement load test scenarios and run baseline measurements.
  - **Outcome:** Clear performance baselines and a reusable test harness.

### PM & Coordination (Daria)
- **Tactical Planning & Tracking (#10)**
  - Keep the tactical plan aligned with reality.
  - Ensure weekly reviews (July 12, 19, 26) capture lessons learned.
  - **Outcome:** Full visibility into progress, blockers, and team health.

---

## 4. Strategic Success Criteria (Exit: July 26, 2026)

By the end of July 26, the following **strategic conditions** must be met to declare success:

- ☑ **Ranking precision (Precision@10)** has improved by at least **5%** against the baseline, verified by an offline evaluation run.
- ☑ **Yandex parser** operates with a failure rate of **less than 5%** over 3 consecutive daily batch runs.
- ☑ **Load test baselines** are established – we know our current P95 latency and RPS limits, and we have a CI‑runnable load test suite.
- ☑ **Color analysis** is integrated into the visual pipeline and has been validated on the labelled logo dataset.
- ☑ **All 8 sprint tasks** (#81, #22, #18, #10, #75, #73, #17, #74) are **closed** (or have a clear, documented path to closure).
- ☑ **Three weekly retrospectives** (July 12, 19, 26) have been conducted, and at least 2 actionable process improvements have been implemented.

---

## 5. Strategic Risks & Mitigations (This Period)

| Risk | Likelihood | Impact | Mitigation |
| :--- | :--- | :--- | :--- |
| **Yandex blocks our scrapers permanently** | Medium | High – loss of a key data source | Implement fallback sources; use off‑line snapshots; engage experts on evasion tactics. |
| **Ranking improvements do not yield +5%** | Medium | Medium – delayed pilot readiness | Re‑evaluate weights; consider simpler filtering first; adjust target if necessary (with stakeholder agreement). |
| **Load test environment is not ready in time** | Low/Medium | Medium – no baseline to track | Start with smaller‑scale tests; use existing staging environment with limited data. |
| **Team overload (8 tasks in 3 weeks)** | Medium | High – burnout and quality drop | Re‑prioritise if needed; defer lower‑impact improvements to Sprint 7 if critical tasks slip. |
| **Color analysis integration breaks visual pipeline** | Low | Medium – regression in existing feature | Run full regression suite before merging; have a rollback plan. |

---

## 6. Resource Strategy (July 6–26)

| Resource | Allocation |
| :--- | :--- |
| **Daniel** | 100% – Ranking, garbage research, and weight calibration. |
| **Alexander** | 100% – Color analysis, visual pipeline integration. |
| **Vladimir** | 100% – Parser hardening (Yandex) and regression testing. |
| **Ilya** | 100% – Load testing (infrastructure + scripts) and backend integration support. |
| **Daria** | 50% – PM overhead (planning, retrospectives, demos) + 50% – Load test metric definition and documentation. |
| **Infrastructure** | Dedicated A100 GPU instance; staging environment provisioned by July 10. |

---

## 7. Governance & Strategic Reviews

| Activity | Date | Owner | Purpose |
| :--- | :--- | :--- | :--- |
| **Sprint Planning (Sprint 6)** | Jul 13 (Mon) | Daria | Adjust priorities based on Sprint 5 outcomes. |
| **Weekly Demo / Review** | Jul 12, 19, 26 (Fridays) | Daria | Showcase completed work to stakeholders; validate strategic progress. |
| **Weekly Retrospective** | Jul 12, 19, 26 (Fridays) | Daria | Capture process improvements and address blockers. |
| **Mid‑Period Strategy Check** | Jul 20 (Mon) | Team | 1‑hour sync to assess if we are on track to meet the July 26 success criteria. |

---

## 8. Handover to Next Phase (Post‑July 26)

At the end of this strategic period, the team will be ready to:

- **Enter the Pilot Phase (Phase 3)** – with stable parsers, improved ranking, and known performance characteristics.
- **Define the next tactical plan** for August – focusing on user feedback, UX improvements, and pilot deployment.
- **Update the long‑term roadmap** with real‑world data from this hardening effort.

