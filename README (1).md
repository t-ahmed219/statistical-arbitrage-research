# Statistical Arbitrage Research

A Python research project exploring pairs trading using cointegration, regression-based hedge ratios and mean-reversion signals.

The aim of the project was not to optimise a backtest until it became profitable, but to test whether a simple statistical-arbitrage idea could hold up under out-of-sample evaluation.

## Approach

I started with Coca-Cola (KO) and PepsiCo (PEP) as an intuitive example pair, then developed the analysis in stages:

1. Download and inspect historical market data.
2. Compare daily returns and correlation.
3. Test stationarity and cointegration.
4. Estimate a regression-based hedge ratio and construct the spread.
5. Generate mean-reversion signals using a rolling z-score.
6. Extend the analysis to a wider universe of candidate pairs.
7. Run a walk-forward backtest using rolling training and unseen test periods.
8. Test sensitivity to signal parameters and transaction costs.

The walk-forward design estimates the hedge ratio using training data only and applies signals to the following test window. Positions are lagged by one trading day to reduce look-ahead bias.

## Results

The baseline KO/PEP strategy did not remain profitable out of sample.

| Metric | Result |
|---|---:|
| Total return | -8.54% |
| Annualised return | -1.54% |
| Annualised volatility | 9.35% |
| Sharpe ratio | -0.16 |
| Maximum drawdown | -19.29% |
| Active-day win rate | 46.12% |

The negative result was useful: a relationship that appears statistically reasonable in historical data does not necessarily translate into a robust trading signal. Walk-forward testing, transaction costs and changing market relationships materially affect the result.

## Notebooks

| Notebook | Purpose |
|---|---|
| `01_market_data_and_returns.ipynb` | Market data, normalised prices, returns and correlation |
| `02_cointegration_and_spread.ipynb` | Stationarity, cointegration, hedge-ratio estimation and spread construction |
| `03_signals_and_single_pair_backtest.ipynb` | Rolling z-score signals and an initial KO/PEP backtest |
| `04_multi_pair_research.ipynb` | Formation-period screening across a wider stock universe |
| `05_walk_forward_and_robustness.ipynb` | Out-of-sample walk-forward testing, parameter sensitivity and transaction-cost analysis |
| `06_final_analysis_and_report.ipynb` | Final performance metrics, equity curve, drawdown and conclusions |

## Project Structure

```text
stat-arb-research/
├── notebooks/
│   ├── 01_market_data_and_returns.ipynb
│   ├── 02_cointegration_and_spread.ipynb
│   ├── 03_signals_and_single_pair_backtest.ipynb
│   ├── 04_multi_pair_research.ipynb
│   ├── 05_walk_forward_and_robustness.ipynb
│   └── 06_final_analysis_and_report.ipynb
├── results/
│   ├── figures/
│   └── tables/
├── requirements.txt
└── README.md
```

## Tools

Python, pandas, NumPy, statsmodels, Matplotlib and yfinance.

## Running the Project

Install the dependencies:

```bash
pip install -r requirements.txt
```

Run the notebooks in numerical order. Notebook 5 saves the out-of-sample results used by Notebook 6.

## Limitations and Next Steps

This is a research backtest rather than a production trading system. It uses simplified assumptions for transaction costs, execution and portfolio construction and does not model short-borrow costs, financing costs or market impact.

Possible extensions include testing a larger universe, applying stricter pair-selection criteria, improving hedge-ratio estimation and comparing alternative position-sizing methods.
