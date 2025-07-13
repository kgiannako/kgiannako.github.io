---
title: "Company Entity Matching with SBERT & FAISS"
date: 2025-07-13
classes: wide
tags: [nlp, faiss, sbert, language-models, embeddings, cosine-similarity, entity-matching]
---
## Company Entity Matching with SBERT and FAISS

This project demonstrates a semantic entity matching pipeline designed to identify whether two company records refer to the same real-world organisation, despite textual variation or noise.

It leverages recent advances in **language models** and **approximate nearest neighbour search** to offer a robust, scalable matching solution suitable for real-world data.

---

### 🧠 Problem

Organisations are often listed with slight differences across databases:
"ABC Ltd, 12 High Street, London, UK"
vs
"A.B.C. Limited, 12 High St., London"


Traditional string-matching fails in such cases. Our goal was to:

- Learn **semantic similarity** between structured company descriptions.
- Retrieve likely matches efficiently from a large candidate set.

---

### 🔧 Tools & Methods

- **Sentence-BERT** (`all-MiniLM-L6-v2` and `all-mpnet-base-v2`)
- **FAISS** (HNSW index for fast top-K search)
- **WDC Entity Matching Dataset** (50 labelled company pairs)
- Evaluation via:
  - Cosine similarity
  - Precision, Recall, F1, Accuracy
  - AUC (Area Under the Curve)
  - Cosine similarity distribution plots

---

### 📊 Results Summary

| Model             | Accuracy | Precision | Recall | F1 Score | AUC   |
|------------------|----------|-----------|--------|----------|--------|
| MiniLM-L6-v2      | **0.88**     | 0.32      | 0.08   | 0.12     | 0.814   |
| MPNet-Base-v2     | 0.87 | **0.36**  | **0.23** | **0.28** | **0.821** |

✅ **MPNet outperformed MiniLM** in all metrics, showing stronger semantic representation of structured company text.

---

### 📈 Cosine Similarity Distributions

![MPNet vs MiniLM Cosine Plot](/assets/images/nlp-company-matching/cosine_distribution.png)

This visualises the distribution of similarity scores for matched vs non-matched pairs. The **better the separation**, the easier it is to set an effective matching threshold.

---

### 💻 Technologies Used

- Python, Jupyter
- SentenceTransformers
- FAISS (Facebook AI Similarity Search)
- Scikit-learn
- Seaborn / Matplotlib
- GitHub, GitHub Pages (Jekyll)

---

### 📂 Repo

You can find the full code here:  
➡️ [GitHub Repo](https://github.com/kgiannako/nlp-company-matching)

---

### 🏁 Outcome

This project demonstrates a production-ready approach to entity matching using modern NLP tools. It balances lightweight infrastructure with powerful semantic understanding, and is adaptable to use cases like:

- Sanctions list matching
- Deduplication of business records
- Lead cleaning in CRMs

---

*Built as part of my NLP portfolio. Always happy to discuss this project or related work.*
