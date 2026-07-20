# Investment Decision Dashboard

Power BI dashboard comparing SPY, TLT, GLD and BTC using risk-adjusted return scoring.

## Business Problem

An individual investor wants to compare the historical performance of four financial assets — S&P 500 (SPY), Treasury bonds (TLT), gold (GLD), and bitcoin (BTC) — investing the same amount of capital in each. The goal is not just to identify the highest absolute gain, but to evaluate risk-adjusted performance using a weighted scoring model.

## Data Source

Daily historical data from [Stooq.com](https://stooq.com), accessed via each asset's historical data page (e.g. `stooq.com/q/d/?s=spy.us&c=0`). Available from 2005 (SPY/TLT/GLD) and 2010 (BTC). Transformed from daily to annualized frequency using Power Query.

## Methodology

Each asset is scored using three normalized indicators (min-max, 0–1 scale), weighted differently depending on the selected risk profile:

**Score = (Sharpe_norm × Weight_Sharpe) + (CAGR_norm × Weight_CAGR) + (Drawdown_norm × Weight_Drawdown)**

| Profile | Sharpe Ratio | CAGR | Max Drawdown |
|---|---|---|---|
| Defensive | 40% | 20% | 40% |
| Balanced | 40% | 30% | 30% |
| Aggressive* | 30% | 50% | 20% |

*Currently labeled "Expensive" in the model — pending rename.

**Sharpe Ratio:** `(Rp − Rf) / σp`, with a fixed 2% annual risk-free rate.

## Interactivity

| Control | Table | Field |
|---|---|---|
| Risk profile | `Profile` | `Segmentation` |
| Investment amount | `Amount to invest` | `Parámetro` |
| Investment period | `Calendar` | `Year` |

## Key Insight

Under the aggressive profile — where CAGR carries the highest weight (50%) — BTC leads in raw growth (normalized CAGR 1.00 vs. 0.56 for gold). Gold still wins the final score (0.78 vs. 0.69) because it dominates both risk metrics: Sharpe Ratio (1.00 vs. 0.62) and, critically, Max Drawdown, where BTC scores the worst value in the group (0.00). The model rewards risk-adjusted quality, not just growth.

## Tools

Power BI · DAX · Power Query

## Author

Jhon Melo — jhonmelocas@gmail.com
