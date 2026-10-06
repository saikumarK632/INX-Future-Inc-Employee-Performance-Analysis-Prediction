# INX-Future-Inc-Employee-Performance-Analysis-Prediction

# INX Future Inc – Employee Performance Analysis & Prediction

A complete **Data Science and Machine Learning project** to analyze employee performance, identify the key factors associated with performance, compare department-level performance, and build models for employee performance prediction.

The project uses real-world employee data from **INX Future Inc** and combines **Exploratory Data Analysis (EDA), statistical testing, feature importance analysis, machine learning, model evaluation, and business recommendations**.

---

## 📌 Project Overview

INX Future Inc was experiencing a decline in employee performance, increasing service-delivery escalations, and an 8-percentage-point decrease in client satisfaction.

The business wanted to understand:

1. How employee performance differs across departments.
2. Which factors are most strongly associated with employee performance.
3. Whether employee performance can be predicted using machine learning.
4. Whether performance can be predicted using only information available at the time of hiring.
5. What actions the organization can take to improve employee performance.

This project addresses all of these questions using a structured data science workflow.

---

## 🎯 Business Objectives

The main objectives of this project are:

* Analyze employee performance across departments.
* Identify the **top three factors associated with performance**.
* Build and compare multiple machine learning classification models.
* Develop a high-performing model for monitoring current employees.
* Investigate whether employee performance can be predicted during hiring.
* Provide actionable recommendations to improve employee performance.
* Avoid using machine learning blindly for employee decisions and instead use predictions to support targeted interventions.

---

## 📊 Dataset

The dataset contains:

* **1,200 employees**
* **26 employee-related factors**
* **1 target variable**
* **28 columns in total**, including employee number and performance rating.

### Target Variable

`PerformanceRating`

| Rating | Meaning     | Percentage |
| ------ | ----------- | ---------: |
| 2      | Good        |      16.2% |
| 3      | Excellent   |      72.8% |
| 4      | Outstanding |      11.0% |

The dataset is imbalanced because most employees have a rating of 3.

Therefore, **accuracy alone is not sufficient** for evaluating the models. Macro F1-score is also used to give equal importance to all performance classes.

---

## 🔎 Project Workflow

```text
Raw Employee Data
        ↓
Data Cleaning & Validation
        ↓
Exploratory Data Analysis
        ↓
Department Performance Analysis
        ↓
Statistical Testing
        ↓
Feature Importance Analysis
        ↓
Top 3 Factor Identification
        ↓
Feature Preprocessing
        ↓
Multiple Model Comparison
        ↓
Hyperparameter Tuning
        ↓
Final Model Evaluation
        ↓
Prediction
        ↓
Business Insights & Recommendations
```

---

## 🧹 Data Preparation

The data preparation stage included:

* Checking dataset dimensions.
* Checking missing values.
* Checking duplicate records.
* Checking employee number uniqueness.
* Validating experience-related fields.
* Identifying potential outliers.
* Preserving genuine outliers instead of automatically removing them.
* Encoding categorical variables.
* Keeping meaningful ordered variables as numerical values.
* Standardizing numerical variables where required.
* Building preprocessing pipelines to ensure consistent processing during prediction.

### Data Quality

The dataset contains:

* **1,200 rows**
* **No missing values**
* **No duplicate rows**
* **Unique employee identifiers**

---

# 📈 Exploratory Data Analysis

## Performance Distribution

The employee performance distribution is:

* **16.2%** Good
* **72.8%** Excellent
* **11.0%** Outstanding

This imbalance was considered during model evaluation.

---

# 🏢 Department-Wise Performance

The analysis found meaningful differences between departments.

| Department             | Employees | Average Rating | Rating 2 |
| ---------------------- | --------: | -------------: | -------: |
| Development            |       361 |           3.09 |     3.6% |
| Data Science           |        20 |           3.05 |     5.0% |
| Human Resources        |        54 |           2.93 |    18.5% |
| Research & Development |       343 |           2.92 |    19.8% |
| Sales                  |       373 |           2.86 |    23.3% |
| Finance                |        49 |           2.78 |    30.6% |

Statistical testing confirmed that department and performance rating are significantly associated.

* Kruskal-Wallis test: **p < 0.001**
* Chi-square test: **p < 0.001**

### Key Finding

**Development has the strongest overall performance, while Finance has the weakest average performance.**

Finance has approximately **30.6% of employees rated 2**, while Sales has **23.3%**.

