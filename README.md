# prostate-cancer-heavy-metals-ml
Prostate cancer risk prediction using Random Forest and Logistic Regression on NHANES heavy metal biomarkers with PCA and permutation feature importance.

# 🧪 Prostate Cancer Risk Prediction Using Heavy Metal Exposure (NHANES)

This repository provides a complete and reproducible machine learning pipeline to predict **prostate cancer (PCa) risk** using blood and urine heavy metal biomarkers from the **NHANES** dataset. The project reproduces the methodology and key findings of a published research study using interpretable machine learning techniques.

Author: Mohit Tiwari  


---

## 🎯 Project Goal

To investigate whether **heavy metal biomarkers** (blood & urine), together with demographic factors (age, BMI, income), can predict prostate cancer risk in men aged 45+ using machine learning.

The project emphasizes:

- Scientific reproducibility  
- Transparent preprocessing  
- Dimensionality reduction  
- Robust evaluation  
- Model interpretability  

---

## 📊 Dataset

- **NHANES (National Health and Nutrition Examination Survey)**
- Cycles: 2017–2018 (reproduction), conceptually based on 2003–2018 study
- Participants: 554 men (45+ years) with metal biomarker data
- Features:
  - 26 log-transformed metal biomarkers
  - 3 covariates (age, BMI, income)
  - Total: 29 features before PCA

---

## 🧠 Models Implemented

### Logistic Regression (LR)

Predicts probability of prostate cancer using the sigmoid function:

P(PCa) = 1 / (1 + e^(−(β₀ + β₁x₁ + ... + βₙxₙ)))

Interpretable coefficients indicate direction and magnitude of risk.

---

### Random Forest (RF)

Ensemble of decision trees:

Final Prediction = Majority Vote of All Trees

Captures nonlinear relationships and interactions between metals and demographics.

---

## 🔻 Dimensionality Reduction

### Principal Component Analysis (PCA)

Transforms correlated metal variables into orthogonal components:

PC₁ = w₁₁x₁ + w₁₂x₂ + ... + w₁pxp  
PC₂ = w₂₁x₁ + w₂₂x₂ + ... + w₂pxp

- 17 components retained
- 95.97% variance preserved

### Singular Value Decomposition (SVD)

Matrix factorization:

A = U Σ Vᵀ

Used to validate PCA results.

---

## 🔍 Model Interpretation

### Permutation Feature Importance (PFI)

Measures performance drop when a feature is shuffled:

Importance(xⱼ) = Accuracy_original − Accuracy_shuffled(xⱼ)

Identifies most influential PCA components (feature_6, feature_12, feature_15).

---

## 📈 Evaluation Metrics

- Accuracy  
- Precision  
- Recall  
- F1-score  
- ROC Curve  
- AUC  

AUC interpretation:

- 0.5 → random  
- 0.7–0.8 → acceptable  
- 0.8–0.9 → good  
- 0.9+ → excellent  

---

## 🧪 Reproduction Workflow (Pipeline)

1. Load and merge 15 NHANES datasets using SEQN  
2. Filter men ≥ 45 years  
3. Create PCa label from MCQ220  
4. Retain participants with urine metal data  
5. Missing value imputation (median/mode)  
6. Select true metals and laboratory variants  
7. Clip and log-transform metal values  
8. Assemble 29-feature dataset  
9. Standardization  
10. PCA + SVD → 17 components  
11. Stratified train-test split (70/30)  
12. Handle class imbalance (SMOTE-Tomek or class weights)  
13. Train Random Forest and Logistic Regression  
14. Evaluate using ROC/AUC and classification metrics  
15. Compute permutation feature importance  

---

## 📌 Key Results

| Model | Accuracy | Precision | Recall | F1 |
|-------|----------|-----------|--------|-----|
| Random Forest | 0.85 | 0.67 | 0.08 | 0.14 |
| Logistic Regression | 0.30 | 0.18 | 1.00 | 0.31 |

- Best AUC ≈ **0.68** (moderate discrimination)
- Random Forest outperformed Logistic Regression overall
- Logistic Regression achieved high recall but poor precision
- Prediction remains difficult due to strong class imbalance

---

## 🔬 Scientific Findings

- Heavy metals contain **weak but non-zero predictive signal**
- Demographics (age, BMI, income) contribute strongly
- PCA components represent **combined metal exposure patterns**
- Individual metals alone are insufficient predictors
- Metal biomarkers assist but do not dominate prediction

Consistent with original research:

- Blood lead (Pb), urinary cesium (Cs), urinary antimony (Sb) → higher risk
- Blood cadmium (Cd) → protective association

---

## 🧾 Final Conclusion

This project demonstrates that:

- Heavy metal exposures have limited standalone predictive power
- Combined exposure patterns and demographics provide moderate signal
- Interpretable ML can uncover complex environmental health relationships
- NHANES is suitable for reproducible epidemiological ML research

The pipeline serves as a template for future exposure–disease modeling studies.

---

## 🛠 Technologies Used

- Python  
- Pandas, NumPy  
- Scikit-learn  
- imbalanced-learn  
- Matplotlib, Seaborn  
- Jupyter Notebook  

---

## ⚠ Disclaimer

This project is for academic and research purposes only and does not constitute medical advice or diagnosis.

---

