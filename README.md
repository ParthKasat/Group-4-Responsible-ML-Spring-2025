# Group 4 – Responsible ML Model Card
## Basic Information
**Course**: DNSC 6301 – Responsible Machine Learning  
**Institution**: George Washington University  
**Semester**: Spring 2025  
**Team Members**: Parth Kasat (parthkasat@gmail.com), Zixiao He (hzx200004@gmail.com)  
**Model Date**: 5/4/2025  
**Model Version**: 1.0  
**License**: Apache License, version 2.0  
**Model implementation code**: [DNSC_6301_Group Project - Group 4.ipynb](https://github.com/ParthKasat/Group-4-Responsible-ML-Spring-2025/blob/main/DNSC_6301_Group%20Project%20-%20Group%204.ipynb)

---

## 📌 Intended Use

### 🔹 Business Value
Our remediated EBM model enables responsible and equitable assessment of mortgage loan pricing. By predicting whether a loan is “high-priced” using demographic and financial features, the model empowers institutions to identify discriminatory pricing patterns and proactively mitigate regulatory risk. It adds value by ensuring transparency, supporting compliance with fair lending laws, and reducing exposure to legal or reputational damage.

### 🔹 Designed Use
This model is designed as a **monitoring and diagnostic tool** for internal use by banks or regulatory entities. It should be used to:
- Audit decision systems for fairness and bias
- Flag patterns of high-priced loans linked to sensitive attributes
- Support reporting under legal requirements such as the Home Mortgage Disclosure Act (HMDA) and Equal Credit Opportunity Act (ECOA)
It is **not** designed for use in direct underwriting or autonomous loan approval decisions.

### 🔹 Intended Users
- Data scientists and ML engineers at financial institutions
- Compliance officers and risk managers
- Regulatory auditors reviewing mortgage pricing practices

### 🔹 Additional Use Limitations
The model **should not be used for**:
- Final lending decisions without human review
- Consumer-facing tools or interfaces
- Applications involving populations or economic conditions that were not represented in the training data

---

## 🧪 Training Data

- **Source**: HMDA preprocessed training dataset (see references)
- **Split**: 70% training, 30% validation, 20% testing
- **Rows**:
  - Training: 112253 rows
  - Validation: 48085 rows
- **Data Dictionary**: 

---

## 📊 Evaluation Data

- **Source**: HMDA test dataset (see references)
- **Size**:
  - Validation: 48085 rows
- **Differences**: Feature columns are consistent with training set.

---

## ⚙️ Model Details

- **Input Features**: ``,``Engineered and preprocessed features excluding leakage columns.
- **Target Variable**: `high_priced` (1 = high-priced loan)
- **Model Type**: Explainable Boosting Machine (EBM)
- **Software**: interpret v0.2.7, scikit-learn v1.1.1
- **Hyperparameters**:
  - `max_bins`: 256
  - `n_estimators`: 100
  - `learning_rate`: 0.1
  - `max_depth`: 6
  - `subsample`: 0.8
  - `colsample_bytree`: 0.8

---

## 📊 Quantitative Analysis

| Dataset      | AUC   | AIR (Black) | AIR (Female) |
|--------------|-------|-------------|--------------|
| Training     | 0.843 | 0.91        | 0.94         |
| Validation   | 0.837 | 0.92        | 0.96         |
| Test         | 0.834 | 0.89        | 0.93         |

### Plots

- 📈 Global Feature Importance (Assignment 2)
- 📈 Partial Dependence: `loan_amount`, `interest_rate`, `race_black`, `sex_female`
- 📉 AIR vs Threshold plots (Assignment 3 & 4)
- 🔍 Fairness vs Performance tradeoff heatmaps (Assignment 5)
- 🧪 Stress Test under Recession Conditions (Assignment 5)

### Alternative Models Considered

- **GLM**: Comparable AUC, less interpretable.
- **XGBoost**: Higher complexity, fairness concerns.
- **Decision Tree**: Overfit under stress.
- ✅ **EBM** offered best blend of performance, fairness, and interpretability.

---

## ⚠️ Ethical Considerations

### 🔹 Potential Negative Impacts

**Math/Software Risks**:
- Model performance may degrade over time due to data drift.
- Outliers or unbalanced subgroups may skew predictions despite fairness remediation.
- Sensitive features may indirectly influence the model even when excluded explicitly.

**Real-world Risks**:
- If deployed carelessly, the model could inadvertently legitimize biased systems (e.g., reinforcing historical disparities).
- Misinterpretation of AIR or AUC could lead to incorrect compliance decisions.
- Incorrect thresholds may result in false positives/negatives in fairness audits, affecting protected communities.

### 🔹 Uncertainties

**Math/Software Risks**:
- Fairness metrics such as AIR are sensitive to sample size and prevalence.
- The model's generalizability outside of the training domain (e.g., different years or regions) is untested.
- Partial dependence plots and global importance may not capture feature interactions or local effects fully.

**Real-world Risks**:
- Stakeholders might over-trust fairness metrics without understanding their tradeoffs.
- Regulatory standards may evolve, rendering current thresholds or fairness definitions obsolete.
- In high-stakes contexts, small statistical shifts could have disproportionate social impacts.

### 🔹 Unexpected Results

- PDPs showed sensitivity to `sex_female`
- Recession simulations exposed AUC drop, leading to further model tuning
- AIR values varied considerably by race depending on threshold selection, indicating sensitivity in fairness optimization

---

## 🔗 References

- **Training Data and Evaluation Data**: [HMDA Data](https://github.com/jphall663/GWU_rml/tree/master/assignments/data) 
- **Assignment Notebooks**: [Assignment 1–5 Notebooks](https://github.com/ParthKasat/Group-4-Responsible-ML-Spring-2025) 

---

> *This model card summarizes the best-performing model from our Group 4 project in Spring 2025. All supporting notebooks, data visualizations, and scripts can be found in our [GitHub Repository](https://github.com/ParthKasat/Group-4-Responsible-ML-Spring-2025).*
