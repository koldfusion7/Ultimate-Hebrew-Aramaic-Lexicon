# Ultimate Hebrew-Aramaic Lexicon

## Status

Planning and architecture phase.

This repository is the canonical design and implementation workspace for the Ultimate Hebrew-Aramaic Lexicon project. The current priority is to design the system correctly before scaling it onto a VPS or other production infrastructure.

## Project Vision

The Ultimate Hebrew-Aramaic Lexicon is intended to become a deep lexical, textual, and analytical foundation for Hebrew and Aramaic research, exploration, and downstream application development.

This project is not meant to be only a dictionary. It is meant to become a structured language intelligence system that can support:

- lexicon and concordance work
- morphology and root analysis
- wordform and lemma relationships
- source-aware text processing
- gematria calculations across multiple methods
- Milui and expanded spelling analysis
- letter transformation and substitution methods
- robust search and cross-linking
- future developer APIs and end-user tools

The long-term goal is to build a stable, extensible backbone for a family of tools that depend on a serious Hebrew-Aramaic language database.

## Core Principles

1. Architecture before infrastructure.
2. Stable schema before large-scale ingestion.
3. Canonical source data must remain distinct from derived data.
4. Every transformation must be traceable and reproducible.
5. Ambiguity must be preserved rather than flattened away.
6. The system must support reruns, checkpoints, and provenance.
7. The schema should be designed for long-term downstream reuse.
8. PostgreSQL is the canonical relational backend.
9. Full-text, analytical, and possibly vector-oriented derivatives may be added later, but not at the cost of relational clarity.
10. The VPS is a deployment target, not the place where architecture gets invented.

## What This Repository Will Contain

This repository is expected to hold the following major project assets:

1. Master architecture documents
2. Schema blueprints
3. SQL migrations
4. ETL and data pipeline scripts
5. Validation and auditing scripts
6. Reference tables for gematria, Milui, and transformation methods
7. Fixture datasets for local testing
8. Developer documentation
9. Roadmaps and implementation notes
10. Eventually, selected services, APIs, or interface layers built on the lexicon core

## Scope

### In Scope

- Hebrew and Aramaic textual ingestion design
- canonical text hierarchy modeling
- tokenization and segmentation
- lexical and root-layer modeling
- morphology analysis structures
- gematria method modeling and computation
- Milui spelling systems and expansions
- transformation and cipher mapping tables
- ETL run tracking, provenance, and validation
- developer-facing documentation and repeatable pipelines

### Out of Scope for the Initial Build Phase

- premature VPS provisioning as the main place of development
- ad hoc schema drift during ingestion
- production UI polish before the backend foundation exists
- overcommitting to a single front-end product before the language core is stable
- trying to solve every downstream app problem before the lexicon backbone is sound

## High-Level System Goals

1. Build a canonical relational schema for Hebrew-Aramaic lexical and textual analysis.
2. Build repeatable ingestion and processing pipelines.
3. Support multiple source traditions, editions, and text versions.
4. Preserve original text while enabling normalized and derived representations.
5. Support multiple analytical layers without destroying provenance.
6. Make the system useful both for scholarship and for application development.
7. Keep the design stable enough that dependent apps do not break every time the ETL evolves.

## Architectural Approach

The project is being approached in four major layers.

### 1. Canonical Source Layer

This layer stores source metadata and raw or minimally transformed text tied to editions and text versions.

Examples:
- source registries
- works and editions
- raw text content
- structural hierarchy such as book, chapter, verse, folio, line, segment

### 2. Normalized Text Layer

This layer stores normalization outputs while preserving links to the canonical source text.

Examples:
- normalization profiles
- normalization rules
- normalized text content
- token boundaries tied to normalized views

### 3. Analytical Layer

This layer stores linguistic and derived analyses.

Examples:
- tokens
- orthographic features
- lemma candidates
- root candidates
- morphology analyses
- confidence and source attribution

### 4. Computational and Derived Layer

This layer stores computational outputs and operational metadata.

