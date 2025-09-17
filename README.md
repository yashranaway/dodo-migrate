# dodo-migrate

A CLI-first migration toolkit to help teams move from other payment providers or MoR platforms (e.g., LemonSqueezy, Gumroad, 2Checkout, FastSpring, Stripe, Paddle) into Dodo Payments. Focused on safety, auditability, and repeatable runs.

## Status

Scaffold only. Implementation intentionally omitted.

## Goals

- Safe, idempotent migrations you can re-run
- Clear data model for customers, products, subscriptions, invoices, payments, coupons, payouts
- Provider adapters that read/export normalized data
- Deterministic transforms to Dodo’s model
- Dry-run planning and human-readable reports
- Rich logs and CSV/JSON artifacts for auditing

## High-level Flow

1. Import: pull data from a provider API or exported files
2. Transform: normalize to Dodo’s canonical schema
3. Validate: run strict schema + referential integrity checks
4. Plan: compute a migration plan with diffs
5. Export: emit Dodo-ready artifacts (JSONL/CSV) or call Dodo APIs (future)

## Migration Scope (supported data)

- Products
- License Keys
- Associated Files
- Discount Codes
- Customers

## Repository Structure

```
src/
  cli/                # CLI entrypoints and commands
  adapters/           # Provider-specific import logic (no secrets committed)
    lemonsqueezy/
    gumroad/
    stripe/
    paddle/
    fastspring/
    2checkout/
    generic-csv/      # Simple CSV-based migration for custom sources
  models/             # Canonical TypeScript interfaces for entities
  services/           # Provider-agnostic domain services
  validators/         # Zod/Valibot schemas and integrity checks
  utils/              # Shared helpers
  importers/          # Pull & stage raw provider data
  transformers/       # Convert raw -> canonical models
  exporters/
    dodo/             # Emit Dodo-compatible artifacts (JSONL/CSV)

docs/
  providers/          # Per-provider notes, mappings, gotchas
examples/             # Sample configs and input data layouts
scripts/              # One-off maintenance and generation scripts
tests/                # Unit/integration tests
```

## Roadmap (scaffold)

- CLI: `dodo-migrate import --provider stripe`, `... plan`, `... export`
- Config: `dodo-migrate.config.(json|ts)` with auth and selection filters
- Providers: Stripe, Paddle, LemonSqueezy, FastSpring, Gumroad, 2Checkout
- Artifacts: write JSONL to `./.dodo-migrate/artifacts` with run-id naming
- Reports: markdown/CSV summaries for diffs and conflicts
- Safety: dry-run by default; explicit `--apply` later

## Getting Started (future)

```bash
# Install
npm i -g dodo-migrate  # or use npx once published

# Example: import from Stripe, then plan and export
dodo-migrate import --provider stripe --since 2022-01-01 --out ./.dodo-migrate
dodo-migrate plan --out ./.dodo-migrate
dodo-migrate export --target dodo --out ./.dodo-migrate
```

## Provider Docs

See docs in `docs/providers`:
- Stripe: data model and object mapping
- Paddle: subscription and price mapping
- LemonSqueezy: customers/orders/subscriptions parity
- FastSpring: events to invoices alignment
- Gumroad: historical sales and refunds format
- 2Checkout: legacy fields and status mapping
- Generic CSV: column expectations

## Contributing

- Keep provider adapters side-effect free; pure import/transform functions
- Prefer interfaces over types; avoid enums (use maps)
- No secrets in code or examples; use environment variables
- Add examples that reflect real edge cases (voids, proration, coupons, trials)

## License

Apache-2.0 (TBD)
