# RSI Strategy Analyzer — Interactive Research App

**Short description:**  
An interactive Streamlit app for evaluating RSI-based trading strategies across multiple markets and timeframes. Built as a research-grade tool to compare strategy performance, regime-dependence, and robustness.

---

##  Why this project
- Demonstrates quantitative research, time-series analysis, and backtesting.
- Shows ability to build reproducible data pipelines, interactive visualizations, and deployable analytics.
- Designed to be useful to traders, researchers, and quant teams evaluating simple technical signals.

---

##  Features
- Multi-market selection (SPY, QQQ, EURUSD, BTC, etc.)
- Multiple timeframes (1m, 5m, 15m, 1h, 4h, 1d)
- Three RSI strategies:
  - Mean Reversion (oversold/overbought)
  - Overbought Reversal (shorting on high RSI)
  - Trend-Follow (RSI cross 50)
- Auto-tagging of market regime: **Trending / Ranging / Volatile**
- Trade-level outputs: entries/exits, PnL per trade, cumulative PnL, win rate
- Interactive charts (Plotly) with trade markers and RSI overlays
- CSV download of trade logs
- Cached data fetch to speed up repeated runs

---

## Quick start (local)
1. Clone repo:
   ```bash
   git clone <your-repo-url>
   cd rsi-strategy-analyzer
