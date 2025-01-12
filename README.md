Below is a sample **README** file that you can adapt and include with your repository. It provides a concise overview of how the notebook works and what it accomplishes.

**DISCLAIMER**: Most of this code was written using ChatGPT.

---

# README

## Overview
This Jupyter Notebook demonstrates a **mean-variance portfolio optimization** workflow using historical price data. It follows **Modern Portfolio Theory (MPT)** concepts introduced by Harry Markowitz. Key highlights include:

- **Data Loading & Preprocessing**: Loads CSV files containing historical prices, handles missing values, trims the dataset, and converts to daily returns.
- **Statistical Computations**: Computes daily returns, covariance matrices, and then annualizes these metrics.
- **Portfolio Optimization**: Uses *convex optimization* to construct:
  - A **minimum-variance portfolio** subject to a desired target return.
  - A **maximum Sharpe ratio portfolio** (“market portfolio”) using a stochastic search approach.
- **Visualizations**:  
  - Correlation & covariance matrix plots.  
  - A treemap / bubble chart illustrating portfolio composition & metrics.  
  - An *efficient frontier* plot showcasing the trade-off between return and volatility for various target returns.  

In simpler terms, the notebook reads historical price data, calculates risk/return statistics, and identifies the portfolio that either (1) meets a target return with the least volatility or (2) maximizes the Sharpe ratio under optional constraints such as a maximum number of assets.

## Requirements
- **Python 3.7+**
- **Jupyter Notebook** (or a similar environment like JupyterLab)
- **Packages**:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `scipy`
  - `squarify`
  - `tqdm`
  - `typing` (standard library in most Python versions)
  
You can install missing packages via:

```bash
pip install numpy pandas matplotlib scipy squarify tqdm
```

## How It Works

1. **Load Price Data**  
   - `load_price_data(...)` function reads a CSV file containing historical price data of various assets (stocks, cryptocurrencies, or indices).
   - It sorts the data by date, drops rows with excessive missing values, and ensures a consistent timeseries index.

2. **Compute Returns & Covariance**  
   - `compute_returns_and_covariance_matrix(...)` calculates the **daily returns** and forms a **covariance matrix** for the assets.
   - `annualize_returns_and_covaraince_matrix(...)` annualizes these daily metrics based on a specified number of trading days per year.

3. **Explore Data**  
   - Correlation plots (`plot_correlation_matrix`) and “return squares” (`plot_return_square`) help visualize the overall relationship among assets and their average returns.

4. **Efficient Frontier**  
   - `plot_efficient_frontier(...)` generates a range of **minimum-variance portfolios** across different target returns.  
   - This produces the classic *efficient frontier* curve, showing the trade-off between risk (volatility) and reward (return).

5. **Portfolio Construction**  
   - **Minimum-Variance Portfolio**:  
     `compute_min_variance_portfolio(...)` finds the portfolio weights that minimize variance for a specified target return.
   - **Max Sharpe Ratio Portfolio**:  
     `compute_max_sharpe_ratio_portfolio(...)` finds the “market portfolio” that maximizes the Sharpe ratio, optionally restricting the portfolio to a certain number of assets.

6. **Rounding & Pruning**  
   - Because fractional weights can be unwieldy, the notebook has helper functions (`round_portfolio`, `round_and_prune_portfolio`) to round asset weights to a specified number of decimals.  
   - Note that rounding can slightly degrade the *ideal* portfolio statistics.

7. **Visualization & Results**  
   - `plot_portfolio(...)` displays a combined **bubble chart** (comparing return & risk) and a **treemap** (showing weight and Sharpe ratio).
   - `calculate_portfolio_statistics(...)` calculates and prints the portfolio’s annual expected return, volatility, and Sharpe ratio.

8. **User-Specific Customization**  
   - You can tweak the number of assets (`number_of_stocks_in_portfolio`), the time horizon (`number_of_historical_years`), the **risk-free rate**, and the **target return** to explore different investment scenarios.

## Usage
1. **Clone or download** this repository to your local environment.
2. Install the **Python** dependencies via `pip` or `conda`.
3. **Open the Jupyter Notebook** (e.g., `mean_variance_portfolio_optimization.ipynb`) in Jupyter Lab or Notebook.
4. **Run the cells** sequentially:
   - Adjust any input variables (e.g., target return, data paths).
   - Follow the inline comments to switch between a target-return portfolio or the maximum Sharpe ratio portfolio.
   - Observe the outputs: correlation matrix, efficient frontier, portfolio composition, and performance metrics.

## Notes & Disclaimers
- **Data Quality**: The notebook’s output depends heavily on the quality and coverage of your input CSV data.  
- **Historical Performance ≠ Future Results**: The approach is purely historical and does not guarantee future performance.  
- **Parameter Sensitivity**: Settings such as `risk_free_rate`, `max_assets`, or even the smoothing (rounding) can materially affect results. Experiment accordingly.  
- **No Short-Selling**: By default, the optimization constrains weights to be non-negative. If you want to allow short positions, you’ll need to adjust bounds in the optimization functions.

## Contact
If you have questions, suggestions, or improvements, feel free to open an issue or contact me via danielsen.contact@gmail.com

---

Feel free to modify this **README** to match your specific workflow, folder structure, or desired level of detail.
