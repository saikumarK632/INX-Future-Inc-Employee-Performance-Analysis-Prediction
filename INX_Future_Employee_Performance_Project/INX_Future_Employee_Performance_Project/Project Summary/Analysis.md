# Analysis – Approach and Choices

## 1. Data preparation (`src/Data Processing/data_processing.ipynb`)
- **Quality:** 1,200 rows, no missing values, no duplicate rows, every employee number unique.
- **Consistency checks:** experience columns were checked against each other and against age. See the notebook for the count of rows failing each check.
- **Outliers:** flagged using the interquartile range rule and **kept**, because they are genuine values (for example long experience) and the selected models are not sensitive to them.
- **Two processed datasets:** `employee_cleaned.csv` (used for modelling) and `employee_labelled.csv` (readable labels for reporting).

## 2. Exploratory analysis (`src/Data Processing/data_exploratory_analysis.ipynb`)
- Target distribution: 72.8 percent rated 3, 16.2 percent rated 2, 11.0 percent rated 4 (imbalanced, so accuracy alone is misleading).
- Department comparison with average rating, rating mix, Kruskal-Wallis and chi-square tests.
- **Three independent factor rankings**, combined by average rank:
  1. Effect size against the rating (Spearman correlation for numbers, Cramér's V for categories)
  2. Random forest importance (one hot columns added back to their original factor)
  3. Permutation importance on held out data
- Profile of the lowest rated employees, and a check of correlated numeric factors.

## 3. Modelling (`src/models/train_model.ipynb`)
| Choice | Reason |
|---|---|
| 80/20 stratified split | Keeps the rating proportions the same in training and test data |
| 5 fold cross validation on training data | Compares and tunes models without touching the test data |
| Macro F1 as main score | Gives equal weight to each rating despite the imbalance |
| Seven candidates including a baseline | Shows what the models add over always guessing rating 3 |
| Pipeline with encoding and scaling inside | The same steps are applied to new employees automatically |
| Grid search on Random Forest and Gradient Boosting | The two strongest candidates |
| Two models (A all factors, B hiring time factors) | Because the business wants to use a model when hiring, and the strongest factors only exist after joining |

## 4. Algorithms not used
Neural networks and dimensionality reduction (principal component analysis) were not used. The dataset is small (1,200 rows), the factors are already few and meaningful, and principal component analysis would make the factors harder to explain to the chief executive officer. Feature importance and statistical tests give clearer answers.
