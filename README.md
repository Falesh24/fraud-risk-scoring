# Fraud Risk Scoring

An XGBoost-based fraud detection system for identifying and prioritising suspicious financial transactions using transaction and balance behaviour.

## Business Problem

Financial fraud detection is a highly imbalanced classification problem where fraudulent transactions represent only a small fraction of total transactions.

The goal of this project is to build a machine learning system that can identify fraudulent transactions while minimising false positives and prioritise high-risk transactions for further investigation.

## Project Overview

This project uses XGBoost to detect fraudulent financial transactions.

The workflow includes:

- Exploratory data analysis
- Fraud distribution and transaction-type analysis
- Transaction and balance feature engineering
- Chronological train/validation/test splitting
- Baseline model development
- XGBoost model development
- Precision-recall based threshold optimisation
- SHAP-based model explainability
- Business interpretation and recommendations

## Dataset

The project uses a financial transaction dataset containing transaction details, account balances, transaction types, and fraud labels.

The dataset is highly imbalanced, with fraudulent transactions representing only a small fraction of all transactions.

The dataset is not included in this repository due to its size.

## Methodology

The project follows a chronological modelling workflow to better reflect future transaction prediction.

1. Exploratory data analysis
2. Feature engineering
3. Time-based train/test split
4. Baseline XGBoost model
5. Engineered XGBoost model
6. Validation-based threshold optimisation
7. Final evaluation on a held-out future test period
8. SHAP-based model interpretation

## Feature Engineering

Several transaction-level features were engineered to capture abnormal balance behaviour, including:

- Balance changes in the originating and destination accounts
- Transaction amount relative to the originating balance
- Origin and destination balance inconsistencies
- Zero-balance indicator
- Hour, day, and night-time indicators

These features were designed to capture transaction behaviour that may be associated with fraudulent activity.

## Model & Evaluation

XGBoost was used as the primary classification model because it performs well on structured tabular data and can capture non-linear relationships between transaction features.

Due to the severe class imbalance, model performance was evaluated using precision, recall, F1 score, and Average Precision rather than accuracy alone.

The classification threshold was optimised using a separate validation period, while the final performance was measured on an unseen future test period.

## Results

The final model achieved the following results on the held-out future test period:

| Metric | Result |
|---|---:|
| Precision | 100.00% |
| Recall | 99.93% |
| F1 Score | 99.96% |
| Average Precision (PR-AUC) | 99.96% |
| False Positives | 0 |
| False Negatives | 3 |

The model detected 4,247 of 4,250 fraudulent transactions while producing no false positives on the test set.

## Explainability

SHAP was used to understand which features contributed most strongly to the model's predictions.

The model relied primarily on balance-related features and transaction-to-balance relationships, particularly:

- Amount-to-balance ratio
- Originating account balance
- Balance changes
- Balance inconsistencies

This provides insight into the transaction characteristics associated with higher fraud risk.

## Business Interpretation

The model can be used as a post-transaction fraud risk scoring system to prioritise suspicious transactions for investigation.

Potential business applications include:

- Prioritising high-risk transactions for manual review
- Ranking transactions by predicted fraud probability
- Adjusting decision thresholds based on the cost of false positives and false negatives
- Monitoring model performance as transaction behaviour changes
- Periodically retraining the model with newer transaction data

## Limitations

- The dataset is synthetic and may not fully represent real-world fraud patterns.
- The model uses post-transaction balance information, so it is framed as a post-transaction fraud detection system rather than a pre-authorisation system.
- Fraud patterns may change over time, requiring ongoing performance monitoring and model retraining.

## How to Run

1. Clone the repository.
2. Install the required dependencies:

```bash
pip install -r requirements.txt
3. Place the dataset in the data/ directory.
4. Open notebooks/fraud_detection.ipynb.
5. Run the notebook from start to finish.

## Project Structure

```text
fraud-risk-scoring/
├── data/
├── notebooks/
│   └── fraud_detection.ipynb
├── README.md
├── requirements.txt
└── .gitignore
