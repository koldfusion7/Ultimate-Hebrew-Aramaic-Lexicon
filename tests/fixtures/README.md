# Fixture Datasets

This directory will hold small, representative datasets used for local and integration testing.

## Purpose

The project should not jump directly from abstract design to full-scale corpus processing.

A controlled fixture corpus is necessary to verify:

- ingestion behavior
- normalization logic
- segmentation
- tokenization
- analysis-layer joins
- gematria calculations
- Milui expansions
- rerun behavior
- checkpoint behavior

## Desired Fixture Properties

The early fixture corpus should include:

- Hebrew prose
- Hebrew poetry
- Aramaic material
- orthographic variation cases
- prefix and suffix complexity
- ambiguous tokenization cases
- enough diversity to expose schema mistakes early

## Rule

No large-scale ingest should begin until the fixture corpus can be processed locally with predictable results.
