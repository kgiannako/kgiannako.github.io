---
title: "A Comparison of Machine Learning Methods for the Prediction of Traffic Speed in Urban Places"
date: 2019-12-23
tags: [machine-learning, traffic, transportation, neural-networks, support-vector-regression, random-forest]
---

## Summary

This post presents a comparison of several machine learning models for predicting traffic speed in urban environments, based on the paper _"A Comparison of Machine Learning Methods for the Prediction of Traffic Speed in Urban Places"_ by Bratsas et al., published in *Sustainability*.

The models evaluated include:
- **Random Forest**
- **Support Vector Regression (SVR)**
- **Multilayer Perceptron (MLP)**
- **Multiple Linear Regression (MLR)**

The study uses probe data from Thessaloniki, Greece, and assesses model performance across three traffic scenarios:
1. **Specific date-road combinations** – Predictions for randomly selected dates and roads.
2. **Short-term forecasts** – Predictions over eight consecutive 15-minute intervals.
3. **Daily forecasts** – Predictions for a full day on random roads.

### Key Findings
- **SVR** performs well in stable traffic conditions with minimal variation.
- **MLP** adapts better in cases of high variability and shows the smallest prediction errors.
- **MLR and Random Forest** perform reasonably but are outperformed by SVR and MLP depending on the context.

These results are relevant for intelligent traffic control systems and urban mobility planning, where accurate, context-aware traffic speed prediction is essential.

[Read the full article on MDPI](https://doi.org/10.3390/su12010142)
