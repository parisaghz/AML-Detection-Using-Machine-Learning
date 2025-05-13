# 🕵️‍♀️ AML Detection Using Machine Learning with SHAP Interpretability

This project implements an interpretable machine learning system to detect potential money laundering transactions using a large-scale synthetic financial dataset.

---

## 🎯 Objective

**Can machine learning models accurately identify suspicious transactions in a highly imbalanced dataset, and which model performs best for practical AML monitoring?**

We focus not only on predictive accuracy but also on **transparency**, using **SHAP values** to interpret and validate model decisions.

---

## 📊 Dataset: SAML-D (Synthetic AML Dataset)

- 🔗 [Kaggle Source](https://www.kaggle.com/datasets/berkanoztas/synthetic-transaction-monitoring-dataset-aml)
- 🔢 **9.5M+** transactions
- ⚠️ Only **0.1039%** are labeled as suspicious (extreme class imbalance)

**Features include**:
- Transaction amount, date/time
- Sender/receiver bank location
- Payment and currency type
- Suspicious flag (`is_laundering`)
- Typology classification (e.g., Fan-Out, Structuring)

---

## 🧪 Project Workflow

### 🔍 Exploratory Data Analysis
- Transaction value distributions
- Typology breakdown by country
- Suspicious vs. normal case ratio
- Correlation analysis (none above 0.04 with target)

### 🛠 Feature Engineering
- Time-based: `Hour`, `Day`, `Part_of_Month`
- Geographic: `Different_Country`
- Currency mismatch: `Different_Currency`
- Temporal-laundering indicators via grouped plots

### 🔄 Class Rebalancing
- Applied **class weighting** using `compute_class_weight`
- Class 1 (suspicious) weighted ≈ 481× more than normal

---

## 🤖 Model Development

| Model              | Recall (Class 1) | AUC-ROC | Accuracy | Notes |
|-------------------|------------------|---------|----------|-------|
| Logistic Regression | 54%             | 0.6888  | 75%      | Fast baseline, 0% precision |
| Random Forest       | 5%              | 0.6022  | 100%     | Biased to majority class |
| **XGBoost (final)** | **73%**         | **0.8248** | 76%  | Best recall, threshold tuned to 0.3 |

📌 **XGBoost selected as final model** due to best performance in high-risk use cases.

---

## 🧠 Explainability with SHAP

Used **SHAP (SHapley Additive Explanations)** to interpret XGBoost results:

- `Amount`, `Payment_type`, and `Different_Currency` were most influential
- SHAP summary plots show how features drive predictions
- Enhances transparency for regulated environments

---

## 📁 Repository Structure

```bash
.
├── notebooks/
│   ├── 01_EDA_Cleaning.ipynb
│   ├── 02_Modeling_LogReg_RF_XGBoost.ipynb
│   ├── 03_SHAP_Explainability.ipynb
├── data/
│   └── SAML-D_cleaned.csv
├── docs/
│   ├── AML_Group_Report_2025.pdf
│   └── Appendix_Typologies.pdf
├── presentation/
│   └── AML_Parisa_Presentation.pptx
├── README.md
