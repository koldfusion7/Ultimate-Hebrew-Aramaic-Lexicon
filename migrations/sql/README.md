# SQL Migrations

This directory will contain the canonical SQL migration files for the Ultimate Hebrew-Aramaic Lexicon project.

## Purpose

The migration layer must become the authoritative history of relational schema evolution.

Schema changes should not live only in chat, ad hoc terminal commands, or undocumented local experiments.

## Expected Contents

This directory will eventually contain:

- initial core schema migrations
- later schema extension migrations
- reference table seed support where appropriate
- rollback notes when needed

## Planned Migration Order

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

## Migration Rules

1. Prefer additive, explicit migrations.
2. Avoid undocumented schema mutation.
3. Keep table naming and constraints consistent.
4. Preserve provenance-related structures from the beginning.
5. Do not let temporary scripting convenience dictate schema shape.
