---
title: "Credit Risk Management: Probability of Default Prediction Using Machine Learning"
date: 2025-05-03
categories: [Finance, Machine Learning]
---

### Summary
Developed a machine learning model to predict the probability of loan default (PD) based on borrower features such as income, interest rate, credit history, etc.  
Used logistic regression and other linear models as the baseline, and used lightgbm, catboost, and XGBoost classifiers to achieve higher predictive performance.

### Key Results
- Achieved an AUC score of 0.96 on the validation set.
- An ensemble approach of lightGBM, XGBoost and catboost performed best overall, balancing recall and precision effectively.

### Methods
- Exploratory Data Analysis:
  - Data visualisations of the numerical and categorical features
  - Visualisations of the predictors vs target
- Descriptive statistics
- Outlier identification using IQR and visualisation
- Data cleaning and feature engineering
- Model evaluation using AUC-ROC and precision-recall curves
- Hyperparameter tuning with cross-validation


### GitHub Repo
[View the code here](https://github.com/kgiannako/credit_risk_modelling) <!-- Replace with your repo link -->
