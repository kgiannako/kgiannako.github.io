---
title: "Approximate Bayesian Computation for Factor Copulas"
date: 2021-09-18
categories: [bayesian-inference, factor-copulas, approximate-bayesian-computation, finance, statistical-modelling]
---
## Summary

This project explores the use of Approximate Bayesian Computation (ABC) to estimate parameters of factor copula models, particularly in the context of stock return data. ABC is a simulation-based method that approximates the posterior distribution when the likelihood is difficult or impossible to compute. It operates by comparing observed and simulated summary statistics using a distance metric and a tolerance threshold.

Factor copulas provide a flexible way to model dependencies between random variables through latent and idiosyncratic components. Several copula models were considered, including symmetric and asymmetric cases, with varying degrees of tail dependence. The estimation focused on dependence measures such as rank correlations and quantile dependence.
<figure>
  <img src="/assets/Rplot11.jpeg" alt="Factor Copulas">
  <figcaption>Scatterplots of samples from four different Factor Copulas, with N(0,1) margins and with linear correlation 0.7</figcaption>
</figure>  
Experiments included models with increasing dimensionality and different distributional assumptions. Simulations showed that as the data size increases and the acceptance threshold tightens, the accuracy of the posterior approximation improves. For more complex models, including those with skewed and heavy-tailed distributions, ABC was still effective when enough data were available.

Regression adjustments, both linear and local-linear, were applied to reduce the bias and variance of the posterior estimates. These adjustments led to lower estimation errors and more concentrated posterior distributions.

The study concludes that ABC is a viable method for estimating high-dimensional, flexible copula models, provided that suitable summary statistics and a sufficient amount of data are available.
<figure>
  <img src="/assets/Rplot13.jpeg" alt="ABC with Regression">
  <figcaption>Approximations of the posterior distribution of model parameters, using the ABC rejection algorithm vs with linear regression adjustment vs with local-linear regression adjustment</figcaption>
</figure>  
### GitHub Repo
[View the code here](https://github.com/kgiannako/Approximate-Bayesian-Computation-for-Factor-Copulas) 
