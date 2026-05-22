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

## Support Vector Machine (Hinge Loss)

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

# Overall Experimental Results

The final experiments investigate how increasing feature complexity affects models with different levels of model complexity under a repeated same-seed sampled experimental setting.

Three feature sets are compared:

- Feature A: basic statistical features
- Feature B: interaction-based engineered features
- Feature C: embedding-based latent features using SVD

Three models with increasing complexity are evaluated:

- Logistic Regression (simple)
- Hinge-loss Linear SVM (medium)
- FT-Transformer (complex)

All reported results are averaged across 10 repeated stratified train/test splits.

---

## Feature A Results

| Model | Accuracy | F1-score | ROC-AUC |
|---|---|---|---|
| Logistic Regression | 0.6344 | 0.6324 | 0.6668 |
| Hinge-loss Linear SVM | 0.6365 | 0.6336 | 0.6768 |
| FT-Transformer | 0.6214 | 0.5810 | 0.6437 |

---

## Feature B Results

| Model | Accuracy | F1-score | ROC-AUC |
|---|---|---|---|
| Logistic Regression | 0.6223 | 0.6089 | 0.6474 |
| Hinge-loss Linear SVM | 0.6302 | 0.6238 | 0.6636 |
| FT-Transformer | 0.6345 | 0.6265 | 0.6542 |

---

## Feature C Results

| Model | Accuracy | F1-score | ROC-AUC |
|---|---|---|---|
| Logistic Regression | 0.6375 | 0.6270 | 0.6741 |
| Hinge-loss Linear SVM | 0.6397 | 0.6334 | 0.6800 |
| FT-Transformer | 0.6296 | 0.6036 | 0.6639 |

---

## Additional Feature A Full-Dataset Results

Additional experiments were conducted on the original full-dataset setting for Feature A.

The full-dataset setting consistently achieved stronger performance compared with the sampled setting.

| Model | Accuracy | F1-score | ROC-AUC |
|---|---|---|---|
| Logistic Regression | 0.7138 | 0.7162 | 0.7876 |
| Hinge-loss Linear SVM | 0.7137 | 0.7173 | 0.7874 |
| FT-Transformer | 0.7152 | 0.7233 | 0.7894 |

These results suggest that larger training scale and stronger statistical coverage remain highly important for recommendation tasks.

---

# Overall Experimental Observations

- The experiments investigate how increasing feature complexity affects models with different levels of model complexity.
- Results show that introducing higher-dimensional engineered features does not always lead to consistent performance improvements across all models.
- Traditional models such as Logistic Regression and Hinge-loss Linear SVM remained competitive even when using simpler feature sets.
- More complex models benefited more noticeably from interaction-based and embedding-based features, but also showed higher variance and sensitivity under repeated sampled experiments.
- Additional experiments comparing the full-dataset and same-seed sampled settings on Feature A showed that larger training scale consistently improved performance across all models.
- This suggests that dataset scale and statistical coverage remain highly important even when advanced feature engineering and complex models are used.
- Overall, the results indicate that feature engineering, model complexity, and training data scale should be considered together rather than independently when designing recommendation systems.

---

# Limitations and Future Work

- Due to computational limitations and project time constraints, full-dataset experiments were only conducted for Feature A.
- Feature B and Feature C contain substantially higher-dimensional engineered features and embedding representations, resulting in significantly higher training cost and runtime.
- As a result, Feature B and Feature C were evaluated using the repeated same-seed sampled setting instead of the original full dataset.
- Future work could explore larger-scale training environments or GPU-based distributed training to evaluate whether higher-dimensional features provide greater advantages under full-dataset conditions.
- Additional future directions may include testing more advanced deep recommendation architectures and exploring alternative collaborative filtering embedding methods.
