# Analysis Plan & Notes — RSI Strategy Analyzer

## 1. Objective
- Quantify the usefulness of RSI-based trading strategies across different asset classes, timeframes, and market regimes.  
- Determine where RSI produces statistically robust excess returns after accounting for transaction costs.

---

## 2. Datasets
- **Equities:** SPY, QQQ (via yfinance)  
- **Crypto:** BTC-USD, ETH-USD (via yfinance or ccxt)  
- **FX:** EURUSD=X, GBPUSD=X (via yfinance or alternative data source)  
- Optional: Futures proxies such as GC=F (Gold) or CL=F (Crude Oil).  

Data stored locally or cached automatically when fetched.  

---

## 3. Strategy Definitions
### a) Mean Reversion
- Buy when RSI < Lower Threshold (L)  
- Exit when RSI > Exit Level (E)

### b) Overbought Reversal
- Short when RSI > Upper Threshold (U)  
- Exit when RSI < Exit Level (E)

### c) Trend-Follow
- Long when RSI crosses above 50  
- Exit when RSI crosses below 50  

**Parameter grids:**  
- RSI Period ∈ {7, 14, 21}  
- L ∈ {20, 25, 30, 35}  
- U ∈ {65, 70, 75}  

---

## 4. Backtesting Mechanics
- Execution at **bar close** (no intra-bar fill assumption).  
- Fixed position sizing (e.g., 1 unit per trade).  
- Add configurable **slippage** and **commission** (e.g., 5bps to 25bps).  
- Metrics to compute:
  - Total Return  
  - CAGR (Compounded Annual Growth Rate)  
  - Volatility  
  - Sharpe Ratio (annualized)  
  - Sortino Ratio  
  - Max Drawdown  
  - Win Rate  
  - Average Trade Return  

---

## 5. Regime Detection
- Features used:
  - Rolling volatility (std of returns)  
  - Trend slope (via rolling regression or price gradient)  
  - ATR (Average True Range)  
  - Autocorrelation  

### Regime classification:
- **Trending:** High slope, moderate-to-high volatility  
- **Ranging:** Low slope, low volatility  
- **Volatile:** High volatility, inconsistent direction  

### Evaluation:
- Measure strategy performance per regime  
- Compare win rate, Sharpe, and PnL across market states  

---

## 6. Parameter Sweep & Robustness Testing
- Conduct **grid search** over RSI periods and thresholds.  
- Generate heatmaps for Sharpe Ratio or total PnL by parameter combination.  
- Perform **bootstrap resampling** or **block bootstraps** for significance intervals.  

---

## 7. Statistical Validation
- Apply t-tests or bootstrap confidence intervals for mean return differences.  
- Control false discovery using **Benjamini–Hochberg correction** for multiple parameter tests.  

---

## 8. Presentation & Insights
- Create short summaries for key markets:
  - Example: “BTC-USD (4H) — Mean Reversion performs best during ranging regimes.”  
- Visuals to include:
  - Equity curve and drawdown plot  
  - Parameter-performance heatmap  
  - Regime-based performance comparison table  

---

## 9. Deliverables
- Final **Streamlit app** with regime tagging and heatmaps  
- Supporting **notebook(s)** for parameter sweeps  
- Exported **charts and tables** summarizing key findings  
- Published **README.md** and **ANALYSIS.md** in the repository  

---

## 10. Future Work
- Introduce **regime-aware machine learning** (predict market state, adapt parameters).  
- Test **ensemble strategies** combining RSI with MACD or ATR filters.  
- Add **live signal monitoring** with alert thresholds.  
- Optimize computational efficiency (vectorization via `vectorbt` or `numba`).

---
