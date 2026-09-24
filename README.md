# P1_personal-loan-modeling
A supervised learning project for predicting personal loan acceptance

## Project Overview

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

### Business Question

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
