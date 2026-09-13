Fraud Detection Pipeline — Data Science Project 2
Overview

This project implements a machine learning-based fraud detection pipeline for e-commerce transaction data.

The main purpose of the project is to identify potentially fraudulent transactions using supervised machine learning techniques while handling an imbalanced classification problem.

Two classification algorithms were implemented and compared:

Logistic Regression
Random Forest

SMOTE (Synthetic Minority Over-sampling Technique) was used to handle class imbalance.

Project Objectives

The objectives of this project are to:

Load and explore an e-commerce transaction dataset.
Clean and preprocess numerical and categorical data.
Generate a fraud-related target variable.
Handle class imbalance using SMOTE.
Build machine learning classification pipelines.
Train Logistic Regression and Random Forest models.
Evaluate models using Precision, Recall, F1-Score, and ROC-AUC.
Compare the performance of both models.
Identify the better-performing fraud detection model.
Dataset

The dataset contains 1,200 e-commerce transaction records with numerical, categorical, and date-related attributes.

Important transaction attributes include:

Quantity
TotalPrice
PaymentMethod
Transaction Date

The original dataset did not contain a verified fraud-label column. Therefore, a synthetic IsFraud target variable was generated using transaction-based rules.

A transaction was classified as fraud when one or more of the following conditions were satisfied:

TotalPrice was above the 95th percentile.
Quantity was above the 95th percentile.
PaymentMethod was Cash on Delivery.

After target generation:

Non-Fraud: 1,140
Fraud: 60

This created a highly imbalanced classification problem.

Methodology

The project followed these major steps:

Dataset loading
Data exploration
Data cleaning
Feature preprocessing
Date feature extraction
Synthetic fraud-label generation
Train-test splitting
Handling class imbalance with SMOTE
Model training
Model evaluation
Model comparison
Feature importance analysis
Data Preprocessing

Numerical features were processed using:

Missing-value imputation
Standard scaling

Categorical features were processed using:

Missing-value imputation
One-hot encoding

The dataset was divided using an 80:20 stratified train-test split.

SMOTE was applied to the training data to increase representation of the minority fraud class.

Machine Learning Models
1. Logistic Regression

Logistic Regression was used as a baseline classification model.

It estimates the probability that a transaction belongs to the fraud or non-fraud class.

2. Random Forest

Random Forest is an ensemble learning algorithm based on multiple decision trees.

It was selected because it can:

Capture non-linear relationships
Handle different feature types
Provide feature-importance information
Perform well on classification problems
Evaluation Metrics

The models were evaluated using:

Precision

Measures how many transactions predicted as fraud were actually fraud.

Recall

Measures how many actual fraudulent transactions were successfully detected.

F1-Score

Provides a balance between Precision and Recall.

ROC-AUC

Measures how effectively the model distinguishes between fraud and non-fraud transactions.

Accuracy was also calculated for reference, but fraud detection performance was primarily evaluated using Precision, Recall, F1-Score, and ROC-AUC.

Results
Model	Accuracy	Precision	Recall	F1-Score	ROC-AUC
Logistic Regression	99.17%	91.67%	91.67%	91.67%	99.71%
Random Forest	99.58%	100.00%	91.67%	95.65%	100.00%
Best Model

Random Forest performed better overall.

It achieved:

Accuracy: 99.58%
Precision: 100.00%
Recall: 91.67%
F1-Score: 95.65%
ROC-AUC: 100.00%

Therefore, Random Forest was selected as the better-performing model for this project.

Technologies Used
Python
Jupyter Notebook
Pandas
NumPy
Scikit-learn
Imbalanced-learn
Matplotlib
Seaborn
Project Structure
Project-2-Fraud-Detection/
│
├── Dataset.csv
├── Project2.ipynb
├── README.md
└── REPORT.md
Limitations

The most important limitation is that the fraud labels were synthetically generated because the original dataset did not contain verified fraud outcomes.

The labels were generated using TotalPrice, Quantity, and PaymentMethod, which are also features used by the models.

Therefore, the very high model performance should not be interpreted as real-world fraud detection performance.

A real fraud detection system would require:

Verified historical fraud labels
Real transaction data
Unseen production transactions
Continuous model monitoring
More robust validation
Conclusion

This project demonstrates a complete supervised machine learning workflow for fraud detection.

The pipeline included data preprocessing, feature engineering, synthetic target generation, SMOTE-based class balancing, model training, evaluation, and comparison.

Both Logistic Regression and Random Forest achieved strong results, while Random Forest performed better overall with an F1-Score of 95.65% and ROC-AUC of 1.00.

This project provided practical experience with classification algorithms, imbalanced datasets, Scikit-learn pipelines, model evaluation, and machine learning-based fraud detection.
