# Strategic Plan -- May 2026

Main goals:

- close the definition of "similar";
- get a labeled test set;
- prepare the visual model and text preprocessing.

Dev environment with GPU is not yet provisioned. Securing it is an explicit task for this month; until then, model work is limited to architecture, code, and small-scale prototyping.

## Goals

| # | Goal | Exit criterion | Owner |
|---|------|----------------|-------|
| G1 | Formalize metrics (M10) | Metrics spec approved by legal | Team |
| G2 | Labeled test dataset | Test set with expert labels ready for model validation (logos + namings) | Daniel (text), Alex (logos) |
| G3 | Visual model ready to train (M1) | Architecture chosen, training script runnable end-to-end on sample data | Alex |
| G4 | Model tests and documentation | Test suite covering May modules; documentation written and in the repo | Daria, Alex, Daniel |
| G5 | Dev environment with GPU | A100 (or equivalent) access confirmed | Daria, Vladimir |

## Weekly Plan

Each task is scoped to roughly 6 hours of work per person per week.

### Week 1 (May 1–7)

| Owner | Task |
|-------|------|
| Daria | Missing project documentation; follow up on GPU request and book legal session |
| Daniel | Metrics spec draft -- metric list, candidate thresholds, worked examples |
| Alex | Rerun existing visual baseline on available hardware; capture starting metrics |
| Ilya | Backend architecture outline; documentation |
| Vladimir | Investigate parser approaches (existing libraries, prior work); short proposal and CI skeleton |

### Week 2 (May 8–14)

| Owner | Task |
|-------|------|
| Daria | Run legal session; incorporate feedback; metrics spec  signed off; update product status doc |
| Daniel | Labeling guidelines for namings; label first 100 naming pairs |
| Alex | Benchmark two candidate architectures; write ADR for visual model |
| Ilya | Backend module boundaries (parser, search, API); architecture doc |
| Vladimir | Parser  -- basic normalization (case, whitespace, punctuation) + unit tests |

### Week 3 (May 15–21)

| Owner | Task |
|-------|------|
| Daria | Mid-month review; GPU follow-up; mentor sync; update risk register and status docs |
| Daniel | Extend naming test set; measure agreement on control subset with legal |
| Alex | Label logo pairs; end-to-end training script on sample data |
| Ilya | Architecture doc update -- parser-to-pipeline contracts; API stubs |
| Vladimir | Parser  -- non-protectable elements, abbreviations, `mark_disclaimer`; tests |

### Week 4 (May 22–31)

| Owner | Task |
|-------|------|
| Daria | End-of-May demo; retro; draft June plan; consolidate docs |
| Daniel | Finalize test dataset; module docs for metrics and datasets |
| Alex | Full fine-tune if GPU available, else document gap; visual model docs |
| Ilya | Finalize architecture docs; June architecture plan |
| Vladimir | Parser edge-case coverage against the agreed list; CI and quality status report |

## Risks

| Risk | Probability | Impact | Owner | Mitigation |
|------|-------------|--------|-------|------------|
| GPU environment delayed | High | High | Daria | Escalate early; use any available hardware for prototyping; delay only full fine-tune, not other goals |
| Legal sign-off slips | Medium | High | Daria | Book session in week 1 with a concrete draft |
| Label disagreement too high to trust dataset | Medium | Medium | Daniel | Start with a small control set; refine guidelines with legal before full labeling |
| Parser edge-case list grows beyond what fits in May | Medium | Medium | Vladimir | Freeze the list end of week 2; extras move to June |

## Exit Criteria

May is closed when G1–G4 are met and the GPU environment is either provisioned or the escalation path is clear. If the visual model cannot be fine-tuned in May due to hardware, G3 is considered met at the "ready to train" stage and full training moves to the first week of June.
