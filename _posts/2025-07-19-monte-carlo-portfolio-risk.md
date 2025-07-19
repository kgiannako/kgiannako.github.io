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

## 🔎 What Did I Learn?

- **Model choice matters:**  
  The t-distribution exposed significantly higher tail risk, particularly for the market-cap weighted portfolio.

- **Historical risk can be misleading:**  
  The market-cap portfolio seemed safer historically, but simulations suggest it could carry higher systemic risk in extreme events.

- **Equal Weighting diversifies some systemic risks but historically showed higher drawdowns.**

---

## 💬 Conclusion

> Risk modeling isn't about choosing one "best" method — it's about understanding each method's perspective on potential losses.  
> Combining historical analysis with simulation-based approaches helps build a fuller picture of portfolio risk, especially when accounting for tail events.

---

[🔗 View the full project on GitHub](https://github.com/kgiannako/your-repo-name)
