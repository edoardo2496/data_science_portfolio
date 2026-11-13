# 🚀 Iron-Price-OU-TimesFM: Commodity Forecasting & Risk Engine

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/edoardo2496/data_science_portfolio/blob/main/Iron-Price-OU-TimesFM/Iron_Price_OU_TimesFM.ipynb)

## 📌 Project Overview
This project benchmarks two distinct quantitative paradigms for forecasting **Raw Iron (`€/kg`)** monthly prices over a 24-month horizon and optimizing industrial procurement strategies:
1. **Stochastic Differential Equations (Ornstein-Uhlenbeck Process):** A classical econometric/quantitative finance approach capturing mean-reversion dynamics, calibrated via OLS regression, solved analytically via **Itô's Lemma**, and simulated through **10,000 Monte Carlo paths**.
2. **Time Series Foundation Models (Google TimesFM 2.5):** A zero-shot deep learning Transformer architecture (`google/timesfm-2.5-200m-pytorch`) capable of capturing complex non-linear sequential patterns and generating probabilistic risk quantiles (`Q10`–`Q90`) without custom gradient training.

---

## 🧠 Methodology & Architecture

### 1. Data Ingestion & Stationarity Validation
* **Dataset:** Monthly raw iron prices (`€/kg`) filtered from `2005-01-01` onwards (`dati_ferro_grezzo.xlsx`).
* **Statistical Validation:** Augmented Dickey-Fuller (**ADF**) test confirms stationarity ($p < 0.05$), validating the mean-reverting hypothesis required for stochastic modeling.

### 2. Ornstein-Uhlenbeck (OU) Stochastic Calibration
The continuous-time price dynamics are modeled as:
$$dS_t = \theta (\mu - S_t)dt + \sigma dW_t$$
* **$\theta$ (Mean-Reversion Speed) & Half-Life:** Quantifies how fast price shocks decay back toward equilibrium.
* **$\mu$ (Long-Term Equilibrium Mean):** Economic anchor representing structural marginal production costs.
* **Operational Z-Score:** Real-time standardization of the current spot price ($S_0$) against residual volatility to trigger actionable procurement signals (*Buying Zone* at $Z < -1.5$, *Risk Zone* at $Z > +1.5$).

### 3. Google TimesFM Zero-Shot Inference
* Uses Google's pre-trained **TimesFM 2.5 (200M parameters)** PyTorch implementation.
* Generates 24-month forward trajectories alongside continuous quantile heads (`10th` and `90th` percentiles) to measure asymmetric market uncertainty.

---

## ⚖️ Key Takeaways: Itô's Lemma vs. Google TimesFM

| Dimension | Ornstein-Uhlenbeck (Itô / Monte Carlo) | Google TimesFM (Foundation Model) |
| :--- | :--- | :--- |
| **Core Mechanism** | Parametric, mean-reverting SDE anchored to historical equilibrium ($\mu$). | Data-driven Transformer recognizing multi-scale temporal patterns. |
| **Uncertainty Cone** | Variance stabilizes asymptotically over long horizons. | Dynamic quantile bands sensitive to recent momentum and regime shifts. |
| **Business Utility** | **Ideal for Timing & Governance:** Provides explainable Z-score rules for CFO/budget justification. | **Ideal for Trend Detection:** Adapts rapidly if macroeconomic regimes shift permanently. |

**Strategic Conclusion:** Combining both models yields a robust **Hybrid Procurement Engine**—using **TimesFM** as an early-warning sensor for directional momentum, while relying on the **Ornstein-Uhlenbeck Z-score** as a disciplined risk-management anchor for inventory sizing.

---

## 🛠️ Tech Stack
* **Language:** Python 3.10
