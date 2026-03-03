---
title: "Probabilistic Vessel Valuation Engine"
date: 2026-03-03
categories:
  - projects
tags:
  - quantitative-finance
  - stochastic-modelling
  - python
  - shipping
  - monte-carlo
excerpt: "Monte Carlo DCF model for dry bulk cargo vessels using a calibrated log-OU freight rate process. Distributions over everything — no point estimates."
header:
  teaser: /assets/vessel-valuation-teaser.png
toc: true
toc_label: "Contents"
classes: wide
---

## Overview

A stochastic DCF valuation engine for dry bulk cargo vessels. The key design decision: every uncertain input is a distribution, not a point estimate. The output is a full distribution of asset NPVs, equity IRRs, and return multiples across 5,000 simulated freight rate environments — giving a structured, quantified view of how vessel value depends on the freight cycle.

Built as a data product demonstrator, deployed as an interactive Streamlit web application.

**[→ Live app](https://vessel-valuation-dcf.streamlit.app)** &nbsp;·&nbsp; **[→ GitHub](https://github.com/kgiannako/vessel-valuation-dcf)**

---

## The Problem with Point-Estimate DCF

Standard vessel valuation assumes a single freight rate path — typically a straight-line mean reversion to some assumed long-run rate. This produces a single NPV, which conceals the most important question: *how sensitive is that value to rate assumptions?*

Shipping is a cyclical industry. A Panamax bulk carrier trading at $9,500/day today could plausibly earn $4,000/day or $20,000/day within two years. A model that doesn't represent this uncertainty isn't a valuation — it's a spreadsheet with hidden assumptions.

---

## The Freight Rate Model

Freight rates are modelled as a **log-normal Ornstein-Uhlenbeck (OU) process**:

\\[d\ln S_t = \kappa(\mu - \ln S_t)\,dt + \sigma\,dW_t\\]

where \\(S_t\\) is the TCE rate, \\(\kappa\\) is the mean reversion speed, \\(\mu\\) is the long-run log-mean, and \\(\sigma\\) is the instantaneous volatility.

The OU process is appropriate for freight rates for two reasons:
- **Mean reversion**: rate spikes (2008, 2021) reliably unwind — unlike equities, rates don't trend indefinitely
- **Strictly positive**: modelling log-rates enforces the lower bound — a vessel always has scrap option value

### Calibration from Data

Parameters are estimated from the Baltic Panamax Index (BPI), 2012–2025, via **AR(1) maximum likelihood estimation** on weekly log-rates. The discretised OU process is an AR(1):

\\[x_{t+1} = \alpha + \beta x_t + \varepsilon_t\\]

with closed-form MLE giving \\(\hat{\beta}\\), \\(\hat{\alpha}\\), \\(\hat{\sigma}_\varepsilon\\), which map back to the continuous-time OU parameters.

| Parameter | Value | Note |
|-----------|-------|------|
| κ (mean reversion speed) | 1.01 | Half-life ~0.68 years — Panamax rates revert quickly |
| σ (annualised log-vol) | 0.71 | Stable across rolling windows |
| μ (long-run mean) | $9,500/day | Mid-range of full-history and post-2015 estimates |

Rolling window analysis confirms κ and σ are stable across time (safe to calibrate), while μ varies substantially (treated as a judgement input anchored to the data range).

---

## Model Architecture

On each of 5,000 simulated rate paths, the model builds a full annual P&L:

- **Revenue**: spot TCE earnings + any fixed time-charter contracts
- **Costs**: daily opex, scheduled drydocking (every 5 years), off-hire
- **Debt service**: amortisation and interest (optional — financing toggle)
- **Terminal value**: second-hand sale (EV/EBITDA multiple) or scrap demolition

Terminal value uses freight–scrap correlation via Cholesky decomposition — in distressed markets, owners scrap aggressively, depressing both freight rates and scrap prices simultaneously.

Each path produces a full IRR (solved via Brentq root-finding), MOIC, and NPV. The output is a distribution, not a number.

---

## Key Design Decisions

**Unlevered by default.** Asset valuation is independent of financing structure. Financing is deal-specific; vessel value is not. A toggle enables levered equity analysis when needed.

**Calibrated, not assumed.** The 📡 CALIBRATED / 🎯 JUDGEMENT distinction in the UI makes explicit which parameters come from data and which encode user views.

**Distributions on costs too.** Opex and drydock costs are drawn from log-normal distributions on each path — not held fixed. A model that randomises revenue but holds costs constant understates true uncertainty.

---

## Tools & Stack

Python · NumPy · SciPy · Streamlit · Matplotlib · Jupyter

---

## Results

The model produces asset NPV distributions with a median of ~$7.9M above purchase price in the base case, with a P10–P90 range of $0.2M–$22M — reflecting genuine freight rate uncertainty rather than false precision.

The calibration notebook documents the full estimation methodology including AR(1) diagnostics, rolling window stability tests, and model validation against the observed rate distribution.

---

## Code

Full source, calibration notebook, and data available on [GitHub](https://github.com/kgiannako/vessel-valuation-dcf).
