# Hybrid SVD Recommender System - Betclic Hackathon

## 📌 Overview
This repository contains the code and methodology for a Hybrid Recommender System developed during a 48-hour RecSys Hackathon hosted by Betclic Group. Working with the MovieLens dataset (170k users, 50k movies), our team developed a robust recommendation engine that balances user personalization, temporal relevance, and catalog diversity. 

The model achieved a **Combined Score of 24.18%**  evaluated across NDCG, Precision, Recall, HitRate, and Coverage metrics.

## 🏗️ Architecture: The 3-Layer Hybrid
The recommendation engine is built on a custom 3-layer architecture:

1. **User Centering (Layer 1):** Normalizes rating distributions per user to remove personal bias (e.g., harsh critics vs. generous raters) before scoring.
2. **Latent Factor Engine (Layer 2):** Utilizes `TruncatedSVD` mapped to 60 latent components to reveal complex intersections between user tastes and movie features.
3. **Diversity Penalty (Layer 3):** Applies a custom penalty to popular blockbusters, significantly boosting catalog coverage and ensuring the discovery of hidden gems.

## ⏱️ Temporal Intelligence
Standard collaborative filtering treats a rating from 10 years ago the same as a rating from yesterday. To solve this "frozen profile" problem, we implemented **Recency Weighting** using exponential decay.By applying a half-life formula, the model prioritizes a user's current interests, allowing recommendations to evolve alongside their tastes.

## 🚀 The Deployment Pivot: Closure Factory
During the evaluation phase, we encountered binary incompatibilities causing the evaluator environment to crash. [cite_start]To bypass this, we implemented a **Closure Factory** wrapper. 
* We precomputed the SVD matrix dot products.
* We mapped the recommendations into a lightweight dictionary.
* We serialized the closure using `cloudpickle`, resulting in a zero-dependency, highly stable deployment artifact that performs instant dictionary lookups instead of heavy matrix math in production.

## 📊 Performance Metrics
The model's performance was evaluated using an 80/20 temporal split.
* **Combined Score:** 24.18%
* Evaluated against NDCG@10, Precision@10, Recall@10, HitRate@10, and Coverage.

## 🛠️ Tech Stack
* **Python 3**
* **Pandas / NumPy / SciPy** (Sparse Matrices)
* **Scikit-Learn** (`TruncatedSVD`, `normalize`)
* **Cloudpickle** (Serialization)

## Note: As the dataset size is huge (860 MB), it could not be uploaded in this repo. If you want the dataset, you can connect with me for the same.
