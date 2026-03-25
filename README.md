# 📉 Customer Churn Prediction using Logistic Regression

## 📌 Overview

* This project focuses on predicting whether a customer will churn using a **binary classification model**. 
* The primary objective is not just prediction accuracy, but minimizing **False Negatives (missed churners)**, as they represent potential revenue loss.

The project emphasizes **model evaluation, decision strategy, and business-driven optimization** rather than just model training.

---

## 🎯 Problem Statement

Predict whether a customer will churn or not, with a focus on:

* Reducing **False Negatives (FN)**
* Maximizing **Recall for churn class**
* Balancing trade-off between **Precision and Recall**

---

## 📊 Dataset & EDA

* Dataset contains customer-related features (demographics, usage, etc.)
* Churn rate: **26.5%** → moderately imbalanced dataset

### Key Observations:

* Class imbalance makes **accuracy unreliable**
* Need for alternative evaluation metrics like **Recall, Precision, ROC-AUC**

---

## ⚙️ Data Preprocessing

* Handled categorical variables using encoding
* Applied feature scaling for numerical features
* Used **stratified train-test split** to preserve class distribution

---

## 🤖 Model: Logistic Regression

A baseline **Logistic Regression model** was trained to:

* Provide interpretability
* Establish a strong baseline before complex models

---

## 📉 Initial Evaluation

* Accuracy: ~80%
* Recall (Churn): **0.55**
* False Negatives: **170**

### ❗ Insight:

High accuracy was misleading due to class imbalance.
Model was missing ~45% of churners → unacceptable.

---

## ⚖️ Handling Class Imbalance

### Approach 1: Class Weights

Used:

```
class_weight = 'balanced'
```

**Effect:**

* Recall improved to **0.78**
* False Negatives reduced to **83**
* False Positives increased significantly

### Insight:

Model prioritized minority class by penalizing FN more.

---

## 🎯 Threshold Tuning (Key Highlight)

Instead of relying on default threshold (0.5), decision boundary was adjusted.

### Tradeoff Analysis:

| Threshold | FN  | Recall | FP  |
| --------- | --- | ------ | --- |
| 0.50      | 170 | 0.55   | 116 |
| 0.30      | 97  | 0.74   | 253 |
| 0.25      | 79  | 0.79   | 298 |
| 0.20      | 53  | 0.86   | 360 |

### Key Insight:

* Lower threshold → higher recall, lower FN
* But increases FP (business tradeoff)

### 🔥 Important Finding:

Threshold tuning achieved **similar performance to class weighting** without modifying model training.

---

## 📈 Model Evaluation

### 🔹 ROC-AUC Curve

* ROC-AUC Score: **0.84**

**Interpretation:**
Model has strong ability to distinguish churn vs non-churn.

---

### 🔹 Precision-Recall Curve

* Average Precision: **0.63**
* Baseline: **0.265**

**Interpretation:**
Model performs significantly better than random and maintains reasonable precision-recall tradeoff.

---

## 🧠 Key Insights

* Accuracy is misleading in imbalanced datasets
* Recall is critical when missing positives is costly
* Threshold tuning is a powerful alternative to class weighting
* ROC-AUC validates model capability (ranking)
* PR curve helps understand tradeoff under imbalance

---

## 📌 Final Conclusion

* Logistic Regression is sufficient for this problem
* Model has strong ranking ability (ROC-AUC 0.84)
* Performance depends more on **threshold selection** than model complexity
* Optimal threshold should be chosen based on **business cost tradeoff**

---

## 🛠️ Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* Matplotlib

---

## 🚀 Key Takeaways

* Learned to evaluate models beyond accuracy
* Understood tradeoff between precision and recall
* Applied threshold tuning for business-driven decisions
* Built a complete ML pipeline from EDA to evaluation

---

## 🔮 Future Improvements

* Compare with tree-based models (Random Forest, XGBoost)
* Perform cross-validation for robustness
* Implement cost-based threshold optimization
* Deploy model as an API or dashboard

---
