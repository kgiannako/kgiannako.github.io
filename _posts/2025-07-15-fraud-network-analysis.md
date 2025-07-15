---
title: "Fraud Network Analysis Using Graph Analytics"
date: 2025-07-15
classes: wide
tags: [data-science, network-analysis, kaggle, fraud-detection]
---
This project investigates financial fraud patterns by modeling transactions as network graphs and applying graph algorithms for exploratory analysis.  
I explored both **tabular financial datasets** and **real-world blockchain transaction networks** to assess how fraud manifests in connected systems.

---

## Objectives
- 🛠️ Build transaction networks from structured datasets.
- 🔍 Use **Breadth-First Search (BFS)** to explore fraud clustering within networks.
- 📊 Analyze connected components and their fraud density.
- 🧮 Compare centrality metrics (degree, betweenness, closeness) across node types.
- 🎨 Visualize key structures in the transaction networks.

---

## Datasets Used
- **IEEE-CIS Fraud Detection (Kaggle):**  
  Used for inferring relationships in structured financial data.
  
- **Elliptic Bitcoin Transaction Dataset (Kaggle):**  
  Provided real-world blockchain transaction links and class labels.

---

## Tools & Technologies
- Python  
- NetworkX (Graph Analysis)  
- Pandas, NumPy  
- Matplotlib, Seaborn (Visualization)  
- Jupyter Notebook  
- Git & GitHub for version control  

---

## Key Findings
- **Fraudulent transactions tend to be on the network periphery.**  
  They avoid acting as hubs or connectors within the network.

- **Limited direct fraud clustering in BFS exploration.**  
  Significant connections emerge only at larger depths.

- **Fraud appears in large, mixed connected components.**  
  Fraudulent nodes are interspersed with licit and unknown transactions.

- **Centrality measures alone do not predict fraud risk effectively.**  

---

## Skills Demonstrated
- Graph data modeling & algorithmic analysis  
- Network-based exploratory data analysis  
- Visual storytelling with complex network structures  
- Statistical evaluation of graph features  
- Clean code organization with Python and Jupyter  

---

## What's Next?
- Experimenting with community detection algorithms  
- Testing graph embeddings (Node2Vec) for latent pattern discovery  
- Integrating network features into supervised machine learning models  

---

## 📂 [View the Full Project on GitHub](https://github.com/kgiannako/fraud-network-analysis)

---
