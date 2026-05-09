# Dataset

This project uses the MovieLens 20M dataset published by GroupLens.

Dataset source:

https://www.kaggle.com/datasets/grouplens/movielens-20m-dataset

The project mainly uses the following files:

| File | Main Columns | Description |
|---|---|---|
| `rating.csv` | `userId`, `movieId`, `rating`, `timestamp` | User movie rating records |
| `movie.csv` | `movieId`, `title`, `genres` | Movie metadata and genres |
| `tag.csv` | `userId`, `movieId`, `tag`, `timestamp` | User-generated movie tags |
| `genome_scores.csv` | `movieId`, `tagId`, `relevance` | Relevance scores between movies and predefined tags |
| `genome_tags.csv` | `tagId`, `tag` | Predefined tag vocabulary |

Binary labels are constructed as:

```text
label = 1 if rating >= 4 else 0
```

which represents:

- `1` → user likes the movie
- `0` → user does not like the movie

The task is formulated as a binary classification problem that predicts whether a user likes a movie based on user-item interactions and engineered features.
---

# Experimental Design

This project investigates how the introduction of high-dimensional features affects the performance of models with different levels of complexity, and explores whether more complex models can utilize high-dimensional features more effectively to improve prediction performance.

Three levels of feature sets are designed:

| Feature Set | Type | Description |
|---|---|---|
| Feature A | Basic | Basic statistical features about users and items |
| Feature B | Interaction | Interaction-based features between users and items |
| Feature C | Embedding | Latent features learned from collaborative filtering using SVD |

Three models with increasing model complexity are compared:

| Model | Complexity | Description |
|---|---|---|
| Logistic Regression | Simple | Linear model with low capacity and high bias |
| Support Vector Machine | Medium | Margin-based model with stronger decision boundaries |
| FT-Transformer | Complex | Transformer-based deep learning model for tabular data |

The full experimental design compares each feature set with each model:

| Feature Set | Logistic Regression | Support Vector Machine | FT-Transformer |
|---|---|---|---|
| Feature A | Baseline performance using basic features | Improvement from a stronger traditional model | Complex model with basic features |
| Feature B | Effect of interaction features on a simple model | Combined effect of interaction features and medium model complexity | Complex model with interaction features |
| Feature C | Whether advanced embeddings can improve a simple model | Traditional model with rich latent features | Highest feature complexity with highest model complexity |


---

# FT-Transformer

The advanced model selected in this project is **FT-Transformer**, a Transformer-based architecture designed specifically for tabular data.

FT-Transformer was proposed in:

- NeurIPS 2021
- Paper: *Revisiting Deep Learning Models for Tabular Data*
- Poster:
  https://neurips.cc/virtual/2021/poster/26866


This project uses the official implementation provided by Yandex Research.

Repository:

```text
https://github.com/yandex-research/rtdl-revisiting-models
```

The implementation is imported from:

```python
from rtdl_revisiting_models import FTTransformer
```

---

# Hyperparameter Tuning

Hyperparameter tuning was implemented manually using repeated validation splits.

Examples include:

## Logistic Regression

- C values

## Linear SVM (Hinge Loss)

- alpha values

## FT-Transformer

- learning rate


Multiple candidate values were evaluated for each hyperparameter.

---

# Evaluation Metrics

The project evaluates model performance using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- True Positives (TP)
- True Negatives (TN)
- False Positives (FP)
- False Negatives (FN)
