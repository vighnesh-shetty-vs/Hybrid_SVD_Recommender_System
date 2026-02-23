# Hybrid SVD Recommender System - Betclic Hackathon

## 📌 Overview
[cite_start]This repository contains the code and methodology for a Hybrid Recommender System developed during a 48-hour RecSys Hackathon hosted by Betclic Group. [cite_start]Working with the MovieLens dataset (170k users, 50k movies)[cite: 444, 445, 446], our team developed a robust recommendation engine that balances user personalization, temporal relevance, and catalog diversity. 

[cite_start]The model achieved a **Combined Score of 24.18%**  [cite_start]evaluated across NDCG, Precision, Recall, HitRate, and Coverage metrics[cite: 40].

## 🏗️ Architecture: The 3-Layer Hybrid
[cite_start]The recommendation engine is built on a custom 3-layer architecture:

1. [cite_start]**User Centering (Layer 1):** Normalizes rating distributions per user to remove personal bias (e.g., harsh critics vs. generous raters) before scoring[cite: 4, 5].
2. [cite_start]**Latent Factor Engine (Layer 2):** Utilizes `TruncatedSVD` mapped to 60 latent components to reveal complex intersections between user tastes and movie features[cite: 6, 7, 23].
3. [cite_start]**Diversity Penalty (Layer 3):** Applies a custom penalty to popular blockbusters, significantly boosting catalog coverage and ensuring the discovery of hidden gems.

## ⏱️ Temporal Intelligence
Standard collaborative filtering treats a rating from 10 years ago the same as a rating from yesterday. [cite_start]To solve this "frozen profile" problem, we implemented **Recency Weighting** using exponential decay[cite: 25, 26, 28]. [cite_start]By applying a half-life formula, the model prioritizes a user's current interests, allowing recommendations to evolve alongside their tastes[cite: 29, 32].

## 🚀 The Deployment Pivot: Closure Factory
[cite_start]During the evaluation phase, we encountered binary incompatibilities causing the evaluator environment to crash. [cite_start]To bypass this, we implemented a **Closure Factory** wrapper. 
* We precomputed the SVD matrix dot products.
* We mapped the recommendations into a lightweight dictionary.
* [cite_start]We serialized the closure using `cloudpickle`, resulting in a zero-dependency, highly stable deployment artifact that performs instant dictionary lookups instead of heavy matrix math in production[cite: 37, 39, 51].

## 📊 Performance Metrics
[cite_start]The model's performance was evaluated using an 80/20 temporal split[cite: 42].
* [cite_start]**Combined Score:** 24.18% [cite: 44]
* [cite_start]Evaluated against NDCG@10, Precision@10, Recall@10, HitRate@10, and Coverage[cite: 208, 210, 212, 215, 223].

## 🛠️ Tech Stack
* **Python 3**
* **Pandas / NumPy / SciPy** (Sparse Matrices)
* **Scikit-Learn** (`TruncatedSVD`, `normalize`)
* **Cloudpickle** (Serialization)
