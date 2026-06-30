# Early Warning and Prediction of Respiratory Virus Outbreaks Using Public Health Surveillance Data

## Overview

This project focuses on the early warning and short-term prediction of respiratory virus outbreaks using public health surveillance data. The main aim of the project is to analyse whether routine public health surveillance indicators can be used to detect early signs of rising Influenza activity and predict the risk of an outbreak in the following week.

The project uses primary care sentinel surveillance data and applies a complete data analytics and machine learning workflow, including data cleaning, preprocessing, exploratory data analysis, feature engineering, model training, hyperparameter tuning, time-series validation, model comparison, and feature importance interpretation.

Although the original dataset contained multiple respiratory pathogens, including Influenza, RSV, and SARS-CoV-2, Influenza was selected as the main modelling focus because it showed the strongest and most reliable outbreak-related patterns within the available surveillance data.

The final outcome of this project is an interpretable machine learning framework that can support short-term outbreak warning using indicators such as tests, detections, positivity rates, lag features, rolling averages, recent changes, and seasonal timing.

---

## Project Title

Early Warning and Prediction of Respiratory Virus Outbreaks Using Public Health Surveillance Data

---

## Author

Rahul Patil  
MSc Data Analytics  
Dublin Business School  

---

## Problem Statement

Respiratory virus outbreaks can increase rapidly and place pressure on healthcare systems. Public health surveillance systems collect valuable weekly data, but this information is often used mainly to describe current or past activity rather than to predict future outbreak risk.

One major challenge is that outbreaks may only be recognised after they are already clearly visible in routine surveillance reports. This can reduce the time available for preparedness, planning, public communication, and response.

Another challenge is that no single surveillance indicator is perfect. For example, the number of positive detections may increase simply because more tests were carried out. Therefore, this project uses multiple indicators together, including tests, detections, positivity rate, lag values, rolling averages, week-to-week changes, and seasonal timing.

The key problem addressed in this project is:

Can routine public health surveillance data be used to predict next-week Influenza outbreak risk in an interpretable and practical way?

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
- Identify temporal and seasonal patterns linked to rising Influenza activity.
- Engineer time-based, lag-based, change-based, and rolling average features.
- Define a next-week outbreak target variable for classification.
- Train and compare five machine learning models.
- Apply time-series cross-validation and hyperparameter tuning.
- Evaluate models using accuracy, precision, recall, F1-score, and ROC-AUC.
- Select the best-performing model.
- Interpret the most important predictors using feature importance analysis.

---

## Dataset Description

The project uses a public health sentinel surveillance dataset containing aggregated weekly respiratory virus surveillance records.

The original dataset included multiple respiratory pathogens, but the final modelling dataset was filtered to focus on Influenza because it provided clearer outbreak-related patterns and stronger predictive results.

### Original Dataset Columns

The original dataset contained the following key columns:

- survtype
- countryname
- yearweek
- pathogen
- pathogentype
- pathogensubtype
- indicator
- age
- value

### Main Indicators Used

The main surveillance indicators used in this project were:

- tests
- detections
- positivity

### Final Cleaned Dataset

After filtering and preprocessing, the final cleaned Influenza dataset contained 4,584 observations. Each row represented an aggregated surveillance record for a specific country and reporting week.

---

## Data Preprocessing

The raw surveillance data was not immediately suitable for machine learning. Several preprocessing steps were applied to convert the data into a clean and modelling-ready format.

### Preprocessing Steps

1. Loaded and inspected the raw dataset.
2. Checked the structure, columns, unique values, and missing values.
3. Filtered the dataset to retain only primary care sentinel surveillance records.
4. Selected Influenza as the main pathogen for modelling.
5. Filtered records for the total age group.
6. Reshaped the dataset by pivoting the indicator column into separate variables.
7. Converted tests, detections, and positivity into separate columns.
8. Handled missing values in key variables.
9. Recalculated positivity where possible using detections and tests.
10. Created time variables from the yearweek column.
11. Sorted the dataset by country and reporting week.
12. Removed rows that could not support lag feature creation.
13. Removed rows that could not support next-week target creation.

### Positivity Formula

    positivity = (detections / tests) * 100