Sales is particularly important because it is the largest department and therefore contains a large number of lower-rated employees.

> Data Science has only 20 employees, so its department-level result should be interpreted cautiously.

---

# ⭐ Top 3 Factors Associated With Employee Performance

Three independent approaches were used:

1. Statistical effect size
2. Random Forest feature importance
3. Permutation importance

The same three factors consistently ranked at the top.

## 🥇 1. Environment Satisfaction

`EmpEnvironmentSatisfaction`

This is the strongest factor identified in the analysis.

Employees with environment satisfaction levels of **1 or 2** had approximately **40%** of employees rated 2.

In contrast, among employees with satisfaction levels of **3 or 4**, only about **0.8%** were rated 2.

This is the clearest signal found in the dataset.

### Important observation

There were **472 employees** with low or medium environment satisfaction.

Among the 194 employees with the lowest performance rating, **188 employees** had environment satisfaction of 1 or 2.

That means approximately **96.9% of the lowest-rated employees were in the low/medium environment-satisfaction group.**

---

## 🥈 2. Last Salary Hike Percentage

`EmpLastSalaryHikePercent`

Employees receiving larger salary increases showed substantially more outstanding performance.

Employees with salary hikes above approximately **18%** had:

* Average rating: **3.30**
* Rating 4: **45.9%**

Compared with employees receiving smaller increases, where the percentage rated 4 was much lower.

This suggests that compensation and recognition are strongly associated with performance in this dataset.

---

## 🥉 3. Years Since Last Promotion

`YearsSinceLastPromotion`

Employees who had recently received a promotion had substantially fewer low performance ratings.

| Promotion Gap     | Rating 2 |
| ----------------- | -------: |
| Up to 1 year      |     9.0% |
| 1–3 years         |    30.2% |
| More than 3 years |    27.9% |

Employees with long promotion gaps also tended to spend more years in the same role and with the same manager.

This suggests a possible **career stagnation signal**.

---

# 👤 Profile of Lower-Performing Employees

Employees with performance rating 2 were compared with all other employees.

The lower-rated group had, on average:

| Factor                     | Lower-Rated Employees | Others |
| -------------------------- | --------------------: | -----: |
| Environment Satisfaction   |                  1.58 |   2.93 |
| Years at Company           |                  9.10 |   6.69 |
| Years Since Promotion      |                  3.70 |   1.90 |
| Years in Current Role      |                  5.79 |   4.00 |
| Years With Current Manager |                  5.35 |   3.86 |

### Interpretation

Lower-performing employees tend to have:

* Lower environment satisfaction.
* Longer time at the company.
* Longer time in the same role.
* Longer time with the same manager.
* Longer gaps since their last promotion.

This points toward possible issues involving **work environment, career growth, recognition, and role stagnation**.

---

# 🤖 Machine Learning

Multiple classification algorithms were compared.

### Models Tested

* Logistic Regression
* Decision Tree
* Random Forest
* Gradient Boosting
* Support Vector Machine
* K Nearest Neighbours
* Most Frequent Class Baseline

Because the target variable is imbalanced, **Macro F1** was selected as the primary model comparison metric.

---

# 🏆 Model A – Current Employee Performance

Model A uses all available employee factors.

### Cross-Validation Results

| Model                  | CV Accuracy | CV Macro F1 |
| ---------------------- | ----------: | ----------: |
| **Gradient Boosting**  |  **93.12%** |   **0.893** |
| Decision Tree          |      88.33% |       0.832 |
| Random Forest          |      90.31% |       0.821 |
| Support Vector Machine |      76.98% |       0.700 |
| Logistic Regression    |      73.65% |       0.668 |
| K Nearest Neighbours   |      74.38% |       0.405 |
| Baseline               |      72.81% |       0.281 |

### Selected Model

**Gradient Boosting**

Best parameters:

```text
learning_rate = 0.1
max_depth = 3
n_estimators = 100
```

---

# 📊 Final Model A Performance

The final model was evaluated on **240 previously unseen employees**.

| Metric            | Gradient Boosting |
| ----------------- | ----------------: |
| Accuracy          |         **92.9%** |
| Macro F1          |         **0.886** |
| Weighted F1       |         **0.928** |
| Baseline Accuracy |             72.9% |

### Per-Class Performance

