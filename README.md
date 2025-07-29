# Cross-Country Portfolio Optimization using Linear Programming

This project applies linear programming to optimize a long-short equity portfolio across multiple countries. It fetches historical stock data from Yahoo Finance and computes expected returns to dynamically allocate portfolio weights that maximize returns while minimizing turnover.

**Developed as part of the 2023 Cornell International Trading Competition**, where I served as a **team lead**

## What It Does

- Fetches **daily stock data** from Yahoo Finance using `yfinance`
- Calculates **daily expected returns** from open and close prices
- Formulates a **portfolio optimization problem** using `PuLP`:
  - Maximize expected return
  - Maintain 50% long and 50% short positions
  - Minimize portfolio turnover across days
  - Enforce long-short exclusivity per asset
- Solves the optimization using the **CBC solver**
- Returns a **time series of optimal weights** for each asset

## Requirements

- `pandas`
- `pulp`
- `yfinance`

You can install them using:

```bash
pip install pandas pulp yfinance
```

## File Overview

- `get_stock_data(...)`: Downloads and processes stock price data for a list of tickers by country
- `get_weights(...)`: Optimizes the portfolio using linear programming with turnover constraints
- `main()`: Defines the portfolio, sets the date range, runs data retrieval and optimization

## Example Portfolio

```python
portfolio = {   
    'BRA': ['PBR','VALE','ITUB','NU','BSBR'],
    'MEX': ['AMX','KCDMY','VLRS','ALFAA.MX','BBAJIOO.MX'],
    'IND': ['RELIANCE.NS','TCS', 'HDB', 'INFY', 'ADANIENT.NS'],
    'USA': ['AAPL', 'MSFT','GOOG','AMZN','NVDA']
}
```

## Date Range

From `2021-12-10` to `2021-12-30` (can be customized).

## Output

A `pandas.DataFrame` containing optimized long-short weights per asset per day:

```
            AAPL   MSFT    GOOG   AMZN   NVDA   ...
2021-12-10  0.12  -0.03   0.08   0.13   -0.10   ...
2021-12-13  0.11   0.00  -0.06   0.15    0.03   ...
...
```

## Techniques Used

- Portfolio Theory
- Linear Programming (with PuLP)
- Financial Data Engineering
- Time Series Optimization

## Potential Extensions

- Add risk constraints (e.g., variance or beta)
- Include transaction cost modeling
- Extend to multi-period forecasting using rolling windows
- Integrate reinforcement learning for adaptive rebalancing
