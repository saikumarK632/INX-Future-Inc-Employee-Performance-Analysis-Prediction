# Summary – INX Future Inc Employee Performance

## 1. Project summary
- **Data:** 1,200 employees, 26 factors, target is the performance rating (2 Good 16.2%, 3 Excellent 72.8%, 4 Outstanding 11.0%).
- **Algorithms:** Logistic Regression, Decision Tree, Random Forest, Gradient Boosting, Support Vector Machine and K Nearest Neighbours were compared with a baseline. **Gradient Boosting** was best and was tuned with grid search and 5 fold cross validation.
- **Most important factors:** environment satisfaction, last salary hike percentage and years since last promotion (selected by three independent methods).
- **Tools:** Python with pandas, NumPy, SciPy, scikit-learn, Matplotlib and Seaborn in Jupyter notebooks.
- **Result:** the model using all factors predicts the rating of unseen employees with **92.9 percent accuracy** (macro F1 0.89), compared with 72.9 percent for always guessing rating 3. A model restricted to information available at hiring reaches only 64.2 percent and is **not useful for hiring**.

## 2. Feature selection and engineering
**Most important features and why.** Environment satisfaction, last salary hike percentage and years since last promotion rank first, second and third on average across effect size, random forest importance and permutation importance. Department and job role come next.

**Transformations.** Ordered scales (satisfaction, education, work life balance, job level) stay numeric. Unordered categories (department, job role, education background, marital status, business travel) are one hot encoded. Two value columns (gender, overtime, attrition) become 0 or 1. Numeric measurements are standardised. All of this is done inside the model pipeline. No dimensionality reduction was applied and no new derived columns were created, because the original factors are already interpretable.

**Correlation among features.** Experience related columns are strongly correlated (for example years at the company with years in the current role 0.76, and with years with the current manager 0.76; job level with total experience 0.78). This was checked and tree based models cope with it. Because the top three factors also come out on top in the permutation ranking, they do not depend on this overlap.

## 3. Results, analysis and insights

### Answer 1 – Department wise performance
| Department | Employees | Average rating | Rated 2 (lowest) |
|---|---|---|---|
| Development | 361 | 3.09 | 3.6% |
| Data Science | 20 | 3.05 | 5.0% |
| Human Resources | 54 | 2.93 | 18.5% |
| Research & Development | 343 | 2.92 | 19.8% |
| Sales | 373 | 2.86 | 23.3% |
| Finance | 49 | 2.78 | 30.6% |

Differences are statistically significant (p below 0.001). **Finance and Sales are the weakest.** Sales is the biggest concern in numbers because of its size (87 employees rated 2). Data Science has only 20 employees, so treat its figure with care.

### Answer 2 – Top three factors
1. **Environment satisfaction.** About 40 percent of employees scoring 1 or 2 are rated 2, versus under 1 percent of those scoring 3 or 4. **188 of the 194 employees (96.9 percent) rated 2 have an environment satisfaction of 1 or 2.**
2. **Last salary hike.** Of employees with a hike of 19 percent or more, 45.9 percent are rated 4, versus 2.0 percent among those with a smaller hike.
3. **Years since last promotion.** Employees who waited two or more years for a promotion are rated 2 in 28.8 percent of cases, versus 9.0 percent for others.

### Answer 3 – Prediction model
| | Model A – all factors | Model B – hiring time factors |
|---|---|---|
| Algorithm | Gradient Boosting | Random Forest |
| Test accuracy | 92.9% | 64.2% |
| Macro F1 | 0.89 | 0.37 |
| Baseline accuracy (always rating 3) | 72.9% | 72.9% |

Model A recognises rating 2 (F1 0.87), rating 3 (0.96) and rating 4 (0.83) well. **Model B is worse than the baseline**, meaning information available before joining (age, education, past experience, role, hourly rate and so on) does not predict later performance in this data. The drivers of performance arise after joining, so the trained model should be used **after a probation or settling in period**, not to reject candidates. Files: `src/models/model_a_all_factors.joblib` and `model_b_hiring_factors.joblib`; usage in `predict_model.ipynb`.

### Answer 4 – Recommendations
1. **Fix the working environment first.** Run an environment satisfaction review with employees scoring 1 or 2 (472 people, 39 percent of staff). Since almost all low ratings sit in this group, improving it is the most direct route to better performance and to client satisfaction.
2. **Review promotion waiting time.** Set a review point for anyone without promotion or a clear development plan after two years.
3. **Make salary hikes transparent and performance linked.** The highest hikes go with many more outstanding ratings, so a clear link between recognition and results is likely to motivate employees.
4. **Focus on Finance and Sales.** Start support programmes (manager coaching, workload and role review) in these departments.
5. **Use the model to protect morale.** Apply Model A to find the small group with a high probability of rating 2 and offer support (coaching, environment fixes, promotion planning) before any penalty. This targets action at the people concerned and leaves the rest of the company untouched.
6. **Do not use the model for hiring decisions.** Use it after joining, and monitor new joiners' environment satisfaction in their first months.

### More business insights
- Low environment satisfaction is spread across all departments (30 to 43 percent of staff in each), so department differences are not explained by this factor alone and deserve a separate look at management and workload.
- Employees working overtime are less often rated 2 (11.0 percent versus 18.3 percent without overtime), which suggests overtime is not the cause of low ratings.
- Gender, marital status and business travel show no meaningful relationship with the rating, and attrition differences are not statistically significant.
- Lowest rated employees have on average longer service, more years in the same role and more years with the same manager (for example 3.7 years since promotion versus 1.9), pointing to stagnation.

## 4. Limitations
- The results show **association, not proven cause**. Actions such as raising environment satisfaction should be tested and monitored.
- The data is a single snapshot of 1,200 employees; only 26 employees with rating 4 are in the test set, so the rating 4 figures are less stable.
- Model A depends on factors such as environment satisfaction that must be collected regularly to keep predictions current.
