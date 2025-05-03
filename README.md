# Group 4 – Responsible ML Model Card
## Basic Information
**Course**: DNSC 6301 – Responsible Machine Learning  
**Institution**: George Washington University  
**Semester**: Spring 2025  
**Team Members**: Parth Kasat (parthkasat@gmail.com), Zixiao He (hzx200004@gmail.com)  
**Model Date**: 5/4/2025  
**Model Version**: 1.0  
**License**: Apache License, version 2.0  
**Model implementation code**: [DNSC_6301_Group Project - Group 4.ipynb](https://colab.research.google.com/drive/1MVRKWiOjqXC3my-fu-PPiSBPm2Cj6Xdo?usp=sharing)

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

- **Input Features**:  
  ```python
  [
    "property_value_std",
    "no_intro_rate_period_std",
    "loan_amount_std",
    "income_std",
    "conforming",
    "intro_rate_period_std",
    "debt_to_income_ratio_std",
    "term_360"
  ]
- **Target Variable**: `high_priced` (1 = high-priced loan)
- **Model Type**: Explainable Boosting Machine (EBM)
- **Software**: interpret v0.2.7, scikit-learn v1.1.1
- **Hyperparameters**:
  ```python
  {
    "max_bins": 128,
    "max_interaction_bins": 16,
    "interactions": 10,
    "outer_bags": 8,
    "inner_bags": 4,
    "learning_rate": 0.01,
    "validation_size": 0.25,
    "min_samples_leaf": 1,
    "max_leaves": 3,
    "n_jobs": 4,
    "early_stopping_rounds": 100,
    "random_state": 12345
  }


---

## 📊 Quantitative Analysis

| Dataset      | AUC   | AIR (Black) | AIR (Female) |
|--------------|-------|-------------|--------------|
| Training     | 0.843 | 0.91        | 0.94         |
| Validation   | 0.837 | 0.92        | 0.96         |
| Test         | 0.834 | 0.89        | 0.93         |

### Plots
- 📈 Best Model Feature Importance: ![image](https://github.com/user-attachments/assets/a8571bf8-ae9c-4a14-b810-64550a0a8d67)

- 📈 Global Feature Importance: ![image](https://github.com/user-attachments/assets/dc0b123f-18dc-4202-b702-8bc63f24b437)

- 📈 Partial Dependence: ![image](https://github.com/user-attachments/assets/dac3d835-0c68-4a66-9058-c5461131fb90)
![image](https://github.com/user-attachments/assets/a55d2b7d-637a-4541-a517-3db432a57053)
![image](https://github.com/user-attachments/assets/6ecee0a6-6bfb-48c1-a2b8-874c5a62a400)
![image](https://github.com/user-attachments/assets/5df602a8-e14a-4219-9492-09a8ea813ec7)
![image](https://github.com/user-attachments/assets/425bc1b1-5600-4c74-8df3-31cc2724a440)
![image](https://github.com/user-attachments/assets/aca6be7b-16c2-4810-921c-71af16d8bc13)
![image](https://github.com/user-attachments/assets/eb1fd4b8-6e36-4116-8ca9-ecc4ab9602a2)
![image](https://github.com/user-attachments/assets/0b496420-d419-43de-86c4-1c7701f1face)
![image](https://github.com/user-attachments/assets/835515f6-f1cf-4f9f-b2d7-033ef2b5bbce)
![image](https://github.com/user-attachments/assets/c1377113-43e9-4a14-8d00-bbfb855ac22d)

- 📉 Stolen  Model: ![image](https://github.com/user-attachments/assets/91725331-c174-4694-8735-3b7336533c87)

- 🔍 Global Logross Residuals: ![image](https://github.com/user-attachments/assets/a98bb427-61c1-4dcd-b0ae-48989d5f1133)

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
