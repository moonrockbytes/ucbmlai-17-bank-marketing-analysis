# Bank Marketing Analysis: Comparing Classifiers

## Overview

This project compares the performance of four classification algorithms — K-Nearest Neighbors (KNN), Logistic Regression, Decision Trees, and Support Vector Machines (SVM) — on a real-world bank marketing dataset. The goal is to identify the best model for predicting whether a client will subscribe to a term deposit following a phone-based marketing campaign.

**Dataset:** UC Irvine Machine Learning Repository — Bank Marketing Dataset (Portuguese banking institution, 2008–2010)

---

## Jupyter Notebook

[bank_marketing_analysis.ipynb](bank_marketing_analysis.ipynb)

---

## Project Structure

```
ucbmlai-17-bank-marketing-analysis/
├── bank_marketing_analysis.ipynb   — Main Jupyter Notebook
├── README.md                       — Project summary (this file)
├── data/
│   ├── raw/                        — Original unprocessed dataset
│   │   ├── bank-additional-full.csv
│   │   ├── bank-additional.csv
│   │   └── bank-additional-names.txt
│   └── processed/                  — Cleaned and encoded dataset
│       ├── bank_encoded.csv
│       ├── bank_features.csv
│       └── bank_target.csv
```

---

## Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/moonrockbytes/ucbmlai-17-bank-marketing-analysis.git
cd ucbmlai-17-bank-marketing-analysis
```

### 2. Create and activate a virtual environment

**macOS / Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install jupyter pandas numpy scikit-learn matplotlib seaborn
```

### 4. Launch Jupyter Notebook

```bash
jupyter notebook bank_marketing_analysis.ipynb
```

---

## Summary of Findings

### Business Problem

A Portuguese bank conducts phone-based marketing campaigns to sell term deposits. With only 11.3% of clients subscribing, the bank is spending resources on 88.7% of contacts that result in no subscription. The goal is to build a classifier that predicts which clients are likely to subscribe, enabling more targeted and efficient outreach.

### Model Performance

| Model | Train Accuracy | Test Accuracy | Test ROC-AUC | CV ROC-AUC |
|-------|---------------|--------------|-------------|------------|
| Baseline (majority class) | 0.8873 | 0.8873 | 0.500 | — |
| Logistic Regression (Tuned) | 0.9002 | 0.9020 | 0.8015 | 0.7894 ± 0.0063 |
| KNN (Tuned) | 0.9011 | 0.9012 | 0.7835 | 0.7666 ± 0.0077 |
| Decision Tree (Tuned) | 0.9049 | 0.9013 | 0.8043 | 0.7868 ± 0.0030 |
| SVM (Tuned) | 0.8982 | 0.8994 | 0.7308 | 0.7195 ± 0.0090 |

### Recommended Model

**Logistic Regression (Tuned)** is the recommended model. Decision Tree (Tuned) and Logistic Regression (Tuned) are virtually tied on test ROC-AUC (0.8043 vs 0.8015), a difference of only 0.0028. Logistic Regression achieves a marginally higher cross-validation mean (0.7894 vs 0.7868), is more stable, significantly faster to train and score in production, requires fewer hyperparameters to tune, and provides interpretable coefficients that allow the bank to understand and justify predictions.

### Key Actionable Insights

1. **Prioritize clients with prior subscription history** — Clients who successfully subscribed in a previous campaign convert at approximately six times the overall average rate and should be targeted first in future campaigns.
2. **Use cellular contact over telephone** — Cellular contacts convert at a higher rate than telephone contacts. Obtaining cellular numbers for telephone-only clients would improve campaign effectiveness.
3. **Focus campaigns in high-conversion months** — March, September, October, and December produce above-average subscription rates despite lower call volumes. May has the highest call volume but below-average conversion.
4. **Reduce excessive contact attempts** — Clients who subscribed were typically contacted fewer times. Limiting contact attempts per client reduces wasted resources.
5. **Monitor economic conditions** — Lower interest rates and employment variation rates are associated with higher subscription rates. These indicators can help identify periods when clients are more receptive.
6. **Target students and retirees** — Both groups show above-average subscription rates and could benefit from tailored campaign messaging.

### Next Steps

1. **Deploy with probability threshold tuning** — The recommended Logistic Regression model outputs a subscription probability per client. Evaluating different threshold values based on the cost of a wasted call versus the revenue from a successful subscription would allow the bank to align the model with its business priorities.
2. **Real-time scoring pipeline** — Integrating the model into the bank's customer management system would allow agents to see a subscription probability score for each client before making a call, enabling real-time prioritization of outreach.
3. **A/B test model-guided vs. random outreach** — Running a controlled experiment comparing model-guided targeting against traditional methods would validate whether the model delivers measurable improvements in real-world campaign performance.
4. **Address class imbalance** — Applying oversampling techniques or adjusting the model to penalize misclassification of subscribers more heavily could improve the model's ability to identify potential subscribers in future campaigns.
5. **Explore ensemble methods** — Benchmarking more advanced methods such as Random Forest and Gradient Boosting against the current model could reveal whether further performance gains are achievable.
