# Feature B — Interaction Feature Construction

## Leakage-Safe Data Pipeline

To avoid data leakage:

1. The original ratings dataset is first sampled in a stratified way.
2. The sampled dataset is then split into train/test sets.
3. User-level, item-level, global statistical features, and all interaction features are computed using only the training set.
4. The test set only uses statistics learned from the corresponding training set.

This ensures:

- no test information leakage
- fair model evaluation
- consistent repeated-split evaluation
- correct machine learning workflow

---

## Feature B Construction

Feature B extends Feature A by adding interaction-based and high-dimensional engineered features.

Feature B includes all 14 Feature A features and additional feature groups.

### 1. Base Statistical Features from Feature A

User features:

- `user_avg_rating`
- `user_rating_count`
- `user_rating_std`
- `user_like_count`
- `user_like_ratio`
- `user_rating_timespan`
- `user_avg_gap_days`

Movie features:

- `item_avg_rating`
- `item_rating_count`
- `item_rating_std`
- `item_like_count`
- `item_like_ratio`

Global and temporal features:

- `global_mean`
- `movie_age_at_rating`

---

### 2. Bias and Interaction Features

Feature B adds user-item interaction features such as:

- `user_minus_global`
- `item_minus_global`
- `user_minus_item`
- `user_item_avg_abs_diff`
- `user_item_count_product`
- `user_item_like_ratio_diff`
- `user_item_like_ratio_product`
- `user_activity_item_popularity_ratio`
- `item_popularity_user_activity_ratio`
- `rating_std_interaction`

These features capture the relationship between user preference patterns and movie-level statistics.

---

### 3. Log-Transformed Features

To reduce the effect of highly skewed count-based features, Feature B includes log-transformed features such as:

- `user_rating_count_log`
- `item_rating_count_log`
- `user_like_count_log`
- `item_like_count_log`
- `user_rating_timespan_log`
- `user_avg_gap_days_log`

---

### 4. Genre One-Hot Features

Movie genres are transformed into multi-hot genre indicators.

Examples include:

- `genre_Action`
- `genre_Comedy`
- `genre_Drama`
- `genre_Thriller`
- `genre_Romance`

These features allow the models to use genre-level movie information.

---

### 5. Time-Based Features

Feature B also includes rating-time features:

- `rating_hour`
- `rating_day_of_week`
- `rating_month`

These features capture simple temporal behavior patterns in user ratings.

---

### 6. Pairwise Cross Features

Controlled pairwise interaction features are generated from selected user, item, and bias features.

Examples include:

- `user_avg_rating_x_item_avg_rating`
- `user_like_ratio_x_item_like_ratio`
- `movie_age_at_rating_x_user_minus_item`
- `user_minus_global_x_item_minus_global`

These cross features increase feature complexity and allow linear models to capture more nonlinear relationships.

---

## Final Feature Count

Each Feature B dataset contains:

- `122 columns` in total
- `119 engineered features`
- `2 ID columns`: `userId`, `movieId`
- `1 target column`: `label`

---

## Repeated Split Summary

The Feature B data is generated using:

- `10 repeated stratified train/test splits`
- `80% training`
- `20% testing`
- different random seeds for each repetition

Each repeat contains approximately:

- `160,000 training instances`
- `39,999 testing instances`

The label ratio is preserved across train and test sets.

---

## Output Files

For each repeat, the following files are saved:

- `raw_train.csv`
- `raw_test.csv`
- `feature_B_train.csv`
- `feature_B_test.csv`
  
A summary file is also saved:

- `feature_B_split_summary.csv`
---

# Main Experimental Results

The following results are based on the repeated same-seed sampled setting and are averaged across 10 repeated experiments.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.6223 ± 0.0035 | 0.6310 ± 0.0031 | 0.5884 ± 0.0096 | 0.6089 ± 0.0058 | 0.6474 ± 0.0022 |
| Hinge-loss Linear SVM | 0.6302 ± 0.0059 | 0.6344 ± 0.0060 | 0.6137 ± 0.0094 | 0.6238 ± 0.0069 | 0.6636 ± 0.0072 |
| FT-Transformer | 0.6345 ± 0.0087 | 0.6398 ± 0.0090 | 0.6168 ± 0.0578 | 0.6265 ± 0.0274 | 0.6542 ± 0.0083 |

---

# Experimental Observations

- Feature B introduces substantially higher-dimensional engineered interaction features compared with Feature A.
- FT-Transformer achieved the strongest overall accuracy under Feature B, suggesting that higher-capacity models can better exploit complex interaction-based features.
- Hinge-loss Linear SVM achieved competitive performance across all evaluation metrics.
- Logistic Regression remained relatively stable but showed weaker performance compared with higher-capacity models.
- The increased variance of FT-Transformer indicates higher sensitivity to sampled training distributions under repeated experiments.


