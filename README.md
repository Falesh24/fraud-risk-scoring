# Fraud Risk Scoring & Transaction Monitoring System

An end-to-end machine learning system for identifying potentially fraudulent financial transactions and converting model predictions into actionable risk decisions.

## Overview

Financial fraud detection is not simply a binary classification problem. A practical risk system must identify suspicious behaviour, quantify risk, manage false positives, and support operational decisions.

This project develops a **fraud risk scoring and transaction monitoring system** that analyses transaction and behavioural signals to:

* Detect potentially fraudulent transactions
* Generate a transaction-level risk score
* Classify transactions into risk categories
* Support **Approve / Review / Decline** decisions
* Explain individual predictions using SHAP
* Provide an extensible foundation for real-time fraud monitoring

## Problem Statement

Build a machine learning-based risk engine capable of distinguishing legitimate financial transactions from fraudulent activity while considering the highly imbalanced nature of fraud data and the business cost of incorrect decisions.

## System Architecture

```text
Transaction Data
       │
       ▼
Data Validation & Exploration
       │
       ▼
SQL Analytics
       │
       ▼
Behavioural Feature Engineering
       │
       ├── Transaction Velocity
       ├── Amount Behaviour
       ├── Account Behaviour
       ├── Transaction Type
       └── Balance Patterns
       │
       ▼
Fraud Risk Model
       │
       ▼
Fraud Probability
       │
       ▼
Risk Scoring Engine
       │
       ├── LOW      → APPROVE
       ├── MEDIUM   → REVIEW
       └── HIGH     → DECLINE
       │
       ▼
SHAP Explainability
       │
       ▼
Monitoring Dashboard
```

## Dataset

This project uses the **PaySim Synthetic Financial Dataset for Fraud Detection**.

The dataset is not included in this repository because of its size.

### Download

[**PaySim Dataset — Kaggle**](https://www.kaggle.com/datasets/ealaxi/paysim1)

After downloading the dataset, place the CSV file inside:

```text
data/
```

Please refer to the original dataset page for licensing and attribution information.

## Key Features

### Transaction-level signals

* Transaction amount
* Transaction type
* Origin account balance
* Destination account balance
* Balance changes

### Behavioural signals

The project extends the raw dataset with derived behavioural features such as:

* Transaction frequency
* Transaction velocity
* Amount deviation
* Account transaction patterns
* Balance inconsistencies
* Unusual transaction behaviour

## Machine Learning

The primary model is based on **gradient-boosted decision trees**.

Model development focuses on:

* Highly imbalanced classification
* Precision and recall trade-offs
* PR-AUC
* F1 score
* Confusion matrix analysis
* Threshold optimisation
* Business-cost-aware evaluation

Accuracy is deliberately not treated as the primary success metric because fraud represents a small proportion of overall transactions.

## Risk Scoring

Instead of returning only a binary fraud prediction, the model produces a probability-based risk score.

```text
Risk Score
    │
    ├── Low Risk
    ├── Medium Risk
    └── High Risk
```

The thresholds are selected based on model performance and the operational trade-off between:

* Missing fraudulent transactions
* Incorrectly flagging legitimate customers

## Explainable AI

**SHAP (SHapley Additive exPlanations)** is used to explain model predictions.

For an individual high-risk transaction, the system can identify contributing factors such as:

```text
High transaction amount       ↑
Unusual transaction behaviour ↑
Abnormal balance movement     ↑
Transaction pattern           ↑
```

This makes the model more interpretable for analysts and risk teams.

## Technology Stack

| Component        | Technology            |
| ---------------- | --------------------- |
| Programming      | Python                |
| Data Analysis    | Pandas, NumPy         |
| SQL              | PostgreSQL            |
| Machine Learning | Scikit-learn, XGBoost |
| Explainability   | SHAP                  |
| Visualisation    | Matplotlib, Seaborn   |
| Dashboard        | Streamlit             |
| API              | FastAPI               |
| Version Control  | Git / GitHub          |

## Project Structure

```text
fraud-risk-scoring/
│
├── data/
│   └── .gitkeep
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_feature_engineering.ipynb
│   └── 03_model_development.ipynb
│
├── src/
│   ├── data/
│   ├── features/
│   ├── models/
│   ├── scoring/
│   └── monitoring/
│
├── models/
│
├── dashboard/
│
├── README.md
├── requirements.txt
└── .gitignore
```

## Results

Results will be added after model development.

| Metric    | Score |
| --------- | ----: |
| PR-AUC    |   TBD |
| Precision |   TBD |
| Recall    |   TBD |
| F1 Score  |   TBD |

## Future Extensions

The system is intentionally designed to be extendable.

Potential extensions include:

* Real-time transaction scoring
* Streaming transaction pipelines
* Customer-level risk profiles
* Merchant risk scoring
* Anomaly detection
* Model drift monitoring
* Automated model retraining
* Human-in-the-loop fraud review
* Real-time API deployment
* Advanced graph-based fraud detection

## Disclaimer

This project uses synthetic financial transaction data for educational and portfolio purposes. It is not intended for making real financial or credit decisions.

## Author

**Falesh Kumar Sahu**

B.Tech — Computer Science & Engineering (Data Science)
