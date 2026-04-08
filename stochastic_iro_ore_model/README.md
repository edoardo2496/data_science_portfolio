# 📈 Stochastic Iron Ore Forecasting Dashboard
### Mean Reversion Framework via Ornstein-Uhlenbeck Process & Itô Calculus

This repository features an analytical Web-App designed for strategic decision support in the steel procurement sector. The primary objective is to model Iron Ore price dynamics to identify market asymmetries and optimal purchasing windows for raw materials.

## 🧠 Mathematical Methodology

Commodity prices typically exhibit cyclical behavior driven by marginal production costs rather than a simple Random Walk. This project implements an **Ornstein-Uhlenbeck (OU)** process, which mathematically captures the **Mean Reversion** property.

### Stochastic Differential Equation (SDE)
The price evolution $S_t$ is modeled as:

$$dS_t = \theta(\mu - S_t)dt + \sigma dW_t$$

Where:
* $\theta$ (**Speed of Reversion**): The rate at which the price is pulled back toward the equilibrium.
* $\mu$ (**Long-term Mean**): The fundamental equilibrium price level.
* $\sigma$ (**Instantaneous Volatility**): The magnitude of stochastic fluctuations.
* $dW_t$: The standard Wiener process (Brownian Motion) increment.

### Analytical Solution via Itô's Lemma
To project the forecast, we utilize the exact solution of the SDE derived through **Itô's Lemma**, defining the expected value at time $t$ given current price $S_0$:

$$E[S_t] = S_0 e^{-\theta t} + \mu(1 - e^{-\theta t})$$

The forecast uncertainty (confidence "cone") is calculated via the process variance:
$$Var[S_t] = \frac{\sigma^2}{2\theta}(1 - e^{-2\theta t})$$



## 🛠️ Tech Stack
* **Back-end Calibration (Python):** Parameters ($\theta, \mu, \sigma$) estimation using linear regression on historical log-increments (World Bank Data).
* **Front-end Engine (JavaScript/Plotly.js):** Client-side implementation of the Itô analytical solution for real-time interactivity.
* **Deployment:** GitHub Pages utilizing a JSON-driven architecture.

## 📊 Business Logic
The dashboard translates future probability density into actionable operational signals:
1.  **Z-Score Analysis:** We evaluate the statistical distance of the spot price from the expected mean.
2.  **Confidence Intervals:** 95% confidence range visualization to assess market risk.
3.  **Advisory Engine:** A conditional logic engine suggests inventory accumulation when the spot price is significantly below the volatility-adjusted expected mean.

---
**Disclaimer:** *This tool is for analytical and modeling purposes only. Financial decisions based on this data are at the user's own risk.*
