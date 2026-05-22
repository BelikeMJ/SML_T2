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
