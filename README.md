# Exploring the Applicability of Monte Carlo Simulations and Optimization for Asset Portfolios

This repository explores two common approaches to portfolio optimization: **Monte Carlo simulations** and mathematical **SLSQP optimization** using `scipy.optimize.minimize`. Both methods are applied to a portfolio consisting of four stocks: AMD, AAPL, MSFT, and ORCL.

## Overview
The goal is to identify the portfolio weights that maximize the Sharpe ratio, which balances return against risk. We compare:

1. Random portfolio generation via Monte Carlo simulation  
2. Precise optimization using the Sequential Least Squares Programming (SLSQP) algorithm

## Data Preparation
- Historical adjusted close prices are retrieved for AMD, AAPL, MSFT, and ORCL.
- Daily returns are calculated from the price data.

## Monte Carlo Simulation
- 10,000 random portfolios are created by assigning random weights to each stock.
- Weights are normalized to sum to 1 (full investment, no leverage).
- For each portfolio:
  - Expected annual return is computed
  - Annualized volatility is calculated from the covariance matrix
  - Sharpe ratio is derived using return and volatility
- The portfolio with the highest Sharpe ratio is highlighted as the Monte Carlo optimal portfolio.

## Optimization with Scipy (SLSQP)
- Uses the `minimize()` function from `scipy.optimize` to directly maximize the Sharpe ratio.
- Since `minimize()` minimizes by default, the Sharpe ratio function is negated.
- Constraints:
  - Weights must sum to 1 (`lambda x: np.sum(x) - 1`)
  - Weights must be between 0 and 1 (long-only portfolios)
- SLSQP identifies the set of weights that produce the maximum Sharpe ratio under these conditions.

## Result Comparison and Visualization
- All portfolios (from the Monte Carlo simulation) are plotted in a risk-return scatter plot.
- Both the Monte Carlo and optimized portfolios are marked clearly.
- The Sharpe ratios and weight allocations of each approach are printed for easy comparison.

## Key Insight
Monte Carlo offers a broad overview of the risk-return space, while SLSQP gives an efficient and targeted solution. Together, they provide a full picture of possible and optimal asset allocations.

## Requirements
- Python 3.8+
- Libraries: `numpy`, `pandas`, `matplotlib`, `scipy`, `yfinance`

This project was created as part of an exploration into quantitative asset allocation techniques using Python.
