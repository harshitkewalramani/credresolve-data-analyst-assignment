# CredResolve — Technical Analysis Pack

This pack is the technical assembly layer for the CredResolve Data Analyst assignment.

## Dialect
SQL is written in **DuckDB SQL** and uses relative paths, so the repository can be rerun from the project root.

## Data source
The materialized Golden Dataset V2 package is the source of truth for downstream tables. Raw snapshots are retained under `raw_snapshot/` for audit/reproducibility.

## Query folders
- `01_raw_audit` — raw inventory / sanity checks
- `02_staging` — staging contract pattern
- `03_clean` — duplicate and cleaning checks
- `04_golden` — Golden reconciliation and key rules
- `05_metrics` — locked metrics and attribution-based channel conversion
- `06_forensics` — data-integrity investigations
- `07_driver_analysis` — Feb→Mar operational/DPD analysis
- `08_counterfactual` — identifiability statement for targeting counterfactual

## Important conventions
- `account_id` is the strongest provisional analytical spine.
- `borrower_id` and `agent_id` are unresolved/non-canonical.
- `payment_reference` is never a deduplication key.
- Strict Golden payment facts quarantine conflicting `payment_id`s.
- `feature/recovery_payment_base_v1.csv` is an explicit, versioned analytical convention that reproduces the locked Feb→Mar gross recovery result without contaminating strict Golden truth.
- `channel_conversion_v2` = mutually-exclusive first-touch, touch-before-payment, 7-day window.
- `campaign_attribution_v1` = 30-day campaign-touch attribution convention.
- Current `outstanding_amount` is not historical balance truth.

## Run
From the repository root, use DuckDB CLI or Python DuckDB integration to execute `.sql` files. The queries are designed for read-only analysis of the materialized package.
