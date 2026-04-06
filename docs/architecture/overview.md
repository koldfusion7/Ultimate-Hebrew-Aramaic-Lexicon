# Architecture Overview

## Purpose

This document defines the high-level architectural direction for the Ultimate Hebrew-Aramaic Lexicon.

The project is being designed as a durable language infrastructure system rather than a one-off script collection or a thin dictionary wrapper. The architecture must support accurate source tracking, repeatable ETL, layered analysis, and downstream reuse by future applications.

## Primary Architectural Goal

Build a stable relational backbone for Hebrew and Aramaic textual, lexical, and analytical data, while preserving the distinction between:

1. source truth
2. normalized representations
3. analytical outputs
4. computational derivatives
5. operational metadata

## Strategic Constraint

The project must be designed before being scaled.

The VPS or cloud server is not the place where schema, ETL logic, and data contracts are invented. Infrastructure should come after the architecture is defined well enough to support predictable execution.

## Architectural Model

The system is divided into four major layers.

### 1. Canonical Source Layer

This layer contains the source-facing entities that preserve provenance and edition specificity.

Examples:
- source registries
- works
- editions
- text versions
- raw text content
- text hierarchy metadata

### 2. Normalization Layer

This layer stores normalized or transformed textual views without overwriting the source form.

Examples:
- normalization profiles
- normalization rules
- normalized text content
- normalization audit metadata

### 3. Linguistic Analysis Layer

This layer contains token, lexical, and morphology-related analyses.

Examples:
- tokens
- token boundaries
- orthographic features
- lemma candidates
- root candidates
- morphology analyses
- confidence and attribution

### 4. Computational and Operational Layer

This layer contains derived calculations and ETL control metadata.

Examples:
- gematria values
- Milui expansions
- letter-transform outputs
- ETL runs
- checkpoints
- validation results
- error logs

## Design Priorities

### Preserve Provenance
Every derived value must be traceable back to a specific source, edition, text version, and processing method.

### Preserve Ambiguity
Where multiple analyses are possible, the schema should preserve ranked or attributed candidates instead of flattening uncertainty into a single fake certainty.

### Preserve Reproducibility
Derived outputs should be tied to method definitions and pipeline stages so that recomputation is possible and auditable.

### Preserve Stability
Downstream applications will depend on the lexicon core. The schema should therefore be designed for durability and careful evolution.

## Repository Role

This repository exists to hold:

- architecture documents
- schema blueprints
- migration files
- ETL script scaffolds
- validation logic
- reference tables
- test fixtures

It is the canonical design and implementation workspace for the project.

## Immediate Next Steps

1. finalize the first-pass conceptual schema
2. separate canonical and derived entities clearly
3. define table modules and identifiers
4. write the first migration plan
5. create ETL scaffolds in execution order

## Non-Negotiable Rules

1. Do not overwrite source text with normalized text.
2. Do not store derived data without method attribution.
3. Do not allow architecture drift because of short-term scripting convenience.
4. Do not treat the server as the primary design environment.
5. Do not move into large-scale ingestion until local fixture runs succeed.
