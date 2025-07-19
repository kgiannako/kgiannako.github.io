---
title: "Monte Carlo Portfolio Risk Analysis"
date: 2025-07-19
classes: wide
tags: [data-science, quantitative-finance, risk-management, monte-carlo, portfolio-analysis, value-at-risk, simulation]
---
Understanding portfolio risk isn't just about looking at historical losses, it's about anticipating how bad things *could* get.  
In this project, I explored three ways to estimate downside risk for two portfolio strategies:

- **Equal Weight Portfolio**
- **Market Cap Weighted Portfolio**

---

## 🛠 Methods Compared
- **Monte Carlo Simulation (Normal Distribution):**  
  Classic approach using historical mean returns and covariance, assuming normally distributed returns.
  
- **Monte Carlo Simulation (t-Distribution):**  
  Fat-tailed simulation to capture extreme events and systemic risk.

- **Historical Rolling Returns:**  
  Non-parametric estimation based on actual past 1-year cumulative returns.

---

## 📈 Key Results

| Method                  | VaR (95%) Equal | CVaR (95%) Equal | VaR (95%) Cap | CVaR (95%) Cap |
|-------------------------|------------------|-------------------|---------------|----------------|
| Monte Carlo (Normal)   | -14.47%         | -22.46%           | -19.65%       | -27.50%        |
| Monte Carlo (t-Dist)   | **-24.68%**     | **-33.70%**       | **-30.10%**   | **-38.61%**    |
| Historical Data        | -15.93%         | -18.56%           | -8.66%        | -10.90%        |

---

## 🧩 Key Insights & Model Reflections  

- **Model assumptions shape risk perception**  
  The normal distribution assumes mild market behavior with independent returns and thin tails — a simplification that led to understated VaR and CVaR in our simulations.  
  By contrast, the t-distribution better captured fat-tailed risks, highlighting the potential severity of systemic downturns, especially in concentrated portfolios.

- **Historical performance does not imply future risk**  
  The market-cap weighted portfolio appeared safer when judged on historical data — showing lower historical VaR and CVaR.  
  Yet simulations revealed it may carry disproportionate tail risk due to concentrated exposure to large-cap names during market-wide shocks.  
  This reflects a key limitation of historical risk metrics: they anchor only to past realized losses and may miss unseen systemic vulnerabilities.

- **Equal Weighting trades off diversification with increased idiosyncratic risk**  
  While equal weighting dampened simulated systemic risk compared to market-cap weighting, it historically suffered higher drawdowns.  
  This suggests that while diversification across sectors and companies reduces exposure to systemic shocks, it can increase exposure to volatile individual components.

- **Simulation is only as good as its assumptions**  
  Even the t-distribution relies on static correlations and constant volatility — both of which can break down in real crises.  
  Monte Carlo models, while flexible, assume market dynamics can be reasonably extrapolated from past statistical properties — an assumption that may fail in turbulent conditions.

---

## 💡 Practical Takeaways  

- **Use multiple risk estimation methods in practice**  
  A single method — whether historical or simulation-based — is insufficient for a comprehensive risk assessment.  
  Overlaying historical analysis with simulations under different distributional assumptions can reveal hidden vulnerabilities.

- **Be wary of over-reliance on historical stability**  
  Portfolios that look stable in the past may carry latent risks when markets behave abnormally — a case clearly shown by the higher simulated risks for the market-cap portfolio under the t-distribution.

- **Tail risk should be a proactive focus, not a retrospective one**  
  Even if historical losses have been mild, scenarios reflecting tail dependencies and fat tails should be part of regular risk assessments — especially in systemic portfolios.

---

> **Conclusion:**  
> This analysis demonstrates that the perception of risk is highly sensitive to both model assumptions and historical data limitations.  
> By challenging historical data with fat-tailed simulations, we uncover meaningful differences in potential downside risk between portfolio strategies — insights critical for informed portfolio construction and robust risk management.

---

[🔗 View the full project on GitHub](https://github.com/kgiannako/your-repo-name)