This formula was used where positivity values were missing but tests and detections were available.

---

## Exploratory Data Analysis

Exploratory Data Analysis was performed to understand the behaviour of Influenza activity over time and across countries.

The analysis focused on:

- Overall structure of the cleaned dataset
- Summary statistics of tests, detections, and positivity
- Weekly trends in Influenza positivity
- Weekly trends in tests and detections
- Country-level comparison of Influenza activity
- Distribution of key variables
- Time-based and seasonal patterns
- Relationship between current indicators and next-week outbreak risk

### Key EDA Observations

- Influenza activity was not constant across the reporting period.
- Some weeks showed low positivity, while other periods showed clear increases.
- Positivity rate was more informative than raw detection counts alone.
- Detections became more meaningful when interpreted together with positivity.
- Influenza activity showed seasonal behaviour.
- Country-level differences were visible in the surveillance data.
- Recent trends and rolling averages were useful for identifying outbreak-related patterns.

---

## Feature Engineering

Feature engineering was one of the most important parts of this project. The goal was to create variables that captured both the current surveillance situation and recent short-term movement in Influenza activity.

### Current-Week Features

These features captured the current weekly surveillance status:

- tests
- detections
- positivity

### Time-Based Features

These features captured seasonal and calendar-based information:

- year
- week
- week_start_date

The week variable was important because Influenza activity often follows seasonal patterns.

### Lag Features

Lag features were created to capture the previous week’s values within each country:

- positivity_lag1
- detections_lag1
- tests_lag1

These features helped the models understand how recent past activity influenced next-week outbreak risk.

### Change-Based Features

Change features were created to capture week-to-week increases or decreases:

- positivity_change
- detections_change

These features were useful because a sudden rise in positivity or detections may act as an early signal of increasing outbreak risk.

### Rolling Average Features

Three-week rolling averages were created to smooth short-term fluctuations and capture recent trends:

- positivity_roll3
- detections_roll3
- tests_roll3

Rolling averages helped the models understand whether Influenza activity was rising, falling, or remaining stable over a short period.

---

## Target Variable

The target variable used in this project was:

    outbreak_next_week

This was a binary classification target.

First, a current outbreak flag was created using positivity rate:

    outbreak_current = 1 if positivity >= 10
    outbreak_current = 0 if positivity < 10

Then, the current outbreak flag was shifted forward by one week within each country to create the final target variable:

    outbreak_next_week

This means the models were trained to use current and recent surveillance indicators to predict whether an Influenza outbreak would occur in the following week.

---

## Machine Learning Models Used

Five machine learning models were trained and compared:

1. Logistic Regression
2. Decision Tree
3. Random Forest
4. Support Vector Machine
5. K-Nearest Neighbours

These models were selected because they represent different classification approaches, from simple baseline models to more flexible non-linear models.

### Logistic Regression

Logistic Regression was used as a baseline binary classification model. It is simple, interpretable, and commonly used in health-related classification problems.

### Decision Tree

Decision Tree was used because it can capture non-linear relationships and create rule-based decision splits. It is also easier to interpret compared to many complex models.

### Random Forest

Random Forest was used because it combines multiple decision trees and usually performs well on structured tabular data. It can capture complex relationships while reducing the instability of a single decision tree.

### Support Vector Machine

Support Vector Machine was used because it can model complex decision boundaries. Since SVM is sensitive to feature scale, standardisation was applied using a pipeline.

### K-Nearest Neighbours

K-Nearest Neighbours was used as a distance-based classification model. Since KNN depends on distance between observations, standardisation was also applied using a pipeline.

---

## Model Training and Validation

A chronological train-test split was used instead of a random split. This was important because the dataset is time-dependent and the aim is to predict future outbreak risk from past surveillance data.

### Train-Test Split

- First 80% of unique weekly periods: Training set
- Last 20% of unique weekly periods: Testing set

This approach ensured that the models were trained on earlier weeks and tested on later unseen weeks.

### Time-Series Cross-Validation

Time-series cross-validation was applied using TimeSeriesSplit with 5 splits.

This preserved the temporal order of the data and avoided future data leakage during validation.

### Hyperparameter Tuning