Examples:
- gematria values by method
- Milui expansions
- transformed forms
- ETL runs and checkpoints
- validation reports
- index build metadata

## Planned Schema Modules

The schema will likely be grouped into the following modules.

### A. Source and Registry
- `sources`
- `source_editions`
- `works`
- `text_versions`
- `licenses`

### B. Structural Hierarchy
- `text_units`
- `text_unit_types`
- `text_unit_links`

### C. Raw and Normalized Text
- `raw_text_content`
- `normalized_text_content`
- `normalization_profiles`
- `normalization_rules`

### D. Token Layer
- `tokens`
- `token_boundaries`
- `token_features`
- `orthographic_profiles`

### E. Lexical Layer
- `lemmas`
- `lemma_forms`
- `roots`
- `languages`
- `parts_of_speech`

### F. Analysis Layer
- `token_lemma_candidates`
- `token_root_candidates`
- `morphology_analyses`
- `analysis_sources`
- `confidence_scores`

### G. Gematria Layer
- `gematria_methods`
- `gematria_method_variants`
- `token_gematria_values`
- `lemma_gematria_values`
- `root_gematria_values`

### H. Milui Layer
- `milui_methods`
- `hebrew_letters`
- `letter_milui_spellings`
- `expanded_spellings`
- `expanded_spelling_components`

### I. Transform and Cipher Layer
- `letter_transform_methods`
- `transform_mappings`
- `transformed_forms`

### J. Provenance and Operations
- `etl_runs`
- `etl_run_steps`
- `etl_artifacts`
- `validation_results`
- `error_logs`
- `checkpoints`

These names are subject to refinement during schema design, but the repository will be organized around these conceptual modules from the start.

## Planned Processing Pipeline

The intended ETL flow is:

1. Register source and edition metadata.
2. Ingest raw text.
3. Normalize text using explicit rule sets.
4. Segment text into structural units.
5. Tokenize text.
6. Attach orthographic metadata.
7. Attach lexical candidates.
8. Attach root candidates.
9. Attach morphology analyses.
10. Compute gematria values.
11. Compute Milui expansions.
12. Compute letter-transform derivatives where needed.
13. Build indexes and materialized outputs.
14. Run validation and audit checks.

Every stage should be restartable, inspectable, and attributable.

## Why Architecture-First Matters

A major project risk is trying to design schema, ETL logic, and infrastructure all at the same time. That creates chaos.

This project deliberately avoids that trap by following this order:

1. Architecture
2. Schema
3. Migrations
4. Script contracts
5. Test fixtures
6. Local dry runs
7. Infrastructure provisioning
8. Full-scale processing

This is a foundational project. Getting the structure right matters more than pretending to move fast.

## Repository Structure

The initial repository structure is expected to evolve toward something like this:

```text
Ultimate-Hebrew-Aramaic-Lexicon/
├── README.md
├── docs/
│   ├── architecture/
│   ├── schema/
│   ├── roadmap/
│   └── references/
├── migrations/
│   ├── sql/
│   └── seeds/
├── src/
│   ├── core/
│   ├── etl/
│   ├── loaders/
│   ├── analyzers/
│   ├── gematria/
│   ├── milui/
│   ├── transforms/
│   └── validation/
├── scripts/
├── tests/
│   ├── fixtures/
│   ├── unit/
│   └── integration/
├── config/
└── data/
    ├── fixtures/
    └── reference/
```

This structure may change as implementation becomes clearer, but the project will remain organized around documents, schema, ETL, validation, and reusable reference data.

## Planned Script Inventory

The initial codebase will likely include scripts such as:

- `config.py`
- `db.py`
- `logging_setup.py`
- `register_sources.py`
- `ingest_texts.py`
- `normalize_texts.py`
- `segment_texts.py`
- `tokenize_texts.py`
- `extract_orthography.py`
- `attach_lemma_candidates.py`
- `attach_root_candidates.py`
- `attach_morphology.py`
- `load_gematria_methods.py`
- `load_milui_methods.py`
- `compute_gematria.py`
- `compute_milui_expansions.py`
- `compute_letter_transforms.py`
- `validate_dataset.py`
- `build_indexes.py`
- `run_pipeline.py`

