# 🏦 Loan Default Prediction with XGBoost

## 🎯 Project Goal
To develop a robust and explainable machine learning model capable of accurately predicting credit default risk. This transition from reactive loss absorption to proactive risk management aims to **reduce non-performing assets (NPAs)** and optimize the bank's lending portfolio.

## 📈 Key Results
The final XGBoost model demonstrated exceptional performance metrics on unseen data:

* **Accuracy:** [INSERT FINAL ACCURACY HERE]%
* **Recall (Defaulters Caught):** [INSERT FINAL RECALL HERE]%
* **Business Impact:** The model provides a clear, defensible decision boundary for loan approval, significantly mitigating financial loss.

## 💡 Key Technologies & Methods
| Category | Tool / Method | Purpose |
| :--- | :--- | :--- |
| **Data Engineering** | Pandas, Scikit-learn Pipelines | Data cleaning, imputation, feature scaling, and one-hot encoding. |
| **Modeling** | **XGBoost Classifier**, Logistic Regression (Baseline) | Used the superior performance of XGBoost for prediction while using Logistic Regression for interpretability validation. |
| **Imbalance Handling**| SMOTE (Synthetic Minority Oversampling Technique) | Corrected class imbalance (low frequency of defaults) to ensure fair model training. |
| **Evaluation** | Recall, F1-Score, Confusion Matrix | Prioritized minimizing False Negatives (uncaught defaulters) to protect bank capital. |

## 📁 Repository Structure
The project is organized for clarity and reproducibility:

| Folder / File | Description |
| :--- | :--- |
| `whitepaper.md` | Full technical deep-dive, detailing EDA, methods, and ethical considerations. (Milestone 2 Content) |
| `notebooks/` | Contains the **Exploratory Data Analysis (EDA)** and model experimentation scratchpad. |
| `src/` | Contains the final, production-ready Python script (`loan_predictor.py`). |
| `images/` | **

[Image of Data Science Workflow]
** Contains the overall data flow architecture (ETL, Modeling, Deployment). |
| `results/` | Final output charts, including Confusion Matrix and Feature Importance plots. |

## 🚀 Get Started
1.  Clone this repository.
2.  Install dependencies: `pip install -r requirements.txt`
3.  Run the main script in the `src/` directory to reproduce the results.