Hyperparameter tuning was applied to improve model robustness and performance.

GridSearchCV was used for:

- Logistic Regression
- K-Nearest Neighbours

RandomizedSearchCV was used for:

- Decision Tree
- Random Forest
- Support Vector Machine

The main tuning metric was F1-score because outbreak prediction requires a balance between precision and recall.

---

## Evaluation Metrics

The models were evaluated using the following metrics:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

### Accuracy

Accuracy measures the overall proportion of correct predictions.

### Precision

Precision measures how many predicted outbreak weeks were actually true outbreak weeks. This is useful for understanding false alarms.

### Recall

Recall measures how many true outbreak weeks were successfully identified. This is important in public health because missed outbreak weeks can reduce the usefulness of an early-warning system.

### F1-Score

F1-score combines precision and recall into one balanced metric. It was especially important in this project because both false alarms and missed outbreaks matter.

### ROC-AUC

ROC-AUC measures how well the model separates outbreak and non-outbreak cases across different thresholds.

---

## Model Performance Results

| Model | Best CV F1 | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Random Forest | 0.8249 | 0.9026 | 0.9070 | 0.8561 | 0.8808 | 0.9444 |
| K-Nearest Neighbours | 0.8036 | 0.8903 | 0.8741 | 0.8634 | 0.8687 | 0.9200 |
| Support Vector Machine | 0.7917 | 0.8821 | 0.8554 | 0.8659 | 0.8606 | 0.9305 |
| Decision Tree | 0.8005 | 0.8697 | 0.8329 | 0.8634 | 0.8479 | 0.9139 |
| Logistic Regression | 0.7770 | 0.8646 | 0.8697 | 0.7976 | 0.8321 | 0.9181 |

---

## Best Performing Model

The best-performing model was Random Forest.

Random Forest achieved the strongest overall performance across the main evaluation metrics:

- Highest cross-validation F1-score
- Highest test F1-score
- Highest accuracy
- Highest ROC-AUC

### Random Forest Final Results

| Metric | Score |
|---|---:|
| Accuracy | 0.9026 |
| Precision | 0.9070 |
| Recall | 0.8561 |
| F1-Score | 0.8808 |
| ROC-AUC | 0.9444 |

The tuned Random Forest model correctly classified most outbreak and non-outbreak weeks while keeping false alarms and missed outbreaks relatively low. This made it the strongest model for the early-warning framework.

---

## Feature Importance

After Random Forest was selected as the best-performing model, feature importance was analysed to understand which variables contributed most to next-week outbreak prediction.

The most important predictors were:

- Current positivity rate
- Week of the year
- Three-week rolling positivity average
- Recent positivity changes
- Lagged positivity values

The results showed that positivity rate was the strongest predictor of next-week outbreak risk. This means that the proportion of positive Influenza tests was more informative than raw detection counts alone.

The importance of the week variable confirmed that seasonal timing plays an important role in Influenza activity. The rolling positivity feature also showed that recent short-term trends are useful for predicting whether an outbreak may occur in the following week.

---

## Key Findings

The main findings of this project are:

- Public health surveillance data can be used for short-term Influenza outbreak prediction.
- Positivity rate is the strongest early warning indicator.
- Recent positivity trends and rolling averages improve predictive performance.
- Seasonal timing is important for predicting Influenza outbreak risk.
- Machine learning models can support outbreak early warning when trained and validated correctly.
- Random Forest provided the best overall performance among the five models tested.
- Time-based validation is more suitable than random splitting for this type of surveillance problem.
- Interpretable model outputs are important for public health decision-making.

---

## Tools and Technologies Used

### Programming Language

- Python

### Development Environment

- Google Colab

### Python Libraries

- Pandas
- NumPy
- Matplotlib
- Scikit-learn

### Machine Learning Techniques

- Binary classification
- Exploratory data analysis
- Feature engineering
- Lag feature creation
- Rolling average feature creation
- Time-series cross-validation
- Hyperparameter tuning
- Model comparison
- Feature importance analysis

---

## Project Workflow

The overall workflow of the project was:

