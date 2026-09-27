---
title: "Credit Risk Management: Probability of Default Prediction Using Machine Learning"
date: 2025-05-03
description: "A probability-of-default model comparing logistic regression baselines with a LightGBM + XGBoost ensemble."
group: "Quantitative finance"
tags: [finance, machine-learning, credit-risk, lightgbm, xgboost]
redirect_from:
  - "/finance/machine learning/credit-risk-modelling/"
---

## Summary
Developed a machine learning model to predict the probability of loan default (PD) based on borrower features such as income, interest rate, credit history, etc.  
Used logistic regression and other linear models as the baseline, and used an ensemble of lightgbm and XGBoost classifiers to achieve higher predictive performance.

## Key Results
- Achieved an AUC score of 0.96 on the validation set.
- An ensemble approach of lightGBM and XGBoost performed best overall, balancing recall and precision effectively.

## Methods
- Exploratory Data Analysis:
  - Data visualisations of the numerical and categorical features
  - Visualisations of the predictors vs target
- Descriptive statistics
- Outlier identification using IQR and visualisation
- Data cleaning and feature engineering
- Model evaluation using AUC-ROC and precision-recall curves
- Hyperparameter tuning with cross-validation


## GitHub Repo
[View the code here](https://github.com/kgiannako/credit_risk_modelling)
