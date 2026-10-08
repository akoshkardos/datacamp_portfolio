# Recipe Site Traffic: Data Science Practical Exam

This project was the final practical exam for the DataCamp **Professional Data Scientist** certification. It brought together the skills I developed across the certification’s two skill tracks and followed two timed exams, **DS101** and **DS201**.

## Business problem

The exam presents a business scenario for Tasty Bytes, a recipe website. The business question and full task instructions are in [`instructions.pdf`](instructions.pdf). The goal is to use recipe data to understand what is associated with high traffic and help the business choose recipes to feature, with a target of at least **80% of featured recipes generating high traffic**.

## What I did

I worked through the end-to-end data science workflow:

1. **Validated and cleaned the data:** checked columns, duplicates, missing values, categories, and numeric ranges; removed duplicate and incomplete records; standardized category and serving values; and encoded the traffic label.
2. **Explored the data:** compared recipe categories, servings, nutrition values, and traffic outcomes using summary statistics and visualizations.
3. **Prepared features for modeling:** separated the target from the predictors and one-hot encoded recipe categories.
4. **Trained and compared classifiers:** used stratified train/test splitting and cross-validated hyperparameter searches to compare logistic regression, ridge classification, a decision tree, and a random forest. Average precision was the main selection metric; I also considered precision, recall, and ROC-AUC.
5. **Evaluated the business tradeoff:** selected logistic regression for its comparable test performance and interpretability, then examined how changing its probability threshold affected the share of featured recipes that were high traffic and the number of recipes selected.
6. **Translated the results into recommendations** for the business.

## Findings and recommendations

Recipe **category** was the clearest signal of traffic in this dataset. Vegetable, potato, pork, meat, and one-dish recipes tended to perform well, while beverages, breakfast, and chicken tended to perform less well. The analysis did not find a clear reason to use nutrition values as a primary feature-selection rule.

At the default 0.50 threshold, the logistic regression model reached about **77% precision** on the held-out test set, below the 80% target. Raising the threshold to **0.65** produced roughly **85% precision** on that test set, while lowering recall to roughly 60%. This tradeoff favors showing fewer recipes with higher estimated chances of attracting traffic.

I recommend prioritizing categories that performed well, and monitoring the precision of featured recipes against the 80% target over time. If the business wants to feature weaker-performing categories, it should consider category-specific selection rules and evaluate them with new data.

## Limitations

The 0.65 threshold was selected after reviewing test-set results, so the reported test precision may be optimistic. It should be validated on a separate, future sample before being treated as a dependable operating result. The findings describe associations in this dataset and do not establish that recipe category causes traffic.

## Project files

- [`recipe_site_traffic_report.ipynb`](recipe_site_traffic_report.ipynb) — analysis, visualizations, model development, and recommendations.
- [`recipe_site_traffic_2212.csv`](recipe_site_traffic_2212.csv) — dataset used in the analysis.
- [`instructions.pdf`](instructions.pdf) — practical exam business scenario and instructions.
