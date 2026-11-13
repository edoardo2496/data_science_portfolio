# 📈 TimesFM-NVDA-Quant: Zero-Shot Financial Forecasting & Risk Quantification

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-Backend-red.svg)](https://pytorch.org/)
[![Google Colab](https://img.shields.io/badge/Colab-T4%20GPU-orange.svg)](https://colab.research.google.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Project Overview
This repository provides a production-ready, repository-structured Jupyter Notebook implementation for **Zero-Shot Financial Forecasting and Risk Quantification** using Google’s state-of-the-art **TimesFM (Time Series Foundation Model)**.

Targeting NVIDIA (`NVDA`) daily closing prices, the project demonstrates how to bypass traditional custom gradient descent training on financial data by leveraging pre-trained foundational priors. It projects future price paths while rigorously quantifying market uncertainty through continuous quantile heads ($Q_{10}$ bearish and $Q_{90}$ bullish risk bands).

---

## 🛠️ Key Technical Features
- **Zero-Shot Architecture:** Utilizes Google's pre-trained `timesfm-2.5-200m-pytorch` model, capturing complex temporal dependencies and volatility dynamics without local fine-tuning.
- **Probabilistic Risk Quantification:** Generates 80% confidence intervals via continuous quantile heads ($Q_{10}$ and $Q_{90}$), offering an essential framework for quantitative risk management.
- **Clean Ingestion & Preprocessing:** Automated data fetching via `yfinance`, robust MultiIndex handling, sorted pandas dataframes (`df_stoks_sorted`), and high-frequency business day mapping.
- **Cloud Accelerated:** Fully optimized to run seamlessly on Google Colab with a T4 GPU backend.

---

## 📂 Repository Structure
```text
├── TimesFM_NVDA_Quant.ipynb          # Main Google Colab Jupyter Notebook
└── README.md                         # Project documentation
