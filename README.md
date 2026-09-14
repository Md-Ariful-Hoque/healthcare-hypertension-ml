# Healthcare Hypertension Prediction Using Machine Learning

## Overview

This project demonstrates an end-to-end healthcare machine learning workflow for predicting hypertension using synthetic electronic health record (EHR) data.

The analysis emphasizes an important issue in healthcare machine learning: **temporal data leakage**. An initial modeling approach produced strong predictive performance, particularly for random forest. The cohort and feature construction were then redesigned so that predictors were restricted to information available **before the hypertension index date**.

After temporal redesign, model performance decreased substantially, illustrating how improper temporal feature construction can lead to overly optimistic estimates of predictive performance.

## Objectives

- Query and integrate healthcare data using SQL and Python
- Construct a hypertension case-control cohort
- Perform temporal cohort design and age matching
- Engineer pre-index healthcare utilization and clinical features
- Prevent temporal data leakage
- Develop logistic regression and random forest models
- Evaluate models using held-out testing and grouped cross-validation
- Compare performance before and after temporal redesign

## Data

The project uses **synthetic healthcare data** rather than real patient records.

The final temporally designed cohort included:

- 156 hypertension cases
- 156 age-matched controls
- 312 total patients
- 156 matched pairs
- 365-day pre-index observation window

Because the data are synthetic, results should not be interpreted as estimates of real-world hypertension risk.

## Machine Learning Models

Two classification models were evaluated:

1. Logistic Regression
2. Random Forest

Matched pairs were kept together during train-test splitting and cross-validation to reduce information leakage between data partitions.

## Final Model Performance

| Model | Test ROC-AUC | CV Mean ROC-AUC | CV SD |
|---|---:|---:|---:|
| Logistic Regression | 0.744 | 0.702 | 0.105 |
| Random Forest | 0.688 | 0.701 | 0.043 |

Logistic regression achieved higher ROC-AUC on the held-out test set, while grouped five-fold cross-validation showed nearly identical discrimination for the two models.

## Impact of Temporal Redesign

| Model | Original Test AUC | Temporal Test AUC | Original CV AUC | Temporal CV AUC |
|---|---:|---:|---:|---:|
| Logistic Regression | 0.787 | 0.744 | 0.758 | 0.702 |
| Random Forest | 0.892 | 0.688 | 0.911 | 0.701 |

The decline in performance after temporal redesign demonstrates the importance of ensuring that predictor information would actually have been available at the intended prediction time.

## Key Takeaway

Rigorous **cohort construction, temporal alignment, leakage prevention, and validation** can be as important as algorithm selection in healthcare machine learning.

After restricting predictors to pre-index information, the apparent advantage of random forest largely disappeared, with logistic regression and random forest producing nearly identical cross-validated ROC-AUC values.

## Tools and Technologies

- Python
- SQL
- Pandas
- NumPy
- scikit-learn
- Matplotlib
- Jupyter Notebook
- Machine Learning
- EHR Data Analysis

## Repository Contents

`healthcare_ml_analysis_final.ipynb` — Complete analysis including SQL querying, cohort construction, feature engineering, temporal redesign, machine learning, validation, and interpretation.

## Limitations

This analysis uses synthetic data and a relatively small temporally eligible cohort. Pre-index healthcare information was sparse, and most eligible hypertension cases were diagnosed around age 18. The purpose of the project is therefore methodological demonstration rather than development of a clinically deployable hypertension prediction model.

## Author

**Md Ariful Hoque**  
PhD Candidate (ABD), Biostatistics  
Florida International University
