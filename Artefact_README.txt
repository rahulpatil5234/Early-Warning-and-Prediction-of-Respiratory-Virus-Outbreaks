Artefact README

Student Name: Rahul Patil
Student Number: 20057979
Programme: Master’s in Data Analytics
Institution: Dublin Business School

Project Title:
Early Warning and Prediction of Respiratory Virus Outbreaks Using Public Health Surveillance Data

Artefact Title:
Machine Learning Model for Next-Week Influenza Outbreak Prediction

Submitted Files:
1. Rahul_Patil_20057979_Artefact_Machine_Learning_Model.ipynb
2. Rahul_Patil_20057979_Surveillance_Dataset.csv
3. Rahul_Patil_20057979_Artefact_README.txt

Artefact Description:
This artefact is a Google Colab / Jupyter Notebook implementation of a machine learning framework for predicting next-week Influenza outbreak risk using public health surveillance data. The notebook includes the full workflow from data loading and pre-processing to feature engineering, model training, hyperparameter tuning, cross-validation, model evaluation, and final interpretation.

Dataset Used:
The dataset used in this artefact is sentinelTestsDetectionsPositivity.csv. The analysis focuses on primary care sentinel surveillance records for Influenza. The main indicators used are tests, detections, and positivity.

Main Steps Included in the Notebook:
1. Import required Python libraries and load the dataset.
2. Inspect the dataset structure and missing values.
3. Filter the dataset for primary care sentinel Influenza records.
4. Reshape the indicator column into separate variables: tests, detections, and positivity.
5. Handle missing values and prepare a clean dataset.
6. Create time-based variables from the yearweek column.
7. Create lag features, change-based features, and 3-week rolling average features.
8. Define the next-week outbreak prediction target.
9. Create a chronological train-test split based on unique weekly periods.
10. Apply time-series cross-validation and hyperparameter tuning.
11. Train and evaluate five machine learning models:
    - Logistic Regression
    - Decision Tree
    - Random Forest
    - Support Vector Machine
    - K-Nearest Neighbours
12. Compare model performance using Accuracy, Precision, Recall, F1-score, and ROC-AUC.
13. Interpret the best model using feature importance.
14. Present visual outputs including feature importance, confusion matrix, and ROC curves.

Main Output:
The tuned Random Forest model was identified as the best-performing model overall. It achieved the strongest balance of Accuracy, Precision, Recall, F1-score, and ROC-AUC. Feature importance analysis showed that positivity, week, and recent rolling positivity trends were the most influential predictors of next-week Influenza outbreak risk.

Software and Libraries Required:
The notebook was developed and executed in Google Colab using Python.

Main Python libraries:
- pandas
- numpy
- matplotlib
- scikit-learn

How to Run the Artefact:
1. Open the notebook file in Google Colab or Jupyter Notebook.
2. Upload the dataset file named sentinelTestsDetectionsPositivity.csv, or ensure the dataset path matches the notebook code.
3. Run each notebook cell in order from Step 1 to Step 22.
4. Review the model comparison table and visual outputs at the end of the notebook.

Important Note:
The artefact is designed as an applied machine learning prototype for public health surveillance support. It is intended to support early-warning analysis and should not be interpreted as a replacement for professional public health decision-making.

Submitted by:
Rahul Patil
Student Number: 20057979