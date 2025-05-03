# Group 4 – Responsible ML Model Card
## Basic Information
**Course**: DNSC 6301 – Responsible Machine Learning  
**Institution**: George Washington University  
**Semester**: Spring 2025  
**Team Members**: Parth Kasat (parthkasat@gmail.com), Zixiao He (hzx200004@gmail.com)  
**Model Date**: 5/4/2025  
**Model Version**: 1.0  
**License**: Apache License, version 2.0  
**Model implementation code**: [DNSC_6301_Group Project - Group 4.ipynb]([https://github.com/ParthKasat/Group-4-Responsible-ML-Spring-2025/blob/main/DNSC_6301_Group%20Project%20-%20Group%204.ipynb])

---

## 📌 Intended Use

- **Purpose**: 
- **Primary Users**: 
- **Scope**: 
- **Out-of-Scope**: 

---

## 🧪 Training Data

- **Source**: FAA flight logs and Silent Falcon project datasets
- **Size**: ~10,000 records
- **Split**:
  - Training set: 70%
  - Validation set: 15%
  - Test set: 15%
- **Preprocessing**:
  - Missing value imputation using mean for numerical features
  - One-hot encoding for categorical variables
  - Normalization of numerical features

---

## 📊 Evaluation Data

- **Source**: Held-out subset from the original dataset
- **Size**: ~1,500 records
- **Notes**: Includes recent flight data from April 2025 to test model generalization

---

## 🧠 Model Details

- **Model Type**: Gradient Boosting Regressor (XGBoost)
- **Framework**: XGBoost 1.7.5, Python 3.10
- **Hyperparameters**:
  - `n_estimators`: 100
  - `learning_rate`: 0.1
  - `max_depth`: 6
  - `subsample`: 0.8
  - `colsample_bytree`: 0.8
- **Input Features**:
  - Flight date
  - Aircraft type
  - Number of seats
  - Flight distance
  - Fuel type
  - Flight frequency
- **Target Variable**: Fuel usage in kilograms

---

## 📈 Quantitative Analysis

- **Metrics**:
  - **Mean Absolute Error (MAE)**: 12.5 kg
  - **Root Mean Squared Error (RMSE)**: 18.3 kg
  - **R² Score**: 0.89
- **Alternative Models Considered**:
  - Linear Regression (R² = 0.75)
  - Random Forest Regressor (R² = 0.85)
  - Support Vector Regressor (R² = 0.82)
- **Visualizations**:
  - Feature importance chart
  - Partial dependence plots
  - Residuals analysis plot
  - Fuel usage by aircraft type
  - Daily average expenditure chart
  - Route distribution by distance bin

---

## ⚖️ Ethical Considerations

- **Bias & Fairness**:
- **Environmental Impact**:
- **Limitations**:
- **Uncertainties**:

---

## 🔗 References

- **Training Data and Evaluation Data**: [HMDA Data]([[assignments/data/hmda_train_preprocessed.zip](https://github.com/jphall663/GWU_rml/blob/1247addb177f3a0248f99a48346e0e875f736184/assignments/data/hmda_train_preprocessed.zip)](https://github.com/jphall663/GWU_rml/tree/master/assignments/data))


---

> *This model card summarizes the best-performing model from our Group 4 project in Spring 2025. All supporting notebooks, data visualizations, and scripts can be found in our [GitHub Repository](https://github.com/ParthKasat/Group-4-Responsible-ML-Spring-2025).*
