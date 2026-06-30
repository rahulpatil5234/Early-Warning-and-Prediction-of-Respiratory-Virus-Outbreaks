# Early-Warning-and-Prediction-of-Respiratory-Virus-Outbreaks
This dissertation uses primary care sentinel surveillance data to detect early signs of rising influenza activity and predict next-week outbreak risk. Key indicators, lag features, rolling trends, and seasonality were analysed across five ML models, with Random Forest performing best overall.
# Early Warning and Prediction of Respiratory Virus Outbreaks Using Public Health Surveillance Data

## Project Overview

This project focuses on the early warning and short-term prediction of respiratory virus outbreaks using public health surveillance data. The main objective of the study is to analyse whether routine surveillance indicators can be used to identify early signs of rising Influenza activity and predict the risk of an outbreak in the following week.

The project uses primary care sentinel surveillance data and applies data preprocessing, exploratory data analysis, feature engineering, machine learning modelling, model evaluation, and interpretation techniques. The final output is an interpretable machine learning framework that can support short-term outbreak warning using indicators such as tests, detections, positivity rates, lag features, rolling averages, and seasonal timing.

Although the original dataset contained multiple respiratory pathogens, including Influenza, RSV, and SARS-CoV-2, Influenza was selected as the main modelling focus because it showed the strongest and most reliable outbreak-related patterns in the available surveillance data.

---

## Background

Respiratory virus outbreaks remain a major public health concern because they can spread quickly, increase illness levels, and place pressure on healthcare systems. Influenza is especially important due to its seasonal recurrence and its impact on communities, healthcare demand, and public health planning.

Traditional surveillance systems are often used to describe current or past activity. However, public health decision-making can benefit more from early warning systems that identify outbreak risk before activity becomes severe. This project investigates whether existing surveillance data can be transformed into a practical and interpretable prediction framework for next-week Influenza outbreak risk.

---

## Problem Statement

One of the main challenges in respiratory virus surveillance is that outbreaks are often recognised only after they are already visible in routine reports. Surveillance systems collect valuable weekly data, but this data is not always converted into predictive insights.

A single indicator, such as the number of positive detections, may not be enough to identify an outbreak because detections can increase when testing volume increases. Therefore, this project considers multiple indicators together, including positivity rate, testing activity, detections, recent changes, lag values, rolling averages, and seasonal timing.

The key problem addressed in this project is:

**Can routine public health surveillance data be used to predict next-week Influenza outbreak risk in an interpretable and practical way?**

---

## Aim of the Project

The aim of this project is to develop an interpretable machine learning-based framework for the early warning and prediction of Influenza outbreaks using public health surveillance data.

---

## Research Questions

This project is guided by the following research questions:

1. What temporal and surveillance patterns are associated with rising Influenza activity?
2. Which surveillance indicators are most useful for identifying early outbreak signals?
3. Which machine learning model performs best for predicting next-week Influenza outbreak risk?
4. How interpretable and practically useful are the model outputs for supporting early warning and public health decision-making?

---

## Objectives

The main objectives of this project are:

- Collect and prepare official Influenza surveillance data from a public health source.
- Clean, filter, and reshape the raw surveillance dataset.
- Analyse trends in tests, detections, and positivity rates.
- Engineer time-based, lag-based, change-based, and rolling average features.
- Define a next-week outbreak target variable for classification.
- Train and compare five machine learning models.
- Apply time-series cross-validation and hyperparameter tuning.
- Evaluate models using accuracy, precision, recall, F1-score, and ROC-AUC.
- Identify the best-performing model and interpret the most important predictors.

---

## Dataset Description

The primary dataset used in this project was a public health sentinel surveillance dataset containing aggregated weekly respiratory virus data.

The original dataset included the following key columns:

- `survtype`
- `countryname`
- `yearweek`
- `pathogen`
- `pathogentype`
- `pathogensubtype`
- `indicator`
- `age`
- `value`

The main indicators used for modelling were:

- `tests`
- `detections`
- `positivity`

After preprocessing and filtering, the final cleaned Influenza dataset contained **4,584 observations**, where each row represented an aggregated surveillance record for a specific country and reporting week.

---

## Data Preprocessing

The raw surveillance dataset was not immediately ready for machine learning, so several preprocessing steps were applied.

### Main preprocessing steps:

1. Loaded and inspected the raw dataset.
2. Filtered the dataset to retain only primary care sentinel surveillance records.
3. Selected Influenza as the main pathogen for modelling.
4. Filtered for total age group records.
5. Reshaped the dataset by pivoting the `indicator` column into separate variables:
   - `tests`
   - `detections`
   - `positivity`
6. Handled missing values in key variables.
7. Recalculated positivity where possible using:

