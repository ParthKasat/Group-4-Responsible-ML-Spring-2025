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

- **Purpose**: To predict aircraft fuel usage and operational costs for regional airports, facilitating efficient resource allocation and environmental impact assessments.
- **Primary Users**: Airport operations managers, environmental analysts, and aviation policy makers.
- **Scope**: Designed for small to mid-sized regional airports within the United States.
- **Out-of-Scope**: Not intended for international airports or military aviation operations.

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
  - Evaluated performance across aircraft types to ensure fairness
  - No significant disparities observed
- **Environmental Impact**:
  - Helps identify high fuel-consuming routes for potential optimization
- **Limitations**:
  - Does not account for real-time factors (e.g., weather, ATC delays)
  - Relies on potentially noisy or incomplete public datasets
- **Uncertainties**:
  - Aircraft metadata mismatches may impact predictions
  - Assumptions on fuel type-to-weight conversions may vary

---

## 🔗 References

- **Training Data**: [FAA Flight Logs](https://www.faa.gov/data_research/aviation_data_statistics/)
- **Evaluation Data**: [Silent Falcon Dataset](https://github.com/ParthKasat/Group-4-Responsible-ML-Spring-2025)

---

> *This model card summarizes the best-performing model from our Group 4 project in Spring 2025. All supporting notebooks, data visualizations, and scripts can be found in our [GitHub Repository](https://github.com/ParthKasat/Group-4-Responsible-ML-Spring-2025).*
