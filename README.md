# Quantitative Momentum & Risk Backtester

A lightweight financial analysis tool that fetches historical asset data to evaluate risk-adjusted performance metrics. The script calculates annualized returns, annualized volatility, the **Sharpe Ratio**, and the absolute **Maximum Drawdown (Max DD)**, while providing a short-term **21-day momentum trend indicator**.

## Core Features

*   **Risk-Adjusted Performance:** Computes the mathematical **Sharpe Ratio** by comparing annualized log returns against a customizable baseline risk-free rate.
*   **Drawdown Tracking:** Features a built-in peak-tracking algorithm to compute the peak-to-trough **Maximum Drawdown** percentage over the entire historical window.
*   **Log-Normal Return Math:** Utilizes continuous log returns scaled by standard equity calendar parameters (`* 252` trading days) to ensure annualized statistical consistency.
*   **21-Day Momentum Indicator:** Employs a standard rolling price check (`iloc[-1] < iloc[-21]`) to instantly output whether the asset is currently riding an uptrend or a downtrend.

## Getting Started

### Prerequisites

Ensure you have the required quantitative and data-gathering libraries installed:

```bash
pip install numpy pandas yfinance
```

### Usage Example

```python
from datetime import datetime
# Import or paste the function here

# Run the backtester on Apple (AAPL) using a 4% risk-free rate benchmark
momentum_backtester(stock="AAPL", start="2010-01-01", risk_free_rate=4)
```

## Function Arguments & Parameters

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `stock` | `str` | `'AAPL'` | The target asset ticker symbol to pull via Yahoo Finance. |
| `start` | `str` | `'2010-01-01'` | The historical boundary start date (`YYYY-MM-DD`) for the asset track. |
| `end` | `str` | *Dynamic (Today)* | The historical boundary end date. Defaults to the current active date. |
| `risk_free_rate` | `float` | `4` | The annualized benchmark risk-free percentage rate (e.g., 10-Year Treasury yield). |

## Terminal Outputs Explained

When executed, the script processes the historical series and prints the following metrics:

*   **Trend:** Outputs `Trend: up` if today's price is higher than the price 21 trading days ago; otherwise outputs `Trend: down`.
*   **Sharpe Ratio:** The asset's excess return per unit of volatility. Higher numbers signify stronger risk-adjusted reward structures.
*   **Annualized Returns:** The mathematically smoothed yearly compounding rate of return derived from log-normal price steps.
*   **Drawdown:** The maximum peak-to-trough drop witnessed over the entire history, acting as a historical proxy for absolute worst-case capital loss scenarios.
