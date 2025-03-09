# Kaggle Competition Solution: Predicting Transplant Survival Rates Using Stacked LightGBM

## Overview

This competition focused on predicting post-transplant survival rates for patients undergoing allogeneic Hematopoietic Cell Transplantation (HCT). The task was evaluated using a specialized metric, the **Stratified Concordance Index (C-index)**, designed to assess model performance equitably across racial groups, emphasizing the reduction of disparities in transplant outcomes.

My final solution ranked in the **top 26%** (857/3325), achieving a **private leaderboard score of 0.692**, a significant improvement from my **public leaderboard score of 0.684**. This placed my solution just **0.009 away from the winning score of 0.701** and resulted in a **gain of 1182 positions** in the private rankings.

---

## Solution Approach

### 1. Data Exploration & Preprocessing

The dataset contained both **categorical** and **numerical** variables, with `efs` (event-free survival) and `efs_time` (time to event) as the primary target variables.

- **Missing Value Imputation Strategies:**
  - Categorical features were filled with a placeholder value (`"UNK"`).
  - Numerical features were imputed using a constant value (`-1`).
- **Feature Transformations:**
  - Standardization techniques such as **MinMax Scaling** and **Label Encoding** were applied to normalize data.

---

### 2. Feature Selection & Engineering

The dataset had a **large number of features**, making feature selection crucial for performance optimization.

- **Top-k Feature Selection:**
  - Identified the **top-k feature combinations** that provided the best results based on prior evaluations.
- **Survival Analysis Transformations:**
  - The **Nelson-Aalen estimator** was used to transform the target variable (`efs`), as it provided better predictive stability than the **Kaplan-Meier estimator**.
  - Additional survival-based features were extracted using the **Cox Proportional Hazards Model** and other survival analysis tools to enrich the dataset.

---

### 3. Model Selection & Training

#### **Stacked LightGBM Regressor with Voting**
- The primary model was an **ensemble** of multiple LightGBM regressors trained with different random seeds.
- A **Voting Regressor** was used to aggregate predictions from multiple LightGBM models.
- The Voting Regressor assigned different **weights** to each LightGBM model to optimize predictive performance.

#### **Cross-Validation Strategy**
- Employed **k-fold cross-validation** on each **top-k feature combination**.
- Predictions were generated for each feature combination separately.
- The final prediction was obtained by **averaging all model predictions** across the selected feature sets.

---

### 4. Model Evaluation & Robustness Check

- The **Stratified Concordance Index (C-index)** was used to evaluate model performance, ensuring **fair assessment across racial groups**.
- My approach ensured **robust validation**, as evidenced by the **performance gain on the private leaderboard**. This validated the solution’s **generalizability** and reduced the risk of overfitting to public leaderboard data.

---

## Key Takeaways

- **Feature selection** played a crucial role in boosting the model’s performance.
- A **stacked LightGBM approach** with multiple seeds provided a **more stable and generalizable** prediction.
- **Survival analysis transformations**, particularly using the **Nelson-Aalen estimator**, improved the accuracy of target encoding.
- **Ensemble-based averaging** across top feature sets ensured better **robustness** and reduced the risk of leaderboard overfitting.

This method proved to be effective in handling the complexities of survival analysis while maintaining **fairness in predictions across diverse patient groups**. My final model performed exceptionally well on the **private leaderboard**, reinforcing the **robustness** of my approach.

---

## Repository Structure

- `solution.ipynb`: The Jupyter notebook containing my best leaderboard solution([see on kaggle](https://www.kaggle.com/code/oluwatobibetiku/cibmtr-submission/notebook?scriptVersionId=224469880)).
- `feature_information/`: feature-combination scores.
- `README.md`: This is the README file.

---

## Acknowledgments

Special thanks to the Kaggle community for valuable discussions and resources that helped refine this solution.

---

📢 **If you found this solution useful, consider giving it a ⭐ on GitHub!**
