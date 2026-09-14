# Fraud Detection Pipeline

A machine learning project developed during the DecodeLabs Data Science Internship.

## Project Overview

This project focuses on identifying potentially fraudulent e-commerce transactions using customer order and payment-related information.

The dataset contains e-commerce transaction records. A fraud indicator was created using selected transaction patterns, including unusually high order values, large quantities, and cash-on-delivery payments.

## Project Highlights

* Prepared and explored an e-commerce dataset
* Created a fraud classification target
* Applied data preprocessing techniques
* Used SMOTE to address class imbalance
* Trained Logistic Regression and Random Forest models
* Compared model performance using classification metrics
* Identified the most influential features for fraud prediction

## Technologies Used

* Python
* Jupyter Notebook
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Imbalanced-learn
* OpenPyXL

## Models

The following classification models were implemented:

1. Logistic Regression
2. Random Forest Classifier

The Random Forest model provided the strongest overall performance in this project.

## Results Summary

| Model               | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
| ------------------- | -------: | --------: | -----: | -------: | ------: |
| Logistic Regression |   99.17% |    91.67% | 91.67% |   91.67% |  99.71% |
| Random Forest       |   99.58% |      100% | 91.67% |   95.65% |    100% |

## Important Features

The features that contributed most to the Random Forest predictions included:

* Total Price
* Unit Price
* Quantity
* Items in Cart
* Referral Source
* Product
* Order Status
* Payment Method

## Repository Contents

* `Project2.ipynb` — Complete project notebook
* `Dataset.csv` — Dataset used for analysis and modelling
* `Dataset for Data Analytics (1).xlsx` — Original dataset
* `Project2_Fraud_Detection_Report.docx` — Detailed project report
* `README.md` — Project overview and documentation

## How to Run

1. Download or clone this repository.
2. Open `Project2.ipynb` in Jupyter Notebook or VS Code.
3. Install the required libraries if needed:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn openpyxl
```

4. Make sure the dataset is placed in the same folder as the notebook.
5. Run the notebook cells in sequence.

