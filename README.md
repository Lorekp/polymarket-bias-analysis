# Polymarket Bias & Mispricing Analysis

An exploratory research report on calibration and pricing patterns in closed Polymarket binary markets. It compares quoted probabilities with resolved outcomes, examines differences across market categories and liquidity levels, and illustrates how historical patterns change under simplified transaction costs.

[Read the published report](https://lorekp.github.io/polymarket-bias-analysis/).

## What is included

The repository publishes a rendered HTML report, attributed to Laurence and dated February 19, 2026. Its embedded **R** code and saved outputs cover:

- Parsing binary Yes/No resolutions and mapping outcome tokens.
- Sampling historical prices at six horizons from one hour to one month before recorded closure.
- Calibration curves, Brier scores, favorite–longshot patterns, and category comparisons.
- Volume filters, monthly persistence, percentile bootstrap confidence intervals, and illustrative Kelly sizing.
- A retrospective P&L simulation and proposed bot implementation notes.

The saved report starts with 111,178 market rows and retains 49,753 clean binary Yes/No resolutions. These are reported dataset counts, not independently reproduced results. Although the title refers to 2025, the displayed quarterly analysis includes 2024 observations.

## Read locally

Download or clone this repository and open `index.html` in a browser. No Python installation, package installation, or analysis execution is required to read the saved report. Use its **Code** menu to show or hide the embedded R chunks.

| File | Purpose |
| --- | --- |
| `index.html` | Rendered report, analysis code, figures, and saved output |
| `.github/workflows/pages.yml` | Publishes the repository to GitHub Pages on pushes to `main` or manual dispatch |
| `.nojekyll` | Disables Jekyll processing |

There is no application server or implemented trading bot in this repository.

## Reproducing the analysis

The published snapshot does not include the original R Markdown source, standalone analysis scripts, data collection pipeline, dependency lockfile, tests, or input data. It therefore provides no supported one-command analysis rebuild.

The embedded code expects two external Parquet inputs:

- `markets_2025_closed.parquet`: market metadata including IDs, closure status and time, JSON outcome/pricing/token lists, tags, titles, and volume.
- `markets_2025_closed_price_history.parquet`: historical `token_id`, `timestamp`, and `price` records.

The displayed analysis uses R packages `arrow`, `dplyr`, `tidyr`, `stringr`, `ggplot2`, `jsonlite`, `lubridate`, `scales`, `purrr`, `boot`, and `data.table`, plus `tibble` and `knitr`. Package versions and a data acquisition procedure are not supplied. Rebuilding requires obtaining the inputs, restoring an executable source document from the displayed code, and configuring its data directory.

## Interpretation and limitations

Treat this as exploratory historical analysis. Segments are selected using the same outcomes later used in the simulation; chronological plotting does not make the evaluation out of sample. Bootstrap intervals for selected segments do not establish an independently validated trading advantage.

The analysis includes only resolved binary Yes/No markets with available price history. Coverage, category rules, and nearest-price snapshot tolerances affect the results. Recorded closure times and aggregate volume also need point-in-time verification before they can support a live trading evaluation.

The cost model assumes a fixed spread charge and a fee on winning payouts. It does not establish executable fills, market capacity, or current fee accuracy. The simulation's `outcome - entry_price` calculation represents one contract with a $1 payoff, despite the report's “$1 bet” wording; it is not a fixed $1 capital allocation per market. Bot sizing and risk controls are proposals, not implemented execution features.

## Attribution and license

The report credits Laurence. It uses the R ecosystem packages listed above; their algorithms and libraries remain the work of their respective authors. No repository-level license is included.

