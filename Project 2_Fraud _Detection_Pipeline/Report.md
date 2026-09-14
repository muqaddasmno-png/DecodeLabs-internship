# Fraud Detection Pipeline

## 1. Project Overview

This project focuses on developing a machine learning pipeline for detecting potentially fraudulent e-commerce transactions.

The project compares two machine learning classification models:

* Logistic Regression
* Random Forest

The main objectives are to preprocess the dataset, handle class imbalance, train classification models, evaluate their performance, and identify the most important features contributing to the model's predictions.

## 2. Dataset Description

The dataset contains 1,200 e-commerce order records and includes information such as:

* Order date
* Product
* Category
* Quantity
* Unit price
* Total price
* Payment method
* Order status
* Referral source
* Coupon code
* Items in cart

A fraud indicator was created using selected transaction-related conditions, including unusually high transaction values, high quantities, and cash-on-delivery payments.

**Note:** The fraud label used in this project is a synthetic label created for educational and demonstration purposes. It does not represent verified real-world fraud cases.

## 3. Tools and Technologies

* Python
* Jupyter Notebook
* Pandas
* NumPy
* Matplotlib
* Scikit-learn
* Imbalanced-learn
* SMOTE

## 4. Project Workflow

The project was completed through the following steps:

1. Loaded the e-commerce dataset.
2. Explored the dataset structure and columns.
3. Created a synthetic fraud indicator.
4. Removed unnecessary identifier columns.
5. Extracted date-based features.
6. Divided the dataset into training and testing sets.
7. Applied numerical and categorical preprocessing.
8. Handled class imbalance using SMOTE.
9. Trained Logistic Regression and Random Forest models.
10. Evaluated both models using classification metrics.
11. Generated confusion matrices.
12. Compared ROC curves and ROC-AUC scores.
13. Extracted feature importance from the Random Forest model.
14. Prepared the final project report.

## 5. Data Preprocessing

The following preprocessing techniques were applied:

* Unnecessary identifier columns were removed.
* Date features were extracted from the order date.
* Missing numerical values were handled through imputation.
* Numerical features were standardized using `StandardScaler`.
* Categorical features were encoded using `OneHotEncoder`.
* The dataset was divided into training and testing sets using a stratified split.
* SMOTE was applied to the training data to handle class imbalance.

## 6. Models Used

### 6.1 Logistic Regression

Logistic Regression was used as a baseline classification model. It is commonly used for binary classification and provides a simple model for comparison.

### 6.2 Random Forest

Random Forest was used as the main classification model. It combines multiple decision trees and can identify nonlinear relationships between features.

## 7. Model Evaluation Metrics

The models were evaluated using the following metrics:

* **Accuracy:** Measures the overall proportion of correct predictions.
* **Precision:** Measures how many predicted fraud cases were actually fraud cases.
* **Recall:** Measures how many actual fraud cases were correctly detected.
* **F1-Score:** Represents the balance between precision and recall.
* **ROC-AUC:** Measures the model's ability to distinguish between the two classes.

## 8. Model Performance Comparison

| Model               | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
| ------------------- | -------: | --------: | -----: | -------: | ------: |
| Logistic Regression |   99.17% |    91.67% | 91.67% |   91.67% |   0.997 |
| Random Forest       |   99.58% |   100.00% | 91.67% |   95.65% |   1.000 |

## 9. Confusion Matrix Analysis

The Random Forest confusion matrix produced the following results:

| Actual / Predicted | Not Fraud | Fraud |
| ------------------ | --------: | ----: |
| Not Fraud          |       228 |     0 |
| Fraud              |         1 |    11 |

### Interpretation

* **228** non-fraud transactions were correctly classified.
* **11** fraud transactions were correctly classified.
* **0** non-fraud transactions were incorrectly classified as fraud.
* **1** fraud transaction was incorrectly classified as non-fraud.

The confusion matrix shows that the Random Forest model made very few incorrect predictions on the test dataset.

## 10. ROC Curve Analysis

The ROC curve compares the true-positive rate and false-positive rate at different classification thresholds.

The ROC-AUC scores were:

* **Logistic Regression:** 0.997
* **Random Forest:** 1.000

The Random Forest model achieved a slightly higher ROC-AUC score than Logistic Regression, showing excellent classification performance on the test dataset.

## 11. Feature Importance Analysis

Feature importance was extracted from the Random Forest model to identify the features that contributed most to its predictions.

| Rank | Feature                 | Importance |
| ---: | ----------------------- | ---------: |
|    1 | TotalPrice              |   0.441803 |
|    2 | UnitPrice               |   0.233682 |
|    3 | Quantity                |   0.162188 |
|    4 | ItemsInCart             |   0.057882 |
|    5 | ReferralSource_Google   |   0.011694 |
|    6 | Product_Laptop          |   0.010508 |
|    7 | ReferralSource_Email    |   0.007775 |
|    8 | Product_Desk            |   0.007351 |
|    9 | ReferralSource_Facebook |   0.006995 |
|   10 | OrderStatus_Returned    |   0.006441 |
|   11 | OrderStatus_Shipped     |   0.004877 |
|   12 | CouponCode_WINTER15     |   0.004327 |
|   13 | PaymentMethod_Online    |   0.003928 |
|   14 | Product_Printer         |   0.003657 |
|   15 | PaymentMethod_Cash      |   0.003409 |

### Interpretation

The most influential feature was `TotalPrice`, followed by `UnitPrice`, `Quantity`, and `ItemsInCart`. This indicates that transaction value and quantity-related features had the greatest influence on the Random Forest model's predictions.

## 12. Results and Discussion

Both models performed well on the test dataset. However, Random Forest performed slightly better than Logistic Regression in terms of accuracy, F1-score, and ROC-AUC.

The Random Forest model achieved:

* **99.58% Accuracy**
* **100.00% Precision**
* **91.67% Recall**
* **95.65% F1-Score**
* **1.000 ROC-AUC**

The model correctly classified most non-fraud and fraud transactions. The feature importance analysis showed that transaction-related numerical features, particularly total price, unit price, and quantity, had the greatest influence on the predictions.

## 13. Limitations

* The fraud labels were synthetically created for educational purposes.
* The dataset does not contain verified real-world fraud records.
* The high performance may be influenced by the rules used to create the fraud label.
* The model should be tested on real and independent datasets before being used in a practical fraud detection system.

## 14. Conclusion

This project successfully developed a machine learning pipeline for detecting potentially fraudulent e-commerce transactions.

Logistic Regression and Random Forest were trained and evaluated using several classification metrics. Random Forest achieved the best overall performance, with an accuracy of 99.58%, an F1-score of 95.65%, and an ROC-AUC of 1.000.

The project demonstrated the complete machine learning workflow, including data preprocessing, class imbalance handling, model training, evaluation, confusion matrix analysis, ROC curve comparison, and feature importance analysis.

## 15. Project Files

* `Project2.ipynb` — Complete Jupyter Notebook implementation
* `Dataset.csv` — Dataset in CSV format
* `Dataset for Data Analytics (1).xlsx` — Original Excel dataset
* `Project2_Fraud_Detection_Report.docx` — Detailed Word report
* `Project2_Report.md` — Markdown version of the project report

## Author

**Muqaddas Mukhtar**

BS Bioinformatics Student
