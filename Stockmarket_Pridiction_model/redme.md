<div align="center">

# 📈 S&P 500 Market Direction Predictor

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/yfinance-0052CC?style=for-the-badge&logo=yahoo&logoColor=white"/>
</p>

<p align="center">
  A machine learning model that predicts whether the S&P 500 index will go <strong>up or down</strong> the next trading day — built with Random Forest and backtested over decades of market data.
</p>

---

</div>

## 🧠 Overview

This project uses historical S&P 500 price data (sourced live via **Yahoo Finance**) and a **Random Forest Classifier** to predict the next-day market direction. It goes beyond a simple train/test split by implementing a **walk-forward backtesting engine** — a methodology widely used in quantitative finance to prevent lookahead bias.

The model is progressively enhanced with engineered features — rolling average ratios and trend momentum indicators — to improve prediction precision.

---

## ✨ Features

- 📡 **Live Data Ingestion** — Pulls the full S&P 500 history (`^GSPC`) directly from Yahoo Finance using `yfinance`
- 🌲 **Random Forest Classifier** — Ensemble model tuned for financial time-series classification
- 🔄 **Walk-Forward Backtesting** — Rolling train/test windows simulate real-world trading conditions
- 🧪 **Feature Engineering** — Multi-horizon rolling ratios & trend signals across 2, 5, 60, 250, and 1000-day windows
- 🎯 **Precision-Optimized Threshold** — Custom 0.6 probability cutoff to reduce false positives and improve signal quality

---

## 🗂️ Project Structure

```
S_P500_prediction_model.ipynb
│
├── 1. Data Collection          → Fetch S&P 500 OHLCV data from 1990 onward
├── 2. Target Engineering       → Binary label: 1 if next close > today close, else 0
├── 3. Baseline Model           → RandomForest on raw OHLCV predictors
├── 4. Backtesting Engine       → Walk-forward validation (2500 warmup, 250-day steps)
├── 5. Feature Engineering      → Rolling ratios + trend features across 5 horizons
└── 6. Enhanced Model           → Tuned RF with probability threshold = 0.6
```

---

## 🔬 Methodology

### Target Variable
```python
sp500["Tomorrow"] = sp500["Close"].shift(-1)
sp500["Target"]   = (sp500["Tomorrow"] > sp500["Close"]).astype(int)
```
A binary label — **1** means the market closed higher the next day, **0** means it didn't.

### Backtesting Engine
```python
def backtest(data, model, predictors, start=2500, step=250):
    for i in range(start, data.shape[0], step):
        train = data.iloc[0:i]
        test  = data.iloc[i:(i+step)]
        predictions = predict(train, test, predictors, model)
        ...
```
Trains only on past data at every step — no future leakage.

### Feature Engineering
```python
horizons = [2, 5, 60, 250, 1000]

for horizon in horizons:
    sp500[f"Close_Ratio{horizon}"] = sp500["Close"] / rolling_avg["Close"]
    sp500[f"Trend_{horizon}"]      = sp500.shift(1).rolling(horizon).sum()["Target"]
```
Captures short- to long-term momentum and mean-reversion signals.

### Precision-Tuned Prediction
```python
preds = model.predict_proba(test[predictors])[:, 1]
preds[preds >= 0.6] = 1   # Only predict "Up" when model is confident
preds[preds <  0.6] = 0
```

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install yfinance scikit-learn pandas matplotlib jupyter
```

### Run the Notebook
```bash
git clone https://github.com/your-username/sp500-prediction-model.git
cd sp500-prediction-model
jupyter notebook S_P500_prediction_model.ipynb
```

---

## 📊 Results

| Model Version | Predictors | Precision Score |
|:---|:---|:---:|
| Baseline | OHLCV | ~52% |
| Enhanced | OHLCV + Rolling Features | **>60%** |

> Precision is prioritized over accuracy — in trading, minimizing false "buy" signals matters more than overall correctness.

---

## ⚠️ Disclaimer

> **This model is for educational purposes only.**
> Do **not** use this to make real trading decisions without further validation, risk management, and domain expertise. Past market patterns do not guarantee future results. Trade at your **own risk**.

You can improve this model further by:
- Adding macroeconomic indicators (VIX, bond yields, sector data)
- Incorporating international market signals from overlapping time zones
- Experimenting with XGBoost, LightGBM, or LSTM architectures
- Tuning hyperparameters via cross-validation

---

## 🛠️ Tech Stack

| Tool | Purpose |
|:---|:---|
| `yfinance` | Live S&P 500 data ingestion |
| `pandas` | Data wrangling & feature engineering |
| `scikit-learn` | Random Forest model & precision metrics |
| `matplotlib` | Visualization of price trends & predictions |
| `Jupyter Notebook` | Interactive development environment |

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">
  <sub>Built with 🤍 for learning quantitative finance and machine learning.</sub>
</div>
