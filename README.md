# Capstone Project 2026 — Data-Driven Stock Analysis Using Time Series Models

End-to-end time series forecasting pipeline on 5 NSE stocks with virtual portfolio execution on StockGro.

---

## Project Structure

```
project_capstone_time-series/
├── capstone_timeseries.ipynb       # Main notebook (all 8 tasks, 46 cells)
├── Capstone Project 2026.pdf       # Original capstone brief
├── README.md                       # This file
│
├── task1_sector_performance.png    # Sector cumulative returns 2021–2025
├── task1_stock_analysis.png        # Per-stock: price, rolling vol, STL trend
├── task2_train_test_split.png      # Train vs test split for all 5 stocks
├── task2_acf_pacf.png              # ACF/PACF plots for ARIMA order selection
├── task3_arima.png                 # ARIMA forecasts vs actual
├── task3_holtwinters.png           # Holt-Winters forecasts vs actual
├── task3_prophet.png               # Prophet forecasts vs actual
├── task3_lstm.png                  # LSTM forecasts vs actual
├── task3_ensemble.png              # All models + ensemble overlay
├── task4_volatility.png            # Rolling volatility + correlation heatmap
├── task4_garch.png                 # GARCH(1,1) conditional volatility
├── task4_stl.png                   # STL decomposition (all 5 stocks)
├── task5_allocation.png            # Portfolio weights pie + strategy breakdown
├── task5_mc_sharpe.png             # Monte Carlo distribution + Sharpe ratios
├── task6_model_comparison.png      # MAPE / RMSE / Directional Accuracy heatmaps
├── task8_performance.png           # Predicted vs actual performance chart
└── dashboard_final.png             # 12-panel complete summary dashboard
```

---

## Dataset

| Parameter | Value |
|-----------|-------|
| Source | Yahoo Finance (`yfinance`) |
| Base period | 1 Jan 2021 – 31 Dec 2025 |
| Extended (live) | 1 Jan 2026 – 13 May 2026 |
| Interval | Daily adjusted close |
| Train set | Jan 2021 – Jun 2025 |
| Test set | Jul 2025 – 13 May 2026 |
| Forecast target | 14–15 May 2026 (2 trading days) |

**Stocks selected:**

| Ticker | Stock | Sector | Reason |
|--------|-------|--------|--------|
| HDFCBANK.NS | HDFC Bank | Banking | Largest private bank; low volatility; positive STL trend |
| TCS.NS | Tata Consultancy Services | IT | Largest IT exporter; consistent uptrend |
| SUNPHARMA.NS | Sun Pharmaceutical | Pharma | Market leader in specialty generics; low beta |
| HINDUNILVR.NS | Hindustan Unilever | FMCG | Dominant FMCG franchise; stable seasonal trend |
| MARUTI.NS | Maruti Suzuki | Auto | India's largest car maker; Auto sector top performer at +196% |

---

## Setup

### Requirements

```bash
pip install yfinance prophet statsmodels scikit-learn tensorflow arch matplotlib seaborn
```

### Python Version

Python 3.9+ recommended. Tested on Python 3.13.

---

## How to Run

1. Open `capstone_timeseries.ipynb` in Jupyter or VS Code
2. Run all cells top to bottom — **Kernel → Restart & Run All**
3. **First run:** stock data downloads from Yahoo Finance and is cached automatically in `data_cache/`
4. **Subsequent runs:** all data loads from cache — takes under a minute

> **Note on rate limits:** If Yahoo Finance returns a rate-limit error on first run, wait 20–30 minutes and try again. Once cached, this will never happen again.

---

## Models Used

| Model | Notes |
|-------|-------|
| **ARIMA** | Grid search over p,q ∈ {0..3}, d=1; best order by AIC |
| **Prophet** | Additive yearly + weekly seasonality; changepoint_prior = 0.05 |
| **Holt-Winters** | Additive trend + seasonal; period = 252 trading days |
| **LSTM** | 60-day sequence; 2× LSTM(50) + Dropout; rolling test prediction |
| **Ensemble** | Simple mean of all 4 models; typically lowest MAPE |

---

## Portfolio Strategy

Three strategies blended into a final allocation (₹10,00,000 virtual capital):

| Strategy | Weight | Signal |
|----------|--------|--------|
| A — Forecast-guided | 40% | Rank by predicted 2-day return (best model per stock) |
| B — Inverse volatility | 30% | `w = (1/σ_GARCH) / Σ(1/σ_GARCH)` |
| D — Sector momentum | 30% | Proportional to sector 5-year cumulative return |

---

## Actual Trading Results (StockGro)

**Trading window:** 14 May 2026 (buy) → 15 May 2026 (auto-close 3:25 PM)

| Stock | Buy Price | Sell Price | Shares | P&L |
|-------|-----------|------------|--------|-----|
| HDFCBANK.NS | ₹741.10 | ₹761.22 | 319 | +₹6,418 (+2.72%) |
| TCS.NS | ₹2,194.89 | ₹2,220.23 | 73 | +₹1,850 (+1.15%) |
| SUNPHARMA.NS | ₹1,814.81 | ₹1,848.49 | 50 | +₹1,684 (+1.86%) |
| HINDUNILVR.NS | ₹2,252.88 | ₹2,254.60 | 66 | +₹114 (+0.08%) |
| MARUTI.NS | ₹12,963.71 | ₹12,994.56 | 22 | +₹679 (+0.24%) |
| **Portfolio** | | | | **+₹9,823 (+0.97%)** |

All 5 positions closed profitable. Directional accuracy: 5/5 correct.

---

## Tasks Overview

| Task | Description |
|------|-------------|
| **Task 1** | Sector index ranking; one large-cap stock selected per top sector |
| **Task 2** | Data download, missing value handling, ADF stationarity test, ACF/PACF, train/test split |
| **Task 3** | ARIMA, Prophet, Holt-Winters, LSTM, and Ensemble forecasting per stock |
| **Task 4** | Log returns, rolling volatility, GARCH(1,1), STL decomposition |
| **Task 5** | Three-strategy portfolio blend, Sharpe ratio, Monte Carlo simulation |
| **Task 6** | MAPE, RMSE, Directional Accuracy comparison across all models and stocks |
| **Task 7** | StockGro virtual trade execution — actual buy prices and shares filled |
| **Task 8** | Predicted vs actual comparison, per-stock P&L, reflection |

---

## Virtual Trading Platform

Platform: [StockGro](https://stockgro.onelink.me/vNON/21jikjek)
Event: **Portfolio – Time Series Analysis 2026**
Capital: ₹10,00,000 | Window: 14–15 May 2026

---

*Capstone 2026 — Time Series Analysis on NSE Stocks*