| Rating          | Precision | Recall |   F1 |
| --------------- | --------: | -----: | ---: |
| Good (2)        |      0.89 |   0.85 | 0.87 |
| Excellent (3)   |      0.94 |   0.97 | 0.96 |
| Outstanding (4) |      0.91 |   0.77 | 0.83 |

The model performs well across all three performance categories.

---

# ⚠️ Model B – Hiring-Time Prediction

A second model was developed using only information that would realistically be available at the time of hiring.

Examples include:

* Age
* Education
* Previous experience
* Job level
* Job role
* Department
* Hourly rate
* Distance from home
* Number of companies previously worked for

### Result

The best Model B algorithm was **Random Forest**.

However:

| Metric            |   Model B |
| ----------------- | --------: |
| Accuracy          | **64.2%** |
| Macro F1          | **0.366** |
| Baseline Accuracy | **72.9%** |

The model was **worse than simply predicting the most common class**.

It also failed to correctly identify any Outstanding employees in the test set.

---

# 🚨 Important Business Conclusion

This is one of the most important findings of the project:

> **Employee information available at the time of hiring was not sufficient to reliably predict future performance in this dataset.**

Therefore, the project **does not recommend using the model to reject or select candidates during hiring**.

Instead, the strongest performance-related factors identified in the analysis—such as environment satisfaction, salary hike, and promotion timing—mostly become meaningful **after employees join the organization**.

### Recommended approach

Use Model A after employees have joined and had sufficient time to settle into their roles.

For example:

```text
Employee joins
      ↓
Initial settling/probation period
      ↓
Collect employee experience factors
      ↓
Run performance prediction
      ↓
Identify employees needing support
      ↓
Provide targeted intervention
```

---

# 💡 Business Recommendations

## 1. Improve the Work Environment

Environment satisfaction is the strongest signal in the analysis.

The organization should regularly identify employees with low environment satisfaction and investigate:

* Manager relationships
* Workload
* Team culture
* Work conditions
* Role clarity
* Support from management

---

## 2. Review Promotion Delays

Employees with long promotion gaps have significantly higher rates of low performance.

The organization should establish career-development reviews for employees who have remained in the same role for extended periods.

---

## 3. Improve Salary and Recognition Policies

Higher salary hikes are strongly associated with higher performance ratings.

The organization should make compensation and recognition processes:

* Transparent
* Performance-linked
* Consistent
* Clearly communicated

---

## 4. Focus on Finance and Sales

Finance has the highest percentage of low-rated employees.

Sales is also important because it is the largest department and therefore has a substantial number of lower-rated employees.

Targeted interventions could include:

* Manager coaching
* Workload analysis
* Role clarification
* Employee engagement programs
* Career-development planning

---

## 5. Use Predictions for Employee Support

The model should not be used simply to label employees as "good" or "bad".

Instead, employees predicted to have a high probability of low performance can be offered:

* Coaching
* Training
* Career-development discussions
* Manager support
* Work-environment improvements

The objective should be **early support rather than punishment**.

---

# 🔬 Statistical and Analytical Methods

The project uses multiple analytical techniques to make the conclusions more reliable.

### Statistical Analysis

* Spearman correlation
* Cramér's V
* Kruskal-Wallis test
* Chi-square test
* Correlation analysis

### Feature Importance

* Statistical effect size
* Random Forest importance
* Permutation importance
* Combined ranking

### Machine Learning

* Logistic Regression
* Decision Tree
* Random Forest
* Gradient Boosting
* Support Vector Machine
* K Nearest Neighbours

### Model Validation

* Stratified 80/20 train-test split
* 5-fold cross-validation
* Grid search
* Macro F1
* Accuracy
* Precision
* Recall
* F1-score
* Confusion matrix

---

# 🛠️ Technology Stack

### Programming

* Python

### Data Analysis

* Pandas
* NumPy
* SciPy

### Machine Learning

* Scikit-learn

### Visualization

* Matplotlib
* Seaborn

### Model Persistence

* Joblib

### Development Environment

* Jupyter Notebook

### Dataset Format

* Excel
* CSV

---

# 📁 Project Structure

