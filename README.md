#  Loan Risk Classification


---

## Business Problem Statement

Lending institutions face financial risks due to customer defaults. The objective of this project is to build a classification model that accurately flags **risky loan applicants** based on their profile and credit behavior, thereby reducing potential loan defaults.

---

## Dataset Overview

* **Source**: LendingClub

The dataset includes a wide variety of borrower attributes and historical loan performance details. Substantial filtering and feature engineering were applied to create a streamlined dataset for modeling.

---

## Target Definition

* **Safe (0)**: Fully Paid
* **Risky (1)**: Late (31–120 days), Default

Note: The "Charged Off" category was intentionally excluded to focus on more interpretable delinquency patterns.

---

## Data Cleaning & Preparation

* Removed loan statuses like `Current`, `Charged Off`, and rare categories
* Dropped leakage-prone and redundant columns (e.g., `funded_amnt`, `recoveries`, `collection_recovery_fee`)
* Addressed missing values via:

  * Imputation (e.g., with median or domain-specific values)
  * Binary flags indicating missingness for risk capture
* Feature engineering:

  * `credit_age`, `installment_to_income`, `income_to_loan_ratio`
* Outliers were treated using IQR or domain-specific thresholds

---

## Exploratory Data Analysis (EDA)

* Identified imbalance in the target variable
* Explored distributions of key variables like `int_rate`, `dti`, and `emp_length`
* Correlation analysis to avoid multicollinearity and identify signal-rich variables

---

## Model Development

Algorithms implemented:

* Logistic Regression (baseline, with and without SMOTE)
* Random Forest (raw and tuned)
* Balanced Bagging Classifier

Final model: **Tuned Ensemble Model** using Bagging and Random Forest techniques.

### Handling Class Imbalance

* Used **SMOTE** to oversample the minority (risky) class and ensure balanced training

---

## Model Evaluation

Evaluation metrics used:

* **Recall** (Primary focus)
* **ROC AUC**
* **Precision**
* **F1 Score**

The final model demonstrated high recall with acceptable trade-offs, prioritizing the identification of as many risky applicants as possible.

---

## Recommendations & Insights

* The tuned ensemble model is suitable for deployment where recall is more important than precision
* Missing value indicators can serve as risk flags—customers not fully disclosing financial info may be riskier
* Ensemble techniques significantly outperform basic classifiers in this imbalanced setting

---

## Project Assets

The repository contains the following key directories and files:

* `README.md`: Project overview and documentation
* `requirements.txt`: List of Python dependencies
* `data/`: Cleaned dataset (`final_cleaned_dataset.csv`)
* `notebooks/`: Contains Jupyter notebook (`model_pipeline.ipynb`) for complete E2E pipeline
* `src/`: Python scripts for modular tasks:

  * `data_preprocessing.py`
  * `feature_engineering.py`
  * `model_training.py`
  * `evaluation.py`
* `reports/`: Model evaluation report
* `visuals/`: Plots comparing model performance

---

## Summary of Workflow

This project follows a complete CRM pipeline starting from data extraction and cleaning to model building and evaluation. The data was thoroughly preprocessed by removing irrelevant categories and leakage-prone columns, imputing or flagging missing values, and engineering relevant features. Exploratory analysis helped uncover class imbalance and key relationships. Several models were tested with a focus on improving recall, and class imbalance was handled using SMOTE. A tuned ensemble model was finalized based on its ability to identify risky borrowers effectively while maintaining strong performance metrics aligned with business priorities.
