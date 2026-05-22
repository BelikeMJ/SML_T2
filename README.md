# Leakage-Safe Data Pipeline

To avoid data leakage:

1. The dataset is first split into train/test sets.
2. All statistical features are computed ONLY from the training set.


This ensures:

- no future information leakage
- fair evaluation
- correct machine learning workflow


---

# Experimental Settings

Two Feature A experimental settings are provided in this repository.

## 1. Full-Dataset Setting

This setting uses the original MovieLens ratings dataset without sampling.

Characteristics:

- larger training scale
- higher data coverage
- stronger statistical stability
- higher overall predictive accuracy

Files related to this setting include:

- `LR_FeatureA_FullDataset.ipynb`
- `SVM_FeatureA_FullDataset.ipynb`
- `FT_FeatureA_FullDataset.ipynb`

---

## 2. Same-Seed Sampled Setting

This setting uses stratified sampled splits aligned with Feature B and Feature C.

Characteristics:

- same random seeds
- same repeated train/test splits
- fair feature-complexity comparison
- controlled experimental setting

Files related to this setting include:

- `LR_FeatureA_SameSeedSampled.ipynb`
- `SVM_FeatureA_SameSeedSampled.ipynb`
- `FT_FeatureA_SameSeedSampled.ipynb`

This setting is used as the main experimental configuration for comparing Feature A, Feature B, and Feature C.

---

# Feature A Construction 

Feature A focuses on statistical and behavioral features extracted from historical user and movie interactions.

Constructed features include:

## User Features

- `user_avg_rating`
- `user_rating_count`
- `user_rating_std`
- `user_like_count`
- `user_like_ratio`
- `user_rating_timespan`
- `user_avg_gap_days`

## Movie Features

- `item_avg_rating`
- `item_rating_count`
- `item_rating_std`
- `item_like_count`
- `item_like_ratio`

## Global Features

- `global_mean`

## Temporal Feature

- `movie_age_at_rating`

Total engineered features:

- `14 features`

---

# Cross Validation Strategy

This project implements:

- `10 repeated stratified train/test splits`

with:

- `80% training`
- `20% testing`

Different random seeds are used for each repetition.

The cross-validation procedure was implemented from scratch without using third-party cross-validation utilities.

---

# Main Experimental Results

Two experimental settings are reported for Feature A.

---

# 1. Full-Dataset Results

The following results are based on the full-dataset setting and are averaged across 10 repeated experiments.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.7138 ± 0.0002 | 0.7114 ± 0.0013 | 0.7213 ± 0.0018 | 0.7162 ± 0.0003 | 0.7876 ± 0.0003 |
| Hinge-loss Linear SVM | 0.7137 ± 0.0003 | 0.7093 ± 0.0016 | 0.7256 ± 0.0019 | 0.7173 ± 0.0004 | 0.7874 ± 0.0004 |
| FT-Transformer | 0.7152 ± 0.0008 | 0.7066 ± 0.0024 | 0.7409 ± 0.0075 | 0.7233 ± 0.0012 | 0.7894 ± 0.0010 |

---

# 2. Same-Seed Sampled Results

The following results are based on the same-seed sampled setting and are used as the primary experimental configuration for comparing Feature A, Feature B, and Feature C.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.6344 ± 0.0025 | 0.6355 ± 0.0022 | 0.6294 ± 0.0053 | 0.6324 ± 0.0034 | 0.6668 ± 0.0021 |
| Hinge-loss Linear SVM | 0.6365 ± 0.0026 | 0.6385 ± 0.0026 | 0.6288 ± 0.0065 | 0.6336 ± 0.0038 | 0.6768 ± 0.0037 |
| FT-Transformer | 0.6214 ± 0.0145 | 0.6490 ± 0.0114 | 0.5279 ± 0.0508 | 0.5810 ± 0.0326 | 0.6437 ± 0.0163 |

---

# Experimental Observations

- The full-dataset setting achieved substantially stronger performance due to larger training scale and improved statistical coverage.
- The same-seed sampled setting is used as the primary experimental configuration for fair comparison across Feature A, Feature B, and Feature C.
- Hinge-loss Linear SVM achieved the strongest performance under the sampled setting.
- Logistic Regression remained competitive, indicating that Feature A already provides useful linear statistical signals.
- FT-Transformer achieved the best overall performance under the full-dataset setting but showed reduced stability under the sampled setting, likely due to the smaller training scale and limited feature complexity of Feature A.
