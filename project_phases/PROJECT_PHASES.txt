# **Project Phases: Bank Personal Loan Campaign Analysis**  

---

## **1. Data Preparation & Cleaning**

- Loaded dataset into pandas.  
- Checked descriptive statistics using `df.describe()` and `df.info()`.  
- Verified class distribution — no missing or empty classes found.  
- Converted **CCAvg (Credit Card Avg)** from string → float.  
- Dropped **ID** (unique) and **ZIP Code** (constant).  
- Binned **Age** into categorical groups of 10s (e.g., 20–29, 30–39).  
- Renamed **Income** and **Mortgage** to represent values in thousands.  
- Converted categorical variables:  
  - **Education:** {1 = Undergrad, 2 = Graduate, 3 = Advanced}  
  - **Personal Loan, Securities Account, CD Account, Online, CreditCard:** {0 = No, 1 = Yes}  

---

## **2. Exploratory Data Analysis (EDA)**

- Plotted **continuous variables** using histograms and boxplots.  
- Plotted **categorical variables** using count plots.  
- Conducted **correlation analysis**:  
  - Correlation matrix (`df.corr()`), heatmap visualization.  
- **Bivariate analysis**: Explored relationships between  
  `Income`, `Experience`, `Mortgage`, `CCAvg` vs `Personal Loan`.  
- **Statistical tests:**  
  - **Chi-Square Test:** Checked association between categorical features and loan acceptance.  
  - **Welch’s t-test:** Tested income difference between loan acceptors and non-acceptors (p ≪ 0.001).  

### **Key Observations:**
- Loan acceptors tend to have **higher income (100K–200K)**.  
- **Education**, **Family size**, and **CD Account** show strong association with loan acceptance.  
- **Online banking** and **CreditCard** usage were less predictive.  

---

## **3. Feature Engineering & Preprocessing**

- Encoded categorical features using one-hot/dummy encoding.  
- Performed **train-test split** (80% training / 20% testing).  
- Applied **StandardScaler** for Logistic Regression (not required for tree-based models).  
- Ensured no data leakage between train and test sets.  

---

## **4. Model Training & Evaluation**

- **Models Trained:**  
  1. Logistic Regression (baseline, interpretable model).  
  2. Random Forest (handles non-linearity, robust).  
  3. XGBoost (boosted trees for performance and recall).  

- **Evaluation Metrics:**  
  - Accuracy  
  - Precision  
  - Recall  
  - F1-Score  
  - ROC-AUC  
  - Confusion Matrix  

- **Hyperparameter Tuning:**  
  - `GridSearchCV` and `RandomizedSearchCV` used for parameter optimization.  
  - For XGBoost: tuned `learning_rate`, `n_estimators`, `max_depth`, `scale_pos_weight`.  

---

## **5. Model Interpretation**

- **Logistic Regression:** Coefficient and **odds ratio** interpretation for feature influence.  
- **Random Forest & XGBoost:** Built-in **feature importance** used to rank predictors.  
- **Permutation Feature Importance:** Assessed impact of individual features independently.  
- **SHAP Values:**  
  - Global: ranked features by overall influence.  
  - Local: explained individual predictions (SHAP waterfall plots).  

---

## **6. Key Findings**

| **Feature** | **Insight** | **Business Meaning** |
|--------------|-------------|----------------------|
| **Income** | Strong positive predictor | Higher income customers more likely to accept loans |
| **Education (Graduate/Advanced)** | ~45–50× higher odds vs. undergrad | Educated customers show stronger trust in financial products |
| **Family Size (3–4)** | Positive association | Indicates mid-life financial planning stage |
| **CD Account** | ~13× higher likelihood | Cross-sell opportunity for existing deposit holders |
| **Online/CreditCard Usage** | Weak influence | Low predictive power; not useful for targeting |

---

## **7. Conclusion**

- **Best Performing Model:** XGBoost (highest recall, precision, and AUC).  
- **Top Predictors:** Income, Education, Family, and CD Account.  
- **Business Summary:**  
  - High-income, well-educated families are key target segments.  
  - CD account holders show the strongest cross-sell potential.  
- **Limitations:** Dataset size and limited behavioral variables.  

---

## **8. Future Work**

- **Pipeline Optimization:** Implement `Pipeline` and `ColumnTransformer` in scikit-learn.  
- **Model Persistence:** Save trained models using `joblib` or `pickle`.  
- **Environment Management:** Use `requirements.txt` or `environment.yml` for reproducibility.  
- **Deployment:**  
  - Develop a **FastAPI** endpoint for real-time predictions (`/predict`).  
  - Integrate **SHAP explanations** into API responses for transparency.  
- **Containerization:** Dockerize the project for seamless deployment.  
- **Monitoring:** Track performance drift and periodically retrain the model.  

---

**Note:**  
This file provides the **technical development summary** of the project.  
For a business-focused overview, refer to [`README.md`](./README.md).  
