# Tebaro Calibration Coefficient — Public Methodology

## Purpose

The Tebaro coefficient is a **dimensionless calibration parameter** intended for product-pricing conversion software. It is not a per-currency exchange quotation.

## Current method identifier

`median_of_currency_ratios_v1`

## Processing model

1. Private eligible observations are normalized into Toman units.
2. Corresponding official-reference observations are kept in Rial units.
3. For each supported currency with valid same-run inputs, the ratio is calculated as:

   `ratio = market_toman × 10 / official_reference_rial`

4. Inputs and ratios must be numeric, finite, positive, and within documented sanity bounds.
5. Cross-currency outliers are rejected using robust comparison against the same-run median.
6. A minimum quorum of **3 valid currencies** is required for the current method.
7. The final coefficient is the median of the accepted currency ratios.
8. The public scalar is rounded to a bounded precision (currently up to 6 decimal places).
9. A recent last-known-good coefficient is used only as a safety anchor. A suspicious jump greater than the configured safety threshold (currently 25%) is rejected rather than automatically replacing the last-known-good output.
10. If acquisition, validation, quorum, or safety checks fail, no new coefficient is published and the last-known-good public value remains unchanged when available.

## Freshness metadata

A successful publication includes:

- `generated_at`: UTC generation time;
- `valid_until`: UTC expiry time;
- `sample_count`: number of accepted current-method observations contributing to the published result;
- `status`: currently `ok` for a publishable payload.

The current publisher normally uses a 24-hour validity window. Consumers may apply stricter local freshness rules.

## Public payload contract

Schema version 1 contains exactly these top-level fields:

- `schema_version`
- `coefficient`
- `generated_at`
- `valid_until`
- `method`
- `sample_count`
- `status`

The public payload intentionally excludes raw rates, per-currency values, provider identities, provider URLs, and scrape logs.

## Limitations

A robust median reduces sensitivity to isolated bad inputs but does not make the coefficient an authoritative market measure. Different currencies and market contexts can exhibit different spreads. The methodology is designed for bounded software calibration, not for trading, settlement, remittance, investment, or financial advice.

Method changes that alter semantics should use a new method identifier and, where the payload contract changes, a new schema version.
