# Schema Blueprint

## Purpose

This document provides the first-pass conceptual schema blueprint for the Ultimate Hebrew-Aramaic Lexicon.

It is not yet the final migration specification. Its purpose is to define module boundaries, entity responsibilities, and the major relationships that will later become SQL migrations.

## Guiding Rules

1. Canonical source data must be separated from derived data.
2. Every analysis must be attributable to a method or source.
3. Text versioning must be explicit.
4. The schema must preserve ambiguity where analysis is uncertain.
5. Wide, brittle tables should be avoided in favor of modular relational design.

## Core Modules

### A. Source Registry
Stores source-level metadata.

Planned entities:
- `sources`
- `source_editions`
- `works`
- `text_versions`
- `licenses`

### B. Text Structure
Stores the hierarchy of textual units.

Planned entities:
- `text_unit_types`
- `text_units`
- `text_unit_links`

This must support structures such as:
- book
- chapter
- verse
- folio
- line
- paragraph
- segment

### C. Text Content
Stores raw and normalized text.

Planned entities:
- `raw_text_content`
- `normalized_text_content`
- `normalization_profiles`
- `normalization_rules`

### D. Token Layer
Stores tokenization boundaries and token-level features.

Planned entities:
- `tokens`
- `token_boundaries`
- `token_features`
- `orthographic_profiles`

### E. Lexical Layer
Stores lemma, root, language, and part-of-speech metadata.

Planned entities:
- `lemmas`
- `lemma_forms`
- `roots`
- `languages`
- `parts_of_speech`

### F. Analysis Layer
Stores token-to-lemma, token-to-root, and morphology analysis outputs.

Planned entities:
- `token_lemma_candidates`
- `token_root_candidates`
- `morphology_analyses`
- `analysis_sources`
- `confidence_scores`

### G. Gematria Layer
Stores method definitions and calculated outputs.

Planned entities:
- `gematria_methods`
- `gematria_method_variants`
- `token_gematria_values`
- `lemma_gematria_values`
- `root_gematria_values`

### H. Milui Layer
Stores letter expansions and spelling systems.

Planned entities:
- `milui_methods`
- `hebrew_letters`
- `letter_milui_spellings`
- `expanded_spellings`
- `expanded_spelling_components`

### I. Transform Layer
Stores substitution and transform methods such as letter mappings.

Planned entities:
- `letter_transform_methods`
- `transform_mappings`
- `transformed_forms`

### J. Operations and Provenance
Stores ETL control, validation, and audit metadata.

Planned entities:
- `etl_runs`
- `etl_run_steps`
- `etl_artifacts`
- `validation_results`
- `error_logs`
- `checkpoints`

## Key Open Questions

These questions must be answered before migration drafting is finalized.

1. What is the canonical ID strategy for text units, tokens, lemmas, and roots?
2. Should tokens belong directly to text versions, or be modeled through a separate bridge?
3. How should ranked morphology candidates be stored and queried?
4. Which entities must be immutable after ingest?
5. Which derived outputs are recomputable and should not be treated as canonical?
6. How should Hebrew and Aramaic divergences be modeled cleanly without fragmenting the schema?

## Draft Migration Order

The likely migration order is:

1. source registry
2. text structure
3. text content
4. token layer
5. lexical layer
6. analysis layer
7. gematria layer
8. Milui layer
9. transform layer
10. provenance and ETL operations

## Immediate Deliverable After This Document

The next step is to turn this conceptual blueprint into a table-by-table design document with:

- primary keys
- foreign keys
- uniqueness rules
- enum/reference tables
- indexing strategy
- mutability rules
