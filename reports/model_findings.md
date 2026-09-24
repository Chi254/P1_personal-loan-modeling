# Model and Evaluation

## 1. Problem Type

# Model Findings

## 1. Modeling Objective

### Business Question

Can customer information be used to predict whether a customer will
accept a personal loan offer?

### ML Problem

This is a supervised binary classification problem.

### Target

`personal_loan`

- `0`: Customer did not accept the loan
- `1`: Customer accepted the loan

### Business Consideration

A False Negative means that a customer who would actually accept the
loan is not identified by the model.

Because the campaign aims to identify potential customers, reducing
False Negatives is the more important consideration.

Therefore, Recall is evaluated alongside Precision and F1-score.

## 2. Evaluation Strategy

The dataset was split into three subsets:

- Training: 60%
- Validation: 20%
- Test: 20%

Stratified splitting was used to preserve the target distribution.

### Role of Each Dataset

| Dataset | Purpose |
|---|---|
| Training | Fit the models |
| Validation | Compare models and select the classification threshold |
| Test | Final evaluation on unseen data |

The test set was not used during model or threshold selection.

### Evaluation Metrics

Because the target is imbalanced, Accuracy is not used as the only
evaluation metric.

The main metrics considered are:

- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC
- Confusion Matrix
  
## 3. Baseline & Model Comparison

### Baseline

A majority-class baseline was established before evaluating the
classification models.

The baseline achieved:

- Accuracy: 90.4%
- Precision: 0%
- Recall: 0%
- F1-score: 0%

### Finding

The baseline shows that a high Accuracy can be achieved by predicting
the majority class, while completely failing to identify positive
customers.

### Implication

Accuracy alone is therefore insufficient for this classification
problem.

### Validation Performance

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Baseline | 90.4% | 0.0% | 0.0% | 0.0% | 0.500 | 0.096 |
| Logistic Regression | 96.2% | 87.2% | 70.8% | 78.2% | 0.964 | 0.855 |
| Decision Tree | 98.0% | 92.2% | 86.5% | 89.2% | 0.978 | 0.915 |
| Random Forest | 98.3% | 98.8% | 83.3% | 90.4% | 0.998 | 0.980 |

### Finding

All three trained models substantially improved over the baseline.

Random Forest showed the strongest overall validation performance
among the evaluated models, particularly in ROC-AUC and PR-AUC.

However, its default threshold of 0.50 produced a Recall of 83.33%.

## 4. Overfitting Check

Training and validation F1-scores were compared to examine whether
model performance decreased on unseen validation data.

| Model | Train F1 | Validation F1 | Gap |
|---|---:|---:|---:|
| Logistic Regression | 0.740 | 0.782 | -0.042 |
| Decision Tree | 0.935 | 0.892 | 0.043 |
| Random Forest | 0.964 | 0.904 | 0.060 |

### Finding

The tree-based models show a higher training F1-score than validation
F1-score.

Random Forest has the largest training-validation gap among the three
models, indicating some degree of overfitting.

However, its validation performance remains strong.

## 5. Business Error Analysis

Two types of prediction errors are particularly relevant.

### False Positive

The model predicts that a customer will accept the loan, but the
customer does not.

Potential impact:
marketing or sales resources may be allocated to a customer who
does not convert.

### False Negative

The model predicts that a customer will not accept the loan, but the
customer actually does.

Potential impact:
a potential customer may be missed.

### Business Implication

Because the campaign objective is to identify potential customers,
False Negatives represent a potential missed opportunity.

Therefore, increasing Recall is an important consideration, while
still maintaining acceptable Precision.

## 6. Threshold Analysis & Model Selection

The default classification threshold of 0.50 was further investigated
because of the business importance of reducing False Negatives.

### Random Forest Threshold Analysis

| Threshold | Precision | Recall | F1 |
|---:|---:|---:|---:|
| 0.20 | 81.42% | 95.83% | 88.04% |
| 0.25 | 88.24% | 93.75% | 90.91% |
| 0.30 | 90.91% | 93.75% | 92.31% |
| 0.35 | 94.62% | 91.67% | 93.12% |
| 0.50 | 98.77% | 83.33% | 90.40% |

### Finding

Lowering the threshold increases Recall while reducing Precision.

Compared with the default threshold of 0.50:

- Recall increases from 83.33% to 93.75%.
- Precision decreases from 98.77% to 90.91%.
- F1-score increases from 90.40% to 92.31%.

### Decision

A threshold of 0.30 was selected as the candidate configuration.

The selection was based on the validation set and the business
consideration of reducing False Negatives.

This should not be interpreted as a universally optimal threshold.
A formal cost-based threshold would require quantified business costs
for False Positives and False Negatives.

### Final Candidate

Model: Random Forest

Threshold: 0.30

## 7. Final Test Evaluation

After selecting the Random Forest with a threshold of 0.30 using the
validation set, the final configuration was evaluated on the
previously unseen test set.

### Final Test Performance

| Metric | Score |
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

### Interpretation

The model correctly identified 92 of the 96 customers who actually
accepted the loan.

There were:

- 4 False Negatives
- 13 False Positives

- ## 8. Conclusion

The modeling process followed a business-driven supervised learning
workflow:

Business Problem
→ Evaluation Strategy
→ Baseline
→ Model Comparison
→ Error Analysis
→ Threshold Analysis
→ Final Test Evaluation

The target imbalance made Accuracy insufficient as a standalone metric.

Random Forest showed strong validation performance and was selected
for further threshold analysis.

A threshold of 0.30 was selected based on validation performance and
the business consideration of reducing False Negatives.

On the previously unseen test set, the final configuration achieved:

- Recall: 95.83%
- Precision: 87.62%
- F1-score: 91.54%

The test confusion matrix contained 4 False Negatives and 13 False
Positives.

The main limitation is that the business costs of False Positives and
False Negatives were not quantitatively specified. Therefore, the
threshold selection is a validation-based business consideration
rather than a formal cost optimization.