Each script should eventually document:

1. inputs
2. outputs
3. tables touched
4. rerun safety
5. checkpoint support
6. validation behavior
7. failure behavior

## Data Sources

The project is expected to draw from multiple textual and lexical sources over time. Initial work is especially concerned with designing a system flexible enough to ingest and reconcile multiple source traditions and export sets without collapsing them into a single simplistic representation.

Source integration strategy will be documented separately in `docs/architecture/` and `docs/references/`.

## Development Strategy

### Phase 1: Design
- define the conceptual model
- freeze a first-pass schema blueprint
- define ID strategy and table boundaries
- define what is canonical versus derived

### Phase 2: Migration Foundation
- write SQL migrations
- seed reference tables
- establish naming conventions and constraints

### Phase 3: ETL Skeleton
- build script scaffolds
- define contracts between stages
- implement config and logging

### Phase 4: Fixture Testing
- create a tiny but representative corpus
- test ingestion, normalization, tokenization, and derived calculations
- verify idempotency and checkpoint behavior

### Phase 5: Infrastructure and Scale
- provision or reconfigure VPS only after the previous steps succeed
- run the full corpus through a stable pipeline
- optimize performance after correctness is established

## Development Environment

The repository is being designed so that work can begin locally before any production server is involved.

Planned assumptions:

- Python for orchestration and ETL
- PostgreSQL as the canonical SQL database
- SQL migrations stored in-repo
- environment-variable driven configuration
- local fixture datasets for repeatable testing

A formal local setup guide will be added once the first implementation files exist.

## Initial Priorities

The next major deliverables for this repository are:

1. a detailed architecture document
2. a canonical schema blueprint
3. an initial migration plan
4. a codebase folder skeleton
5. script stubs for the early ETL phases
6. reference tables for gematria and Milui methods

## Non-Negotiable Design Rules

1. Do not treat the VPS as the place where the architecture is figured out.
2. Do not flatten ambiguous morphology into fake certainty.
3. Do not overwrite source text with normalized or derived representations.
4. Do not let schema drift because a quick hack seems convenient.
5. Do not build dependent apps on unstable table structures.
6. Do not skip provenance.
7. Do not compute derived data without method attribution.
8. Do not proceed to large-scale ingestion before local fixture runs succeed.

## Intended Audience

This repository is for:

- the project owner
- human developers contributing to the lexicon core
- AI coding assistants and agentic workflows
- future downstream application developers
- researchers who need to understand the architecture and data model

## Collaboration Guidance

Contributors should favor:

- explicit design over vague intention
- exact file contents over hand-waving
- migrations over undocumented schema changes
- reproducible ETL over one-off scripts
- durable documentation over chat-only decisions

When in doubt, document the design decision in-repo.

## Roadmap Snapshot

Short-term:

1. initialize repository documentation
2. define architecture documents
3. define schema modules and identifiers
4. write first migration set
5. build ETL skeletons

Medium-term:

1. ingest a controlled fixture corpus
2. validate tokenization and morphology structures
3. load gematria and Milui reference systems
4. test end-to-end pipeline locally

Long-term:

1. ingest broader corpora
2. optimize search and retrieval
3. expose service layers or APIs
4. support downstream applications built on the lexicon core

## License and Usage

License selection is still pending and will depend on the mix of original code, reference tables, and incorporated source data. Until a project license is explicitly added, assume that rights and reuse constraints remain under active review.

## Current Repository State

This repository is intentionally starting from a clean slate.

That is not a lack of progress. It is a deliberate choice to build the foundation in the right order.

## Summary

The Ultimate Hebrew-Aramaic Lexicon is being built as a serious language infrastructure project.

The immediate task is not to rush into server setup or premature scale. The immediate task is to define the architecture, schema, migrations, and script boundaries clearly enough that everything built afterward rests on a stable foundation.

If this repository is maintained with that discipline, it can become the backbone for a large family of Hebrew-Aramaic tools rather than another fragile prototype.
