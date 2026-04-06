# ETL Layer

This directory will contain the extract-transform-load pipeline code for the Ultimate Hebrew-Aramaic Lexicon.

## Purpose

The ETL layer is responsible for moving the project from source data to structured relational data in a repeatable, auditable way.

## Expected Responsibilities

- source registration
- raw text ingest
- normalization
- segmentation
- tokenization
- orthographic feature extraction
- lemma and root candidate attachment
- morphology analysis attachment
- gematria and Milui calculation stages
- validation and checkpoint-aware reruns

## Planned Early Scripts

- `register_sources.py`
- `ingest_texts.py`
- `normalize_texts.py`
- `segment_texts.py`
- `tokenize_texts.py`
- `extract_orthography.py`
- `attach_lemma_candidates.py`
- `attach_root_candidates.py`
- `attach_morphology.py`
- `compute_gematria.py`
- `compute_milui_expansions.py`
- `compute_letter_transforms.py`
- `validate_dataset.py`
- `run_pipeline.py`

## Operational Rules

1. Each stage should declare its inputs and outputs.
2. Each stage should document the tables it touches.
3. Long-running stages should support chunking where practical.
4. Reruns should be safe or explicitly guarded.
5. ETL metadata should be recorded for every meaningful run.
