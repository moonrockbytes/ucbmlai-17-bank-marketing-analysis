# Required Assignment 17.1: Comparing Classifiers

**Author:** Rakesh Chandrasekaran
**Course:** Professional Certificate in ML and AI
**Module:** 17 — Comparing Classifiers

---

## Overview

This project compares the performance of four classification algorithms — K-Nearest Neighbors (KNN), Logistic Regression, Decision Trees, and Support Vector Machines (SVM) — on a real-world bank marketing dataset. The goal is to identify the best model for predicting whether a client will subscribe to a term deposit following a phone-based marketing campaign.

**Dataset:** UC Irvine Machine Learning Repository — Bank Marketing Dataset (Portuguese banking institution, 2008–2010)

---

## Jupyter Notebook

[bank_marketing_analysis.ipynb](bank_marketing_analysis.ipynb)

---

## Project Structure

```
Module 17/
├── bank_marketing_analysis.ipynb   — Main Jupyter Notebook
├── README.md               — Project summary (this file)
├── data/
│   ├── raw/                — Original unprocessed dataset
│   │   ├── bank-additional-full.csv
│   │   ├── bank-additional.csv
│   │   └── bank-additional-names.txt
│   └── processed/          — Cleaned and encoded dataset
│       ├── bank_encoded.csv
│       ├── bank_features.csv
│       └── bank_target.csv
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
**Logistic Regression (Tuned)** is the recommended model. While the Decision Tree achieves a marginally higher test ROC-AUC (0.8043 vs 0.8015), the difference of 0.0028 is not practically significant. Logistic Regression achieves a higher cross-validation mean (0.7894 vs 0.7868), is more stable, faster to deploy, requires fewer hyperparameters, and provides interpretable coefficients that allow the bank to understand and justify predictions.

### Key Actionable Insights

1. **Prioritize clients with prior subscription history** — Clients who successfully subscribed in a previous campaign convert at approximately six times the overall average rate and should be targeted first in future campaigns.
2. **Use cellular contact over telephone** — Cellular contacts convert at a higher rate than telephone contacts. Obtaining cellular numbers for telephone-only clients would improve campaign effectiveness.
3. **Focus campaigns in high-conversion months** — March, September, October, and December produce above-average subscription rates despite lower call volumes. May has the highest call volume but below-average conversion.
4. **Reduce excessive contact attempts** — Clients who subscribed were typically contacted fewer times. Limiting contact attempts per client reduces wasted resources.
5. **Monitor economic conditions** — Lower interest rates and employment variation rates are associated with higher subscription rates. These indicators can help identify periods when clients are more receptive.
6. **Target students and retirees** — Both groups show above-average subscription rates and could benefit from tailored campaign messaging.

### Next Steps
1. Evaluate different prediction thresholds based on the cost of a wasted call versus the revenue from a successful subscription.
2. Integrate the model into the bank's customer management system for real-time client scoring before calls.
3. Run a controlled A/B test comparing model-guided targeting against traditional outreach methods.
4. Apply oversampling techniques to address class imbalance and improve identification of potential subscribers.
5. Benchmark ensemble methods such as Random Forest and Gradient Boosting for potential performance gains.
