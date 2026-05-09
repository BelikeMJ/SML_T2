
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

- **NeurIPS 2021**
- Paper:
  *Revisiting Deep Learning Models for Tabular Data*

According to the paper, FT-Transformer is a simple adaptation of the Transformer architecture for tabular machine learning tasks and demonstrated strong performance across a wide range of datasets. :contentReference[oaicite:1]{index=1}

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

Hyperparameter tuning was implemented manually.

Examples include:

## Logistic Regression

- regularization strength

## SVM

- C values

## FT-Transformer

- learning rate
- weight decay

Multiple candidate values were evaluated for each hyperparameter.

---

# Evaluation Metrics

The project evaluates models using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
