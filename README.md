# Market Data Digest

Six-month performance snapshot for the investment club's three holdings, generated from Yahoo Finance daily price history.

## Data window

- **Start:** 2026-04-23
- **End:** 2026-10-21
- **Interval:** daily (trading days only)
- **Trading days per ticker:** 126
- **Source:** Yahoo Finance daily close history (six months)

## Tickers

- **AAPL** — Apple Inc.
- **MSFT** — Microsoft Corporation
- **NVDA** — NVIDIA Corporation

## Files

- `digest.csv` — the summary metrics, one row per ticker, rows sorted alphabetically by ticker.
- `price_history.csv` — the underlying daily closing price series (378 rows) used to compute the summary.

## Metric definitions

`digest.csv` has the header `ticker,avg_close,max_close,min_close,pct_change`:

- **ticker** — the stock symbol (AAPL, MSFT or NVDA).
- **avg_close** — the arithmetic mean of every daily closing price in the six-month window, rounded to two decimals.
- **max_close** — the highest daily closing price observed anywhere in the window, rounded to two decimals.
- **min_close** — the lowest daily closing price observed anywhere in the window, rounded to two decimals.
- **pct_change** — percentage change from the first close in the window to the last close in the window, computed as `(last_close − first_close) / first_close × 100`, expressed as a plain number rounded to two decimals (so 26.03 means +26.03%).

All four metrics are computed from the retrieved price history in a sandboxed shell (not by hand). Closes are the daily closing prices as returned by the Yahoo Finance daily history feed; rows containing null closes (e.g. an in-progress current trading day) are excluded.

## Validation

`.github/workflows/digest-ci.yml` defines a single job named `validate` that runs on manual trigger (`workflow_dispatch`). It fails if the first line of `digest.csv` is not the expected header `ticker,avg_close,max_close,min_close,pct_change`.

The full CSV is also pasted into issue #1 ("Weekly digest review") for club discussion.
