# Beyond Inflated Accuracy: Mitigating Look-Ahead Bias and Benchmarking Advanced Architectures for KSE-100 Stock Prediction

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.15-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-Latest-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Overview
This repository contains a critical reproduction and extension of recent research regarding stock prediction for the Pakistan Stock Exchange (KSE-100).

**The Core Finding**
While reproducing a baseline study that claimed **85% accuracy**, we identified a methodological flaw known as **Look-Ahead Bias**. The original model achieved high accuracy by using input features (such as *Momentum*) that contained current-day price information to classify the current-day trend.

**The Solution**
We implemented a corrected framework that:
1.  **Removes Leakage:** Enforces a strict forecasting window where the model must predict *tomorrow's* price ($t+1$) using only *today's* data ($t$).
2.  **Validates Reality:** Establishes a realistic market accuracy baseline of approximately **55%**.
3.  **Advanced Models:** Introduces XGBoost and Transformer architectures to improve upon the traditional ANN, SVM, RF, and LSTM models used in the baseline study.

---

## Key Findings: Look-Ahead Bias
The difference between the inflated results of the baseline paper and the realistic results of this project lies in the target definition.

### 1. The Leaked Configuration (Baseline)
* **Method:** The model predicts if the price went up *today* while having access to indicators calculated using *today's* price.
* **Feature Analysis:** The model relied almost 90% on the "Momentum" indicator, effectively extracting the answer from the input.
* **Result:** ~85% Accuracy (Invalid for real-world trading).

### 2. The Honest Configuration (Proposed)
* **Method:** The model predicts if the price will go up *tomorrow*, with no access to future data.
* **Feature Analysis:** The model relies on a balanced set of indicators like RSI, Stochastic Oscillator, and Volume.
* **Result:** ~55% Accuracy (Valid and consistent with financial theory).

---

## Models Implemented

| Model | Type | Description |
|-------|------|-------------|
| **ANN** | Deep Learning | The baseline Multi-Layer Perceptron replicated from literature. |
| **SVM** | Classical ML | Support Vector Machine used for baseline comparison. |
| **Random Forest** | Ensemble | Bagging method used in the base paper; serves as a comparison to XGBoost. |
| **LSTM** | Deep Learning | Recurrent Neural Network for sequential data (Base Paper model). |
| **XGBoost** | Ensemble | **(New)** Gradient boosting optimized for tabular technical indicators. |
| **Transformer** | Deep Learning | **(New)** Custom architecture using Self-Attention to capture time-series dependencies. |

---

> **Note:** The "Honest" accuracy hovering around 52-55% is not a failure; it is the statistical reality of the Efficient Market Hypothesis.

---

## Repository Structure

```bash
├── AAI_Final_Implementation.ipynb   # Main notebook (Preprocessing, Training, Evaluation)
├── Conference_Paper.pdf             # IEEE formatted paper detailing the research                         
└── README.md                        # Project documentation
