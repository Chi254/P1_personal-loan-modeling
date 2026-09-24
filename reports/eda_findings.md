## 10. Key EDA Findings

### 1. Target Imbalance

The target variable is highly imbalanced.

- Class 0: 4,520 observations
- Class 1: 480 observations
- Class 1 represents approximately 9.6% of the dataset.

**Implication:**  
Accuracy alone may not be sufficient to evaluate the classification
model. Precision, Recall, F1-score and the Confusion Matrix should also
be considered during model evaluation.

---

### 2. Data Quality

No missing values or duplicate rows were identified in the dataset.

**Implication:**  
No basic missing-value imputation or duplicate-row removal is required
at this stage.

---

### 3. Numerical Features

The numerical feature analysis shows that `income`, `ccavg`, and
`mortgage` have relatively wide ranges and contain potential outliers.

The boxplots also show differences between customers who accepted and
did not accept a personal loan. In particular, customers who accepted
the loan generally have higher `income` and `ccavg` values.

`mortgage` also shows differences between the two groups, although both
groups contain many observations with zero mortgage.

**Implication:**  
These variables may contain useful information for the classification
task and should be considered during model development. Their actual
predictive contribution should be evaluated using the models rather
than inferred from EDA alone.

---

### 4. Experience Requires Further Investigation

Negative values were identified in the `experience` variable.

**Implication:**  
These observations should be investigated before preprocessing.
No values are automatically corrected or removed during the EDA stage.

---

### 5. Categorical / Discrete Features

Observed personal-loan acceptance rates vary across several categorical
variables.

The differences are particularly noticeable for `education`, `family`,
and `cd_account`, while `online` and `creditcard` show relatively small
differences.

For `cd_account`, the observed acceptance rate is substantially higher
for customers with a CD account, although this group contains relatively
few observations.

**Implication:**  
These variables should be considered during model development, while
differences in subgroup size should be taken into account.

---

### 6. ZIP Code Requires Further Investigation

`zip_code` contains a relatively large number of unique values.

Rather than removing it immediately, further investigation is needed
to determine whether the ZIP Code can be transformed into meaningful
geographic information.

**Implication:**  
A modeling decision about `zip_code` should be made after investigating
its potential geographic meaning.