```text
INX_Future_Employee_Performance_Project/
│
├── README.md
│
├── Project Summary/
│   ├── Summary.md
│   ├── Requirement.md
│   └── Analysis.md
│
├── references/
│   ├── data_dictionary.csv
│   ├── Project_Brief_INX_Future_Employee_Performance.pdf
│   └── Project_Submission_Guidelines.pdf
│
├── data/
│   ├── raw/
│   │   ├── INX_Future_Inc_Employee_Performance_CDS_Project2_Data_V1_8.xls
│   │   └── README.txt
│   │
│   ├── processed/
│   │   ├── employee_cleaned.csv
│   │   ├── employee_labelled.csv
│   │   ├── feature_ranking.csv
│   │   ├── model_comparison_all_factors.csv
│   │   └── model_comparison_hiring_factors.csv
│   │
│   └── external/
│
├── src/
│   │
│   ├── Data Processing/
│   │   ├── data_processing.ipynb
│   │   └── data_exploratory_analysis.ipynb
│   │
│   ├── models/
│   │   ├── train_model.ipynb
│   │   ├── predict_model.ipynb
│   │   ├── model_a_all_factors.joblib
│   │   ├── model_b_hiring_factors.joblib
│   │   └── model_metadata.json
│   │
│   └── visualization/
│       ├── visualize.ipynb
│       └── figures/
│
└── ...
```

---

# ▶️ How to Run the Project

## 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd INX_Future_Employee_Performance_Project
```

## 2. Install dependencies

```bash
pip install pandas numpy scipy scikit-learn matplotlib seaborn joblib xlrd jupyter
```

## 3. Start Jupyter Notebook

```bash
jupyter notebook
```

## 4. Run notebooks in this order

### Step 1 – Data Processing

```text
src/Data Processing/data_processing.ipynb
```

### Step 2 – Exploratory Data Analysis

```text
src/Data Processing/data_exploratory_analysis.ipynb
```

### Step 3 – Train Models

```text
src/models/train_model.ipynb
```

### Step 4 – Make Predictions

```text
src/models/predict_model.ipynb
```

### Step 5 – Generate Visualizations

```text
src/visualization/visualize.ipynb
```

---

# 📌 Key Takeaways

The most important conclusions from the project are:

### 1. Employee environment matters

Environment satisfaction is the strongest factor associated with performance.

### 2. Recognition matters

Higher salary hikes are strongly associated with outstanding performance.

### 3. Career progression matters

Long promotion gaps are associated with higher levels of low performance.

### 4. Department performance differs

Finance and Sales require more attention, while Development performs strongly.

### 5. Machine learning can identify current performance

The Gradient Boosting model achieved:

**92.9% test accuracy and 0.886 macro F1.**

### 6. Hiring prediction is not reliable

The hiring-time model achieved only:

**64.2% accuracy and 0.366 macro F1**, below the 72.9% baseline.

Therefore, it should **not** be used for hiring decisions.

---

# ⚠️ Limitations

This analysis has several limitations:

* The dataset contains only **1,200 employees**.
* It represents a single snapshot rather than longitudinal employee records.
* Only **26 rating-4 employees** were present in the test set, so the Outstanding-class metrics are less stable.
* The analysis identifies **associations, not proven causal relationships**.
* Some experience-related variables are strongly correlated.
* Model A requires employee factors that are only available after joining.
* Employee performance is influenced by factors that may not be captured in the dataset.

Therefore, the findings should support business decisions rather than replace human judgment.

---

# 🤝 Responsible Use

Employee performance prediction can have significant consequences.

This project should be used to:

* Identify employees who may need support.
* Understand organizational issues.
* Improve employee experience.
* Support career-development planning.
* Guide management interventions.

It should **not** be used as the sole basis for:

* Rejecting job candidates.
* Terminating employees.
* Reducing compensation.
* Penalizing employees.

Human review and organizational context should always be considered.

---

# 📚 Project Outputs

The project produces:

* Cleaned employee dataset
* Labelled employee dataset
* Feature ranking
* Model comparison results
* Trained machine learning models
* Model metadata
* Prediction workflow
* Department analysis
* Performance visualizations
* Business recommendations

# ⭐ Final Project Conclusion

This project demonstrates an end-to-end approach to solving a real-world employee analytics problem.

The analysis found that **environment satisfaction, salary hike percentage, and promotion timing** are the three strongest factors associated with employee performance.

A Gradient Boosting model using all available employee factors achieved **92.9% accuracy** and **0.886 macro F1** on previously unseen employees.

However, the experiment also produced an equally important negative finding: a model restricted to information available at hiring performed worse than a simple baseline. This indicates that **future employee performance cannot be reliably predicted from hiring-time information alone using this dataset**.

The recommended business strategy is therefore not to use machine learning to eliminate candidates, but to use it **after employees join to identify potential performance issues early and provide targeted support**.

