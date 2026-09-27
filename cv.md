---
title: "Curriculum Vitae"
description: "Senior Data Scientist at Lloyd's List Intelligence, London"
permalink: /cv/
class: cv
---

Senior Data Scientist (MSc Statistics, UCL) at Lloyd's List Intelligence with 5 years in maritime and trade analytics, currently leading applied research on cargo-flow tracking across crude and container markets. My work spans AIS and geospatial analytics, satellite-imagery detection pipelines, NLP/LLM retrieval and entity resolution, including a compliance screening system that reached £200k ACV in its first 10 weeks. I'm experienced in both applied research and building production systems.

## Experience

### Senior Data Scientist · Lloyd's List Intelligence
*Mar 2026 – Present · Applied research and innovation: PoC lead, strategy and data partnerships*

- Leading a PoC tracking crude flows across major export lanes, built on AIS-derived data: STS and lightering transfers, port/berth/anchorage/FPSO load and discharge events, a draught-to-tonnes payload model, and terminal-based inference to identify crude parcels and crude-capable tonnage, achieving up to 90% correlation against official trade statistics
- Translating PoC findings into company strategy: defining the data, methodology and partnership gaps required to productionise cargo-flow tracking, and informing data acquisition and vendor decisions
- Leading the data science workstream for a trade-finance PoC, fusing document-based container tracking with AIS and macro data to derive cargo-flow signals and portfolio benchmarking; demoed to tier-1 banking customers
- Researched, validated and productionised optical and SAR satellite imagery pipelines for vessel detection and AIS spoofing verification

### Data Scientist · Lloyd's List Intelligence
*Jun 2024 – Feb 2026 · Squad lead, cross-functional delivery*

- Led end-to-end delivery as data science lead in a cross-functional squad, from problem scoping and modelling through to deployment and product launch
- Architected and deployed a production NLP/LLM retrieval pipeline on AWS SageMaker (text-to-embeddings, FAISS indexing and custom re-ranking), reducing manual compliance screening time by ~50% and driving £200k ACV within 10 weeks of launch
- Built a production entity-resolution pipeline automating ~40% of cases, removing the need for additional headcount and contributing to a 3–4% reduction in product development capex
- Prototyped an internal RAG-based assistant (AWS Bedrock + Bedrock Knowledge Bases + Streamlit) to speed up responses to product and data queries for internal teams and customers
- Researched graph-based maritime risk representations (vessel–entity–ownership networks) and multi-source entity resolution, evaluating GNN approaches for sanctions and operational risk prediction
- Mentored two data analysts on technical delivery and product alignment

### Senior Data Analyst · Lloyd's List Intelligence
*Mar 2023 – May 2024*

- Developed PoC vessel fuel consumption and emissions models (ML and regression) to support ESG analytics
- Delivered statistical and ML imputation models for maritime draft, payload and fuel data, improving upstream data quality for ESG emissions estimates
- Collaborated with engineers to design and automate fuzzy matching pipelines in AWS for vessel–port alignment, increasing prediction accuracy and coverage

### Maritime Data Analyst · Lloyd's List Intelligence
*Oct 2021 – Feb 2023*

- Contributed ML feature engineering for ETA, congestion and destination prediction models; validated model robustness and operational relevance
- Led a team of three analysts to develop a new advanced analytics product feature, aligning technical outputs with stakeholder value

### Junior Data Scientist / Author · Open Knowledge Foundation Greece
*Jun 2019 – Dec 2019*

- Compared ML methods (neural networks, SVR, random forest) for short-term traffic speed prediction using 5 months of Thessaloniki traffic data collected with CERTH; results published in *Sustainability* (2020) — [project write-up](/projects/traffic-speed-prediction-ml/)

## Education

### MSc Statistics (Distinction) · University College London
*2020 – 2021*

**Dissertation:** Approximate Bayesian Computation for Factor Copula Models in Finance — modelling complex dependence structures for financial risk ([write-up](/projects/abc-for-copulas/))  
**Relevant modules:** Stochastic Methods in Finance, Decisions & Risk, Forecasting, Statistical Inference, Statistical Computing  
**Key projects:** VaR modelling with copulas; GLM/RF/XGBoost sales forecasting; ARIMA/ES time series forecasting

### BSc Mathematics (GPA 7.93/10) · Aristotle University of Thessaloniki
*2015 – 2019*

**Dissertation:** Predicting Pittsburgh Sleep Quality Index Using Machine Learning Models  
**Relevant modules:** Probability Theory, Econometrics, Deep Learning, Time Series Analysis, Stochastic Methods in Finance, PDEs, Information Theory, Numerical Analysis, Stochastic Processes, Linear Algebra, Measure Theory, Game Theory

## Technical Skills

**Languages:** Python (pandas, scikit-learn, PyTorch), SQL (incl. spatial SQL), R  
**ML & AI:** Supervised/unsupervised learning, NLP & LLMs, semantic search & embeddings (FAISS, Elasticsearch), RAG and agentic retrieval (LangGraph, Bedrock Knowledge Bases), computer vision and object detection (YOLOv8, optical and SAR imagery), knowledge graphs (Neo4j), entity resolution, GNNs, geospatial analysis (GeoPandas)  
**Cloud & Infra:** AWS (SageMaker, Bedrock, ECS/Fargate, S3, Redshift, ECR), Snowflake, Oracle, DuckDB, Parquet, Docker, Git/GitHub, CI/CD, MLflow  
**Quant & Finance:** Stochastic calculus, Monte Carlo simulation, option pricing (Black–Scholes, Greeks), copula modelling, Value-at-Risk, Ornstein–Uhlenbeck and mean-reverting processes, Hidden Markov Models, time series forecasting  
**Analytics & BI:** Tableau, Power BI, LaTeX

## Selected Projects

**[Sanctions Knowledge Graph with Agentic Retrieval](/projects/sanctions-knowledge-graph/)**  
End-to-end agentic knowledge base over OFAC, UN and EU sanctions lists: parsed source XML into a Neo4j graph (~25k entities), built a 60k-vector FAISS semantic index, and implemented a two-stage entity resolution pipeline producing 4k+ cross-source SAME_AS edges. Deployed as a LangGraph ReAct agent with five retrieval tools spanning graph traversal, semantic search and structured lookups.

**[Probabilistic Vessel Valuation Engine](/projects/vessel-valuation-engine/)**  
Stochastic DCF model for dry bulk cargo vessels using a log-normal Ornstein–Uhlenbeck freight rate process, with parameters calibrated from the Baltic Panamax Index via AR(1) MLE. Monte Carlo simulation produces full distributions of asset NPV, equity IRR and MOIC. Deployed as an [interactive web app](https://vessel-valuation-dcf.streamlit.app).

**LLM/RAG Retrieval System**  
Production-grade retrieval pipeline with embedding generation, vector indexing, custom re-ranking and automated evals, designed for high-precision compliance and information retrieval use cases.

## Publications & Certifications

- Bratsas, C., Koupidis, K., Salanova, J., **Giannakopoulos, K.** et al. (2020). ["A Comparison of Machine Learning Methods for the Prediction of Traffic Speed in Urban Places."](https://doi.org/10.3390/su12010142) *Sustainability*, 12(1), 142.
- Columbia University — Computational Finance (Financial Engineering & Risk Management)
