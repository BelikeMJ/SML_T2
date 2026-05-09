
# Experimental Design

This project studies the trade-off between feature engineering and model complexity in user preference prediction.

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
