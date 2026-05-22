# Leakage-Safe Data Pipeline

To avoid data leakage:

1. The dataset is first split into train/test sets.
2. All statistical features are computed ONLY from the training set.


This ensures:

- no future information leakage
- fair evaluation
- correct machine learning workflow

---

Two Feature A experimental settings are provided:

1. Full-dataset splits using the original MovieLens ratings dataset.
2. Same-seed sampled splits aligned with Feature B and Feature C for fair feature-complexity comparison.


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
