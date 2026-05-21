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