1. Load public health surveillance data.
2. Inspect dataset structure and key columns.
3. Filter for primary care sentinel Influenza records.
4. Filter for total age group records.
5. Reshape indicator-based data into separate columns.
6. Handle missing values.
7. Recalculate positivity where possible.
8. Create time variables from yearweek.
9. Perform exploratory data analysis.
10. Engineer lag, change, and rolling average features.
11. Define the current outbreak flag.
12. Create the next-week outbreak target.
13. Split data chronologically into training and testing sets.
14. Apply time-series cross-validation.
15. Tune five machine learning models.
16. Evaluate models on a future hold-out test set.
17. Compare model performance.
18. Select Random Forest as the best-performing model.
19. Interpret feature importance.
20. Summarise findings and future improvements.

---

## Repository Structure

The repository may include the following files:

| File | Description |
|---|---|
| README.md | Project documentation |
| Project_Report.pdf | Full dissertation/project report |
| sentinelTestsDetectionsPositivity.csv | Original surveillance dataset |
| cleaned_influenza_data.csv | Cleaned and preprocessed dataset |
| model_training.ipynb | Python notebook for preprocessing, modelling, and evaluation |
| requirements.txt | Required Python libraries |
| images/ | Folder for charts, confusion matrix, ROC curve, and feature importance plots |

---

## Visual Outputs

The project includes the following visual outputs:

- Research methodology workflow
- Data cleaning and reshaping workflow
- Feature engineering and target creation summary
- Weekly Influenza positivity trend
- Weekly tests and detections trend
- Model comparison table
- Random Forest feature importance chart
- Confusion matrix
- ROC curve comparison of all tuned models

You can add screenshots or plots in the README using the format below:

    ![Model Comparison](images/model_comparison.png)

    ![Feature Importance](images/feature_importance.png)

    ![Confusion Matrix](images/confusion_matrix.png)

    ![ROC Curve](images/roc_curve.png)

---

## Conclusion

This project demonstrates that routine public health surveillance data can be used to build an interpretable early-warning framework for Influenza outbreak prediction. By combining surveillance indicators, engineered time-based features, and machine learning models, the study shows that next-week outbreak risk can be predicted with strong performance.

Random Forest emerged as the best-performing model, achieving high accuracy, strong F1-score, and the highest ROC-AUC among the five models tested. The most important predictors were positivity rate, recent positivity trends, and seasonal timing.

Overall, the project highlights how data analytics and machine learning can support public health decision-making by turning routine surveillance data into practical early-warning insights.

---

## Limitations

The project has some limitations:

- The model depends on the quality and completeness of the surveillance dataset.
- Testing behaviour may influence indicators such as detections and positivity.
- The outbreak threshold was based on positivity and may need adjustment in real-world public health settings.
- The framework was mainly focused on Influenza and may not transfer equally well to other respiratory viruses.
- The model should be used as a decision-support tool, not as a replacement for public health judgement.

---

## Future Work

Future improvements could include:

- Extending the model to other respiratory viruses such as RSV and SARS-CoV-2.
- Adding hospitalisation, ICU admission, or mortality data.
- Including weather, mobility, or vaccination data.
- Testing advanced models such as XGBoost, LightGBM, LSTM, or GRU.
- Building a real-time dashboard for outbreak monitoring.
- Applying the framework to country-specific outbreak prediction.
- Using SHAP or other explainable AI techniques for deeper interpretation.
- Deploying the model as a public health decision-support prototype.

---

## Skills Demonstrated

This project demonstrates the following skills:

- Data cleaning
- Data preprocessing
- Exploratory data analysis
- Feature engineering
- Time-series-aware modelling
- Machine learning classification
- Hyperparameter tuning
- Model evaluation
- Model comparison
- Feature importance interpretation
- Public health data analytics
- Research-based problem solving
- Technical documentation

---

## Final Summary

This project presents a complete machine learning workflow for predicting next-week Influenza outbreak risk using public health surveillance data. The study shows that official surveillance indicators such as positivity rate, tests, detections, lag features, rolling averages, and seasonal timing can be transformed into meaningful predictive features.

Among the five models tested, Random Forest achieved the best overall results and was selected as the final model. The project provides a practical example of how machine learning can support early warning, outbreak monitoring, and public health decision-making.
