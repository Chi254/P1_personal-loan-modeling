# P1_personal-loan-modeling
A supervised learning project for predicting personal loan acceptance

## 1. Project Overview

This project is a supervised machine learning project that predicts
whether a bank customer will accept a personal loan offer.

The project focuses on building a complete binary classification
workflow, from understanding the business problem and exploring the
data to model evaluation and final test performance.

### Project Type
- Learning task: Supervised Learning
- Problem type: Binary Classification
- Target variable: `personal_loan`
- Positive class: Customer accepts the personal loan
- Negative class: Customer does not accept the personal loan

- ## Business Problem

The bank wants to identify customers who are more likely to accept
a personal loan offer.

The model is intended to support the identification of potential
customers for a personal loan campaign.

### 2. Business Question

Can customer information be used to predict whether a customer
will accept a personal loan offer?

### Prediction Errors
Two types of errors are important:
- False Positive: The model predicts that a customer will accept
  the loan, but the customer does not.
- False Negative: The model predicts that a customer will not accept
  the loan, but the customer actually does.
For this campaign, a False Negative represents a potential missed
customer opportunity.

-> Therefore, Recall is considered an important metric alongside
Precision and F1-score.

## 3. Dataset

The dataset contains customer-level information related to personal
loan campaign decisions.

### Target Variable

`personal_loan`

- `0`: Customer did not accept the loan
- `1`: Customer accepted the loan

### Dataset Characteristics

The target variable is imbalanced:

- Class 0: 4,520 customers
- Class 1: 480 customers
- Positive class: approximately 9.6%

Because of this imbalance, accuracy alone is not sufficient to
evaluate model performance.

Precision, Recall, F1-score, ROC-AUC and PR-AUC are considered during
model evaluation.

## 4. Approach

The project follows the following workflow:

Business Problem
→ Data Understanding
→ Data Quality Check
→ Exploratory Data Analysis
→ Train / Validation / Test Split
→ Baseline Model
→ Preprocessing
→ Model Comparison
→ Overfitting Check
→ Threshold Analysis
→ Final Test Evaluation
→ Conclusion

### Data Preparation

The dataset was divided into:

- 60% Training set
- 20% Validation set
- 20% Test set

Stratified splitting was used to preserve the class distribution
across the three datasets.

The test set was kept separate from model and threshold selection
and was used only for final evaluation.

### Models

Three classification models were evaluated:

1. Logistic Regression
2. Decision Tree
3. Random Forest

## 5. Model Evaluation

### Baseline

A majority-class baseline was established before training the
classification models.

The baseline achieved:

- Accuracy: 90.4%
- Precision: 0%
- Recall: 0%
- F1-score: 0%

This demonstrates why accuracy alone is not sufficient for this
imbalanced classification problem.
### Validation Performance

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Baseline | 90.4% | 0.0% | 0.0% | 0.0% | 0.500 | 0.096 |
| Logistic Regression | 96.2% | 87.2% | 70.8% | 78.2% | 0.964 | 0.855 |
| Decision Tree | 98.0% | 92.2% | 86.5% | 89.2% | 0.978 | 0.915 |
| Random Forest | 98.3% | 98.8% | 83.3% | 90.4% | 0.998 | 0.980 |

### 6. Threshold Analysis

The default classification threshold of 0.50 was further investigated
because the campaign places importance on reducing False Negatives.

For the Random Forest:

| Threshold | Precision | Recall | F1 |
|---:|---:|---:|---:|
| 0.20 | 81.42% | 95.83% | 88.04% |
| 0.25 | 88.24% | 93.75% | 90.91% |
| 0.30 | 90.91% | 93.75% | 92.31% |
| 0.35 | 94.62% | 91.67% | 93.12% |
| 0.50 | 98.77% | 83.33% | 90.40% |

Lowering the threshold increases Recall but decreases Precision.

A threshold of 0.30 was selected as the candidate configuration
because it provides higher Recall than the default threshold while
maintaining Precision above 90% on the validation set.

The threshold was selected using the validation set only.

## 7. Final Result

The final candidate configuration was:

- Model: Random Forest
- Classification threshold: 0.30

The model was then evaluated once on the previously unseen test set.

### Final Test Performance

| Metric | Test Score |
|---|---:|
| Accuracy | 98.30% |
| Precision | 87.62% |
| Recall | 95.83% |
| F1-score | 91.54% |
| ROC-AUC | 99.86% |
| PR-AUC | 98.80% |

### Confusion Matrix

| | Predicted 0 | Predicted 1 |
|---|---:|---:|
| Actual 0 | 891 | 13 |
| Actual 1 | 4 | 92 |

The model correctly identified 92 of the 96 customers who actually
accepted the loan.

There were 4 False Negatives and 13 False Positives on the test set.

## 8. Conclusion

This project demonstrated a complete supervised binary classification
workflow for predicting personal loan acceptance.

The main findings were:

1. The target variable was highly imbalanced, making accuracy alone
   insufficient for model evaluation.

2. Logistic Regression, Decision Tree and Random Forest were compared
   using multiple evaluation metrics.

3. Random Forest showed strong validation performance.

4. Threshold analysis demonstrated the trade-off between Precision
   and Recall.

5. A threshold of 0.30 was selected for the Random Forest based on
   validation performance and the business consideration of reducing
   False Negatives.

6. On the previously unseen test set, the final configuration achieved
   95.83% Recall and 91.54% F1-score.

The final test result should be interpreted as an evaluation of this
dataset and modeling setup rather than a guarantee of future campaign
performance.

### 9. Limitations

- The business costs of False Positives and False Negatives were not
  quantitatively specified.
- Therefore, the threshold of 0.30 was selected based on validation
  performance and qualitative business consideration rather than a
  formal cost-based optimization.
- ZIP Code was identified as a potentially useful geographic feature,
  but geographic transformation was not fully developed in this
  project.
- Model performance was evaluated on this dataset and may not directly
  generalize to future customer populations.

### 10. Next Steps

- Quantify the business cost of False Positives and False Negatives.
- Use business costs to determine an appropriate classification
  threshold.
- Further investigate the geographic information contained in ZIP Code.
- Validate the model on future or external customer data.
