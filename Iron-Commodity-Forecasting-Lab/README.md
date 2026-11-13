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

## 📊 Empirical Results: Itô's Lemma vs. Google TimesFM

Evaluating both models across 3, 6, 12, and 24-month horizons reveals a clear structural divergence between economic mean-reversion and data-driven momentum extrapolation:

| Horizon | OU Expected (`€/kg`) | OU 95% CI Lower | OU 95% CI Upper | TimesFM Forecast (`€/kg`) | Spread (TimesFM vs. OU) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **3 Months** | `0.2560` | `0.1672` | `0.3448` | `0.2525` | `-1.37%` (`-0.0035 €/kg`) |
| **6 Months** | `0.2591` | `0.1407` | `0.3776` | `0.2452` | `-5.36%` (`-0.0139 €/kg`) |
| **12 Months** | `0.2644` | `0.1141` | `0.4146` | `0.2395` | `-9.42%` (`-0.0249 €/kg`) |
| **24 Months** | `0.2717` | `0.0958` | `0.4476` | `0.2321` | `-14.57%` (`-0.0396 €/kg`) |

### Key Analytical Insights:
* **Mean-Reversion Pull (OU Model):** Because the current spot price sits below the 20-year structural average ($\mu$), Itô's analytical solution projects a steady upward reversion from `0.2560 €/kg` (3m) to `0.2717 €/kg` (24m).
* **Downward Momentum Detection (TimesFM):** Unconstrained by economic equilibrium priors, Google's Transformer detects recent downward sequential momentum and projects a gradual decline toward `0.2321 €/kg` at 24 months.
* **Statistical Consistency:** Despite the ~14.6% directional spread at the 2-year mark, TimesFM's trajectory remains entirely within the Ornstein-Uhlenbeck 95% confidence cone (`0.0958` – `0.4476 €/kg`), confirming that both scenarios are statistically consistent with historical commodity volatility.

---

## ⚖️ Architectural & Business Comparison

| Dimension | Ornstein-Uhlenbeck (Itô / Monte Carlo) | Google TimesFM (Foundation Model) |
| :--- | :--- | :--- |
| **Core Mechanism** | Parametric, mean-reverting SDE anchored to historical equilibrium ($\mu$). | Data-driven Transformer recognizing multi-scale temporal patterns. |
| **Uncertainty Cone** | Variance stabilizes asymptotically over long horizons. | Dynamic quantile bands sensitive to recent momentum and regime shifts. |
| **Procurement Strategy** | **Forward Hedging / Stocking:** Signals locking in contracts before prices revert upward toward $\mu$. | **Just-in-Time Purchasing:** Advises lean inventory to capitalize on projected short-to-medium term price drops. |

**Strategic Conclusion:** Combining both models yields a robust **Hybrid Procurement Engine**—using **TimesFM** as an early-warning sensor for directional momentum, while relying on the **Ornstein-Uhlenbeck Z-score** as an explainable risk-management anchor for CFO governance and inventory sizing.

---

## 🛠️ Tech Stack
* **Language:** Python 3.10+
* **Foundation Model:** `timesfm` (`google/timesfm-2.5-200m-pytorch`), PyTorch
* **Econometrics & Math:** `statsmodels` (ADF Test), `scikit-learn`, `numpy` (Euler-Maruyama MC & Itô's Lemma)
* **Data & Visualization:** `pandas`, `openpyxl`, `matplotlib`, `seaborn`

---

## 📂 Repository Structure
Iron-Price-OU-TimesFM/
│
├── Iron-Commodity-Forecasting-Lab.ipynb   # Main Google Colab / Jupyter Notebook
├── dati_ferro_grezzo.xlsx                 # Historical monthly raw iron dataset
└── README.md                              # Project documentation & empirical benchmark
