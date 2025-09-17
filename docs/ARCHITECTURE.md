# Architecture (scaffold)

This document outlines the intended architecture. No implementation yet.

## Modules

- `src/cli`: command definitions and argument parsing
- `src/importers`: provider ingestion (API, webhooks dump, file exports)
- `src/transformers`: raw provider -> canonical models
- `src/validators`: schema validation and referential checks
- `src/exporters/dodo`: emit artifacts for Dodo (JSONL/CSV)
- `src/services`: cross-cutting domain logic
- `src/models`: canonical entity interfaces

## Canonical Entities (initial)

- Customer, Product, Price, Subscription, Invoice, Payment, Refund, Coupon, Payout

## Run Directory

Each run writes to `./.dodo-migrate/<run-id>/`:

```
.dodo-migrate/
  <run-id>/
    raw/            # Provider raw payloads
    normalized/     # Canonical models JSONL
    reports/        # Markdown/CSV summaries
    artifacts/      # Dodo-ready exports
    logs/           # Structured logs
```

## Idempotency

- Deterministic transforms and stable IDs (e.g., provider_id → canonical_id mapping)
- Content-addressed files where possible
- Re-run safe: same inputs produce identical outputs

## Config (future)

- `dodo-migrate.config.(json|ts)`
- Auth per provider via env vars
- Filters: date ranges, object types, org scoping
- Output directory and concurrency tuning

## Testing Strategy

- Unit tests for transformers and validators
- Golden files for JSONL outputs
- Provider fixtures redacted and anonymized
