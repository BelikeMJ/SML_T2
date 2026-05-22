# Feature C — Embedding Feature Construction

## Leakage-Safe Data Pipeline

To avoid data leakage:

1. The original ratings dataset is sampled in a stratified way.
2. The sampled dataset is split into train/test sets.
3. Statistical features, interaction features, and SVD embeddings are computed using only the training set.
4. The test set only uses statistics and embeddings learned from the corresponding training split.

This ensures:

- no test information leakage
- fair model evaluation
- consistent repeated-split evaluation

---

## Feature C Construction

Feature C extends Feature B by adding collaborative filtering embedding features learned using SVD.

Feature C includes:

- all Feature A features
- all Feature B interaction features
- SVD latent embeddings

---

## 1. Statistical and Interaction Features

Feature C inherits:

- user statistical features
- item statistical features
- interaction features
- log-transformed features
- genre one-hot features
- temporal features
- pairwise cross features

from Feature A and Feature B.

---

## 2. SVD Embedding Features

Feature C introduces:

- `64-dimensional user embeddings`
- `64-dimensional item embeddings`

Example features include:

- `svd_user_embedding_0`
- `svd_item_embedding_0`

The embeddings are learned from the training data using sparse Singular Value Decomposition (SVD).

---

## 3. Embedding Interaction Features

Additional embedding-based features include:

- `svd_user_item_dot`
- `svd_user_item_cosine`
- `svd_predicted_rating`

These features capture latent relationships between users and movies.

---

## Final Feature Count

Each Feature C dataset contains:

- `253 columns` in total
- `250 engineered features`
- `2 ID columns`: `userId`, `movieId`
- `1 target column`: `label`

---

## Repeated Split Summary

The Feature C data is generated using:

- `10 repeated stratified train/test splits`
- `80% training`
- `20% testing`

Each repeat contains approximately:

- `160,000 training instances`
- `39,999 testing instances`

---

## Output Files

For each repeat, the following files are saved:

- `raw_train.csv`
- `raw_test.csv`
- `feature_C_train.csv`
- `feature_C_test.csv`

A summary file is also saved:

- `feature_C_split_summary.csv`

---

# Main Experimental Results

The following results are based on the repeated same-seed sampled setting and are averaged across 10 repeated experiments.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.6375 ± 0.0024 | 0.6453 ± 0.0024 | 0.6097 ± 0.0073 | 0.6270 ± 0.0041 | 0.6741 ± 0.0022 |
| Hinge-loss Linear SVM | 0.6397 ± 0.0017 | 0.6445 ± 0.0022 | 0.6226 ± 0.0059 | 0.6334 ± 0.0029 | 0.6800 ± 0.0017 |
| FT-Transformer | 0.6296 ± 0.0092 | 0.6484 ± 0.0078 | 0.5669 ± 0.0505 | 0.6036 ± 0.0270 | 0.6639 ± 0.0093 |

---

# Experimental Observations

- Feature C extends Feature B by introducing high-dimensional SVD collaborative filtering embeddings.
- Hinge-loss Linear SVM achieved the strongest overall performance under Feature C across most evaluation metrics.
- Logistic Regression remained competitive despite the substantially increased feature dimensionality.
- FT-Transformer showed higher variance and lower stability under repeated sampled experiments.
- The results suggest that the SVD embedding features improved the effectiveness of linear and margin-based models more consistently than the deep tabular model under the current sampled training scale.
