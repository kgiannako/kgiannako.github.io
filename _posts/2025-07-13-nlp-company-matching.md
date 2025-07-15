---
title: "Company Entity Matching with SBERT & FAISS"
date: 2025-07-12
classes: wide
tags: [nlp, faiss, sbert, language-models, embeddings, cosine-similarity, entity-matching]
---

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
| MiniLM-L6-v2      | 0.75     | 0.27      | **0.69**   | 0.38     | 0.81   |
| MPNet-Base-v2     | **0.77** | **0.28**  | **0.69** | **0.40** | **0.82** |

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

### 🔄 Next Steps

Although the models demonstrated solid ranking performance (AUC > 0.80), classification precision remains relatively low. Below are a few avenues to improve the system:

1. **Increase Dataset Size**  
   The current dataset contains only 50 labelled pairs, which limits the model's ability to generalise. Expanding the training set, even to a few hundred pairs, would likely improve reliability.

2. **Field-Specific Weighting**  
   Not all fields contribute equally. For instance, the `brand` or `title` may carry more matching value than a long `description`. Custom weighting or encoding could help highlight important tokens.

3. **Fine-Tune the Language Model**  
   While we used pre-trained SBERT models (MiniLM and MPNet), fine-tuning on domain-specific entity pairs with a contrastive or triplet loss would help the model better distinguish subtle differences.

4. **Train a Lightweight Classifier**  
   Using the cosine similarity and/or embedding differences as features in a logistic regression or tree-based model could improve decision boundaries without retraining the language model.

5. **Broader Retrieval Evaluation**  
   Moving beyond pairwise scoring to a full retrieval task (e.g., matching a single query against a catalogue of 1,000 companies) would enable metrics like hit rate, recall@k, and real-world relevance.

6. **Deploy as a Search Interface**  
   The core components are well-suited for deployment in a demo interface (e.g., Streamlit or Flask app), allowing interactive search and inspection of match results.

---

### 🏁 Outcome

This project demonstrates a production-ready approach to entity matching using modern NLP tools. It balances lightweight infrastructure with powerful semantic understanding, and is adaptable to use cases like:

- Sanctions list matching
- Deduplication of business records
- Lead cleaning in CRMs

---

*Built as part of my NLP portfolio. Always happy to discuss this project or related work.*
