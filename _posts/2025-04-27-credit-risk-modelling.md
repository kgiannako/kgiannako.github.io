---
title: "Credit Risk Prediction Using Machine Learning"
date: 2025-04-27
categories: [Finance, Machine Learning]
---

### Summary
Developed a machine learning model to predict the probability of loan default based on borrower features such as income, interest rate, credit history, etc.  
Used logistic regression and other linear models as the baseline, and used lightgbm, catboost,and XGBoost classifiers to achieve higher predictive performance.

### Methods
- Exploratory Data Analysis:
 - Data visualisations of the numerical and categorical features
 - Visualisations of the predictors vs target
- Descriptive statistics
- Outlier identification using IQR and visualisation
- Data cleaning and feature engineering
- Model evaluation using AUC-ROC and precision-recall curves
- Hyperparameter tuning with cross-validation

### Key Results
- Achieved an AUC score of 0.96 on the validation set.
- XGBoost performed best overall, balancing recall and precision effectively.

### Finance Relevance
Accurate credit risk modeling helps financial institutions minimize loan defaults, optimize lending strategies, and improve overall portfolio quality.

### GitHub Repo
[View the code here](https://github.com/kgiannako/credit_risk_modelling) <!-- Replace with your repo link -->
