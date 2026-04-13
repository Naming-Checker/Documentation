# MoSCoW

## Must Have

### M1. Logo visual similarity model (image-to-image)
- Develop a model to compare two logo images.
- Input: two images; output: visual similarity percentage.
- Criteria from requirements: overall visual impression, color/color combination, shape, composition.
- Support combined marks (visual + text element).
- Local model only (no external calls, internal MTS network requirement).
- Priority #1 per stakeholder direction.

### M2. Preprocessing of text naming records from the database
- Parse and normalize "dirty" naming fields (extract clean naming from descriptive text).
- Remove digits and numbers without distinctive graphic execution.
- Remove common abbreviations (OJSC, LLC, Ltd, GmbH, etc.).
- Use `mark_disclaimer` to remove non-protectable elements.
- Remove generic product/service descriptors (generic and category terms).

### M3. Phonetic (sound) similarity for text namings
- Implement a model/algorithm for phonetic comparison.
- Requirements criteria: matching sounds, sound proximity, position of sound clusters, matching syllables, syllable count, vowel/consonant composition, containment of one mark in another, stress.
- Handle transliteration (Cyrillic <-> Latin).
- Handle spelling distortions (ELLASTIC -> ELASTIC).

### M4. Semantic (meaning) similarity for text namings
- Implement a model/algorithm for semantic comparison.
- Criteria: similarity of concepts/ideas, cross-language meaning alignment, matching key element with independent meaning.
- Account for opposite concepts.
- Account for cases where same-root words with different meanings are not similar.

### M5. Text similarity metrics
- Implement string-based text similarity metrics.
- Account for prefix containment (PROBI -> PROBIMAX).

### M6. Final similarity score formula (text naming)
- Combine phonetic, semantic, and text similarity into a single percentage.
- Final formula is determined from testing results.

### M7. Trademark database search
- Filter by Nice classes (MKTU).
- Return top-200 most similar namings with similarity percentage.

### M8. Infringement check (text)
- Compare naming with one target text naming -> similarity percentage.

### M9. Infringement check (logo)
- Compare existing logo with potential infringement -> visual similarity percentage.
- Uses model from M1.

### M10. Quality metric formalization and test dataset creation
- Define what is considered "similarity": align with experts (legal team) on positive and negative pairs.
- Build labeled test dataset: naming pairs and logo pairs with expert labels (similar / not similar / borderline).
- Define metrics: accuracy, precision, recall, F1, and target thresholds.
- Define what is included in "top-200 output" and how correct-match share is measured.
- Use this dataset throughout the project to validate each module.

### M11. External web interface for users
- Minimal UI for result delivery.

### M12. Non-functional requirements
- Accuracy >= x% (final definition based on M10).
- Response time < 2 minutes.
- Deployment on NVIDIA A100 PCIe 80GB GPU.
- All models must be local, with no external internet calls.
- Docker containerization.

## Should Have

### S1. Search across internet sources (product names, tariffs, works)
- Parse registries: RAO (Russian and international rights holders), Ministry of Culture (films), Roskomnadzor (media).
- Search across: Yandex Video, Yandex Music, Kinopoisk, YouTube, Rutube, Google Books, Yandex Search.
- Aggregate into a single top-200 most relevant match list.

### S2. Graphic similarity of word marks (text as image)
- Account for font type and letter case (uppercase/lowercase, print/cursive).
- Account for character placement, alphabet, and color.
- Account for cases where original text styling turns word marks into figurative marks.

## Could Have

### C1. Extended preprocessing for edge cases
- Handle complex cases: neologisms, compound words, metaphorical namings.
- Filter descriptive non-distinctive elements from broader context (not only from `mark_disclaimer`).

## Won't Have (not in current iteration)

### W1. Output of explicit trademark violation determinations

## Implementation Order (recommended)

| Stage | Tasks | Rationale |
|------|--------|-------------|
| 1 | M1 (logo visual similarity) + M10 (test dataset and metrics) | Stakeholder priority + quality cannot be validated without test baseline |
| 2 | M2 (data preprocessing) | Blocks all text similarity modules |
| 3 | M3, M4, M5 (phonetics, semantics, text metrics) | Core text similarity stack, can be parallelized |
| 4 | M6 (final formula) | Depends on stage 3 outputs |
| 5 | M7, M8, M9 (DB search, text/logo infringement checks) | Integration of models with data and API |
| 6 | M11 (web interface) | Minimal UI for result delivery |
| 7 | M12 (non-functional requirements, Docker, GPU) | Final deployment hardening |
| 8 | S1 (internet source parsing) | Coverage expansion |
| 9 | S2 (graphic similarity for word marks) | Text similarity enhancement |
| 10 | C1 (extended preprocessing edge cases) | Quality improvement |
