# 🚢 Titanic What-If Engine: Probabilistic Survival Stress-Testing

[![Python](https://shields.io)](https://www.python.org/)
[![Scikit-Learn](https://shields.io)](https://scikit-learn.org/)
[![Status](https://shields.io)]()

## 📌 Project Overview
This repository moves beyond standard exploratory scripts to focus on **end-to-end Machine Learning engineering, hyperparameter optimization, robustness stress-testing, and real-time probabilistic inference**.

Using the historical Titanic passenger manifest, we build an automated **Scikit-Learn Pipeline** powered by a tuned **Random Forest Classifier**. Beyond out-of-sample evaluation, the repository implements synthetic data corruption stress-tests and an **Interactive What-If Inference Engine** that computes conditional survival probabilities (`predict_proba`) from custom user-defined input vectors.

---

## 🛠️ System Architecture & Workflow
1. **Exploratory Analysis & Feature Filtering:** Inspecting missingness patterns (`age`, `deck`, `embarked`) and dropping high-sparsity or leaky/redundant features (`alive`, `class`, `embark_town`, `deck`).
2. **Modular Preprocessing Pipeline (`ColumnTransformer`):**
   - *Numerical features (`age`, `sibsp`, `parch`, `fare`):* Median imputation + `StandardScaler`.
   - *Categorical features (`sex`, `embarked`, `who`, `adult_male`, `alone`):* Most-frequent imputation + `OneHotEncoder`.
3. **Stratified Validation & Hyperparameter Tuning:** 80/20 stratified train-test split followed by 5-fold cross-validated `RandomizedSearchCV` (`n_estimators=200`, `max_depth=10`, `min_samples_split=10`).
4. **Robustness Stress-Testing:** Injecting synthetic Gaussian noise (σ = 5 years) on `age` and uniform perturbations (± 20%) on `fare` to evaluate out-of-sample stability under corrupted inputs.
5. **Interactive What-If Inference Engine:** A real-time CLI simulator allowing users to input custom demographic and socio-economic parameters to compute conditional survival odds.

---

## 📊 Key Findings & Model Performance

| Evaluation Regime | Accuracy | ROC-AUC | F1-Score (Survived) |
| :--- | :---: | :---: | :---: |
| **Clean Test Set (Out-of-Sample)** | **83.0%** | **0.8441** | **0.76** |
| **Stressed Test Set (Noisy Inputs)** | **80.0%** | **0.8503** | **0.72** |

- **Resilience to Input Noise:** Under synthetic perturbations on `age` and `fare`, the tuned Random Forest maintains an **80.0% accuracy** and **0.8503 ROC-AUC**, demonstrating strong generalization without overfitting.
- **Socio-Economic & Class Shift (What-If Benchmark):** Moving a baseline 25-year-old solo male passenger from 3rd Class (`£7.25` fare) to 1st Class (`£150.00` fare) increases his estimated survival probability from **4.20%** to **38.23%**.

---

## 🚀 Quick Start & Interactive Simulation (Google Colab)
1. Open the notebook `Titanic_WhatIf_Engine.ipynb` in **Google Colab** (or Jupyter).
2. Run all setup, training, and stress-testing cells sequentially.
3. Scroll down to **Section 9 (`valuta_sopravvivenza()`)** and enter your custom passenger profile in the interactive prompt to simulate your survival probability.

---

## 📂 Repository Structure
```text
├── Titanic_WhatIf_Engine.ipynb       # Full ML pipeline, stress-test & interactive CLI simulator
└── README.md                         # Technical documentation
```

