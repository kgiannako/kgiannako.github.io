---
title: "Regime-Based Portfolio Strategies with Hidden Markov Models"
date: 2025-07-20
classes: wide
tags: [data-science, quantitative-finance, portfolio-management, HMM, risk-management, time-series]
---
In this project, the use of **Hidden Markov Models (HMMs)** was explored for regime detection in financial markets and how these regimes can inform simple, rule-based investment strategies.

## 📈 Regime Detection in Financial Markets  

Financial markets often exhibit distinct behavioural regimes, periods of stability, growth, or heightened risk, each with characteristic returns and volatility.  
Hidden Markov Models (HMMs) offer a structured way to detect these regimes directly from return data, without predefined labels.

---

## 🧩 Methodology Overview  

- **HMMs were trained on both daily and weekly log returns of the S&P 500.**  
  This allowed for capturing both short-term volatility patterns and longer-term market phases.

- **Identified regimes included:**  
  - Calm/stable periods  
  - Bullish or speculative phases  
  - Crisis/high-risk periods  

- **Strategy Variants Tested:**  
  - Exposure only during calm regimes  
  - Exposure during calm and bullish regimes  
  - Dynamic exposure scaled by regime risk  
  - Standard Buy & Hold as a benchmark  

- **Performance Metrics:**  
  - Cumulative returns  
  - Sharpe and Sortino ratios  
  - Maximum drawdown  

---

## ⚙️ Key Insights  

- **Daily HMMs** tend to reflect short-term volatility clustering but are prone to noise.  
- **Weekly HMMs** provide clearer regime separation, suitable for medium-term portfolio decisions.  
- **Regime-aware strategies consistently improved risk-adjusted returns** compared to passive exposure.  
- Dynamic exposure, adjusting positions based on regime, offered a practical balance between return and risk.  

---

## 📊 Practical Applications  

The weekly HMM model can support a regime-driven portfolio approach by:  
- Maintaining exposure in stable or bullish regimes  
- Reducing or eliminating exposure during identified crisis periods  
- Acting as a disciplined overlay for portfolio risk management  

---

## ⚖️ Considerations & Limitations  

- Regime detection models require periodic reassessment due to market structural changes.  
- HMM outcomes are sensitive to initial conditions and may vary between fits.  
- These strategies are intended for risk management, not short-term market timing.  

---

## 📈 Results Summary  

**On Daily Data:**  
- **Only Calm Regime Strategy:** Highest Sharpe (1.74), lowest drawdown (-10.84%)  
- **Dynamic Exposure Strategy:** Balanced performance with good risk-adjusted returns  
- **Including Bullish Regime on Daily Data:** Increased drawdowns without proportionate return  
- **Buy & Hold:** Weakest risk-adjusted performance, high drawdowns (-83.88%)  

**On Weekly Data:**  
- **Calm + Bullish Regimes Strategy:** Delivered the strongest performance, annualised return of 21.69%, Sharpe of 1.54, and controlled drawdown (-20.94%)  
- **Dynamic Exposure Strategy:** Strong Sharpe (1.31), moderate drawdowns  
- **Only Calm Regime on Weekly Data:** Too conservative, limiting upside  
- **Buy & Hold:** Continued to underperform across metrics

| Strategy | Annualised Return | Sharpe Ratio | Sortino Ratio | Max Drawdown |
|----------|-------------------|--------------|--------------|--------------|
| **Only Calm Regime (State 0)** | 9.67% | 0.86 | 1.23 | -37.32% |
| **Calm + Bullish Regimes (State 0 or 1)** | **21.69%** | **1.54** | **2.66** | **-20.94%** |
| **Buy & Hold** | 4.14% | 0.23 | 0.28 | -82.65% |

---

The weekly model showed that combining calm and bullish regimes produced the best balance of returns and risk.  
Dynamic exposure also performed well, highlighting the benefit of scaling positions according to detected regimes.  
Buy & Hold consistently underperformed on risk-adjusted metrics and suffered significant drawdowns.

---
[📂 View the Project on GitHub](https://github.com/kgiannako/sp500-volatility-regime-hmm)

