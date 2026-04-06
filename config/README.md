# Configuration

This directory will contain project configuration templates and environment guidance.

## Planned Contents

- environment variable templates
- database connection guidance
- local development config examples
- pipeline execution profiles

## Configuration Principles

1. Environment-variable driven configuration should be preferred.
2. Missing required configuration should fail loudly.
3. Local and production settings should be separable.
4. Config should support repeatable ETL execution rather than one-off shell hacks.
