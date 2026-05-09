
# Models

Three models with different model complexities are compared.

| Model | Complexity |
|---|---|
| Logistic Regression | Simple |
| Linear SVM (Hinge Loss) | Medium |
| FT-Transformer | Complex |

---

# FT-Transformer

This project uses the official implementation of FT-Transformer from:

- Yandex Research
- Paper:  
  *Revisiting Deep Learning Models for Tabular Data*

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
