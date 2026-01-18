# Quantitative-Trading-Strategy-NIFTY-Regime-Based-System
This project implements an end-to-end quantitative trading system for the NIFTY index using market data, options analytics, regime detection, rule-based trading, and machine learning.

Name : Riya Phagna
Roll No. 24/SCA/MCA/040
The system integrates:

Robust data engineering

Advanced feature engineering using options Greeks and volatility

Market regime classification using Hidden Markov Models

A regime-filtered EMA trading strategy

Machine learning models to enhance trade selection

High-performance trade (outlier) analysis for deeper insights

The objective is to demonstrate quantitative research, ML engineering, and systematic trading skills in a production-style framework.

Data Description

The project uses 5-minute interval data for the last one year:

NIFTY 50 Spot – OHLCV

NIFTY Futures – Continuous current-month contract with rollover handling

NIFTY Options – ATM, ATM±1, ATM±2 (Call & Put)

All datasets are cleaned, aligned by timestamp, and merged for analysis.

Feature Engineering

The following features are created:

Technical Indicators

EMA (5)

EMA (15)

Options-Based Features

Delta, Gamma, Theta, Vega, Rho

Average Implied Volatility

IV Spread (Call IV − Put IV)

Put-Call Ratio (OI-based and Volume-based)

Delta Neutral Ratio

Gamma Exposure

Market Features

Spot and Futures Returns

Futures Basis

The final feature set is saved as:

data/features/nifty_features_5min.csv

Regime Detection

Market regimes are identified using a Hidden Markov Model (HMM) with three states:

+1 : Uptrend

0 : Sideways

-1 : Downtrend

The model is trained on the first 70% of the data using options-driven and volatility-based features.
Regime labels are used to filter trading signals and reduce noise.

Trading Strategy

A 5/15 EMA crossover strategy is implemented with a regime filter:

Long Trades:
EMA(5) crosses above EMA(15) and regime = Uptrend

Short Trades:
EMA(5) crosses below EMA(15) and regime = Downtrend

No Trades:
Sideways regime

Trades are executed at the next candle open to avoid look-ahead bias.

Backtesting & Performance Metrics

The strategy is backtested using a train-test split (70% / 30%).

Performance metrics include:

Total Return

Sharpe Ratio

Sortino Ratio

Calmar Ratio

Maximum Drawdown

Win Rate

Profit Factor

Average Trade Duration

Machine Learning Enhancement

To improve trade quality, a binary classification problem is defined:

Target = 1 if trade is profitable, else 0

Models Used

XGBoost Classifier

LSTM Neural Network (10-candle sequence input)

Trades are executed only when the ML model predicts profitability with confidence > 0.5.
Performance is compared between:

Baseline strategy

XGBoost-filtered strategy

LSTM-filtered strategy

Outlier Trade Analysis

High-performance trades are identified using a 3-sigma (Z-score) rule.

Analysis includes:

Regime distribution

IV and Greeks behavior

Time-of-day patterns

Trade duration and EMA gap

Statistical tests and visualizations are used to compare outlier trades with normal profitable trades.

Repository Structure
quant-nifty-regime-strategy/
│
├── data/
│   ├── raw/
│   ├── cleaned/
│   └── features/
│
├── notebooks/
│   ├── 01_data_acquisition.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_regime_detection.ipynb
│   ├── 05_baseline_strategy.ipynb
│   ├── 06_ml_models.ipynb
│   └── 07_outlier_analysis.ipynb
│
├── src/
│   ├── data_utils.py
│   ├── features.py
│   ├── greeks.py
│   ├── regime.py
│   ├── strategy.py
│   ├── backtest.py
│   └── ml_models.py
│
├── models/
├── results/
├── plots/
├── requirements.txt
├── README.md
└── data_cleaning_report.txt

Installation & Setup
git clone <repository-url>
cd quant-nifty-regime-strategy
pip install -r requirements.txt


Run notebooks sequentially from 01_data_acquisition.ipynb to 07_outlier_analysis.ipynb.

Key Results Summary:

Regime-based filtering significantly reduces drawdowns

Options-based features improve regime classification

Machine learning models enhance risk-adjusted returns

Outlier trades reveal strong regime and volatility pattern


Prepare interview Q&A from this README

Just tell me 👍
