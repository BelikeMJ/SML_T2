
# Models

Three models with different model complexities are compared.

| Model | Complexity |
|---|---|
| Logistic Regression | Simple |
| Linear SVM (Hinge Loss) | Medium |
| FT-Transformer | Complex |

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