```text
positivity = (detections / tests) * 100
Created time variables from the yearweek column.
Sorted records by country and week.
Removed rows that could not support lag features or next-week target creation.
Feature Engineering

Feature engineering was one of the most important parts of this project. The aim was to create variables that captured the current surveillance situation as well as recent short-term changes in Influenza activity.

Current-week features
tests
detections
positivity
Time-based features
year
week
week_start_date
Lag features

Lag features were created to capture the previous week’s values within each country.

positivity_lag1
detections_lag1
tests_lag1
Change-based features

Change features were created to capture week-to-week increases or decreases.

positivity_change
detections_change
Rolling average features

Three-week rolling averages were created to smooth short-term fluctuations and capture recent trends.

positivity_roll3
detections_roll3
tests_roll3

These features helped the models understand not only the current level of Influenza activity but also whether the activity was rising, falling, or remaining stable.

Target Variable

The target variable used in this project was:

outbreak_next_week

This was a binary classification target.

First, a current outbreak flag was created using the positivity rate:

outbreak_current = 1 if positivity >= 10
outbreak_current = 0 if positivity < 10

Then, this current outbreak flag was shifted forward by one week within each country to create the final prediction target:

outbreak_next_week

This means the models were trained to use current and recent surveillance indicators to predict whether an Influenza outbreak would occur in the following week.

Machine Learning Models Used

Five machine learning models were trained and compared:

Logistic Regression
Decision Tree
Random Forest
Support Vector Machine
K-Nearest Neighbours

These models were selected because they represent different classification approaches, ranging from simple interpretable models to more flexible non-linear models.

Model Training and Validation

A chronological train-test split was used instead of a random split. This was important because the project involved time-dependent surveillance data.

Train-test split
First 80% of unique weekly periods: training set
Last 20% of unique weekly periods: testing set

This approach ensured that the models were trained on past data and tested on future unseen data.

Cross-validation

Time-series cross-validation was applied using TimeSeriesSplit with 5 splits. This helped preserve the temporal order of the data during validation.

Hyperparameter tuning

Hyperparameter tuning was applied to improve model performance.

GridSearchCV was used for:
Logistic Regression
K-Nearest Neighbours
RandomizedSearchCV was used for:
Decision Tree
Random Forest
Support Vector Machine

The main tuning metric was F1-score, because outbreak prediction requires a balance between precision and recall.

Evaluation Metrics

The models were evaluated using the following metrics:

Accuracy
Precision
Recall
F1-score
ROC-AUC
Why F1-score was important

In an outbreak prediction setting, both false alarms and missed outbreaks matter. Precision helps measure false alarms, while recall helps measure missed outbreak cases. F1-score balances both, making it a suitable metric for this project.

Model Performance Results
Model	Best CV F1	Accuracy	Precision	Recall	F1-Score	ROC-AUC
Random Forest	0.8249	0.9026	0.9070	0.8561	0.8808	0.9444
K-Nearest Neighbours	0.8036	0.8903	0.8741	0.8634	0.8687	0.9200
Support Vector Machine	0.7917	0.8821	0.8554	0.8659	0.8606	0.9305
Decision Tree	0.8005	0.8697	0.8329	0.8634	0.8479	0.9139
Logistic Regression	0.7770	0.8646	0.8697	0.7976	0.8321	0.9181
Best Performing Model

The best-performing model was Random Forest.

Random Forest achieved the highest overall performance across the main evaluation metrics:

Highest cross-validation F1-score
Highest test F1-score
Highest accuracy
Highest ROC-AUC

The tuned Random Forest model achieved:

Accuracy  : 0.9026
Precision : 0.9070
Recall    : 0.8561
F1-Score  : 0.8808
ROC-AUC   : 0.9444

This shows that Random Forest was able to classify both outbreak and non-outbreak weeks effectively while maintaining a strong balance between precision and recall.

Feature Importance

The Random Forest model was also used to identify the most important predictors of next-week outbreak risk.

The most important predictors were:

Current positivity rate
Week of the year
Three-week rolling positivity average
Recent positivity changes
Lagged positivity values

The results showed that positivity rate was the strongest predictor of next-week outbreak risk. This means that the proportion of positive Influenza tests was more informative than raw detection counts alone.

The importance of the week variable also confirmed the seasonal nature of Influenza activity. This suggests that outbreak risk depends not only on current surveillance levels but also on the timing of the year.

Key Findings

The main findings of this project are:

Public health surveillance data can be used for short-term Influenza outbreak prediction.
Positivity rate is the most important early warning indicator.
Recent positivity trends and rolling averages improve predictive performance.
Seasonal timing plays an important role in Influenza outbreak risk.
Machine learning models can support outbreak early warning when trained and evaluated correctly.
Random Forest provided the best overall performance among the five models tested.
Time-based validation is more suitable than random splitting for surveillance-based outbreak prediction.
Tools and Technologies Used

The project was implemented using Python in Google Colab.

Programming Language
Python
Libraries
Pandas
NumPy
Matplotlib
Scikit-learn
Machine Learning Techniques
Binary classification
Feature engineering
Time-series cross-validation
Hyperparameter tuning
Model comparison
Feature importance analysis
Project Workflow

The overall workflow of the project was:

Load public health surveillance data
Inspect dataset structure
Filter for primary care sentinel Influenza records
Reshape indicator-based data into separate columns
Handle missing values
Create time variables
Perform exploratory data analysis
Engineer lag, change, and rolling features
Define next-week outbreak target
Split data chronologically
Train five machine learning models
Tune models using cross-validation
Evaluate models on a future hold-out test set
Select the best-performing model
Interpret feature importance and results
Conclusion

This project demonstrates that routine public health surveillance data can be used to build an interpretable early-warning framework for Influenza outbreak prediction. By combining surveillance indicators, engineered time-based features, and machine learning models, the study shows that next-week outbreak risk can be predicted with strong performance.

Random Forest emerged as the best overall model, achieving high accuracy, strong F1-score, and the highest ROC-AUC. The most important predictors were positivity rate, recent positivity trends, and seasonal timing.

Overall, the project highlights how data analytics and machine learning can support public health decision-making by turning routine surveillance data into practical early warning insights.

Future Work

Future improvements could include:

Extending the model to other respiratory viruses such as RSV and SARS-CoV-2.
Including additional public health indicators such as hospitalisation or ICU admission data.
Testing advanced forecasting models such as XGBoost, LSTM, or GRU.
Developing a real-time dashboard for outbreak monitoring.
Applying the framework to country-specific outbreak prediction.
Improving interpretability using SHAP or other explainable AI methods.
Author

Rahul Patil
MSc Data Analytics
Dublin Business School
