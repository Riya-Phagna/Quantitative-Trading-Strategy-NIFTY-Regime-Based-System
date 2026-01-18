📈 NIFTY Regime-Based Quantitative Trading System

A regime-aware quantitative trading framework for the NIFTY index, integrating market microstructure data, derivatives analytics, Hidden Markov Models, and machine learning to achieve robust, risk-adjusted performance.

Name : Riya Phagna
Roll number : 24/SCA/MCA/040

📌 Project Overview

This project implements an end-to-end systematic trading pipeline designed to adapt dynamically to changing market conditions.
Rather than applying a single strategy across all environments, the system first detects market regimes and then executes regime-specific trading logic, further enhanced using machine learning-based trade filtering.

🔍 Key Highlights

Multi-asset data integration (Spot, Futures, Options)

Regime detection using Hidden Markov Models (HMM)

EMA crossover strategy with regime-based execution

Options Greeks & volatility-driven feature engineering

XGBoost & LSTM models for trade probability filtering

Out-of-sample backtesting with detailed performance analytics

🧠 Strategy Philosophy

Markets behave differently under different regimes.
A strategy that works in trends may fail in ranges.

This system:

Identifies market regimes first

Trades selectively based on regime context

Avoids low-signal environments

Uses ML models to increase precision, not complexity

🗂️ Project Structure
├── data/
│   ├── raw/                  # Raw NIFTY spot, futures & options data
│   ├── processed/            # Cleaned and feature-engineered datasets
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_feature_engineering.ipynb
│   ├── 03_regime_detection_hmm.ipynb
│   ├── 04_strategy_backtesting.ipynb
│   ├── 05_ml_trade_filtering.ipynb
│   └── 06_outlier_trade_analysis.ipynb
│
├── models/
│   ├── hmm_model.pkl
│   ├── xgboost_model.pkl
│   └── lstm_model.h5
│
├── results/
│   ├── performance_metrics.csv
│   ├── equity_curves/
│   └── trade_statistics/
│
├── requirements.txt
├── README.md
└── LICENSE

📊 Data Description
Instruments Used

NIFTY Spot Index

NIFTY Futures (Continuous Contract)

NIFTY Options Chain

Data Characteristics

Frequency: 5-minute bars

Futures rollover handled via continuous contract logic

All datasets timestamp-aligned to prevent leakage

🧮 Feature Engineering
📉 Technical Indicators

EMA (9, 15, 45)

Returns & momentum measures

🧠 Derivatives Features

Options Greeks:

Delta

Gamma

Theta

Vega

Rho

Average Implied Volatility

IV Spread (Call vs Put)

📊 Sentiment & Positioning

Put-Call Ratio (PCR):

Open Interest-based

Volume-based

Futures Basis

🔁 Market Regime Detection

Model: Hidden Markov Model (HMM)

Number of states: 3

Regimes Identified
Regime	Interpretation
Regime 0	Uptrend
Regime 1	Sideways
Regime 2	Downtrend
Training Methodology

Trained on first 70% of historical data

Remaining 30% used strictly out-of-sample

Prevents look-ahead bias

⚙️ Trading Strategy Logic
Signal Generation

5 / 15 EMA crossover

Regime-Based Execution Rules
Regime	Action
Uptrend	Long trades only
Downtrend	Short trades only
Sideways	No trades

This approach:

Reduces whipsaw losses

Improves Sharpe & drawdown profile

Filters low-conviction signals

🤖 Machine Learning Enhancement

To further refine trade quality:

Models Used

XGBoost (Tree-based classifier)

LSTM (Sequence model)

ML Objective

Binary classification:

1 → Trade likely profitable

0 → Trade likely unprofitable

ML Integration

Trades executed only if predicted probability exceeds threshold

Acts as a confidence filter, not a signal generator

📈 Backtesting & Performance Evaluation
Evaluation Framework

Strict out-of-sample testing

No parameter leakage

Trade-by-trade analytics

Key Metrics

Total Return

Sharpe Ratio

Sortino Ratio

Maximum Drawdown

Win Rate

Average Trade Return

🚨 Outlier Trade Analysis

Identification of extreme winners using 3-sigma rule

Trade segmentation by:

Market regime

Greeks exposure

Time of day

Insights Extracted

Specific volatility regimes produce outsized returns

Certain intraday windows outperform consistently

Provides guidance for:

Position sizing

Time-based filters

Risk allocation
