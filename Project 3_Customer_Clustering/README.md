# Project 3 — Customer Clustering

## Project Overview

This project focuses on customer segmentation using unsupervised machine learning. The goal is to group customers based on their purchasing behavior and identify meaningful customer segments.

The project uses customer transaction data and the K-Means clustering algorithm to create customer groups.

## Dataset

The dataset contains **1,200 order records** with **14 columns**, including:

* Order ID
* Date
* Customer ID
* Product
* Quantity
* Unit Price
* Shipping Address
* Payment Method
* Order Status
* Tracking Number
* Items in Cart
* Coupon Code
* Referral Source
* Total Price

There are **1,189 unique customers** in the dataset.

## Data Preprocessing

The following preprocessing steps were performed:

1. Loaded the Excel dataset using Pandas.
2. Checked the dataset structure and data types.
3. Identified missing values.
4. Replaced missing `CouponCode` values with `No Coupon`.
5. Checked for duplicate records.
6. Aggregated order-level data into customer-level data.
7. Created customer behavior features.
8. Standardized the numerical features using `StandardScaler`.

No exact duplicate rows were found in the dataset.

## Customer Features

Customer-level features used for clustering were:

* `TotalOrders`
* `TotalQuantity`
* `TotalSpending`
* `AvgOrderValue`
* `AvgItemsInCart`

These features represent customer purchasing frequency, quantity, spending, order value, and cart behavior.

## Clustering Method

The **K-Means clustering algorithm** was used for customer segmentation.

The Elbow Method and Silhouette Score were used to evaluate different numbers of clusters.

The calculated Silhouette Scores were:

| Number of Clusters | Silhouette Score |
| ------------------ | ---------------: |
| 2                  |           0.4116 |
| 3                  |           0.4236 |

Based on the clustering analysis and interpretability of the resulting groups, **3 clusters** were selected for the final model.

## Cluster Results

The final K-Means model produced three customer segments:

| Cluster   | Customers | Percentage |
| --------- | --------: | ---------: |
| Cluster 0 |       744 |     62.57% |
| Cluster 1 |       434 |     36.50% |
| Cluster 2 |        11 |      0.93% |

### Cluster 0

This group contains customers with relatively lower total quantity and spending.

* Average quantity: 2.22
* Average spending: 558.32
* Average items in cart: 4.59

### Cluster 1

This group contains customers with higher purchasing activity and spending.

* Average quantity: 4.21
* Average spending: 1,912.07
* Average order value: 1,912.07
* Average items in cart: 7.05

### Cluster 2

This is a small group of repeat customers.

* Average orders: 2.00
* Average quantity: 5.45
* Average spending: 1,775.98
* Average order value: 887.99
* Average items in cart: 5.05

## Visualization

Principal Component Analysis (PCA) was used to reduce the five-dimensional customer feature space to two dimensions for visualization.

The resulting PCA plot shows the distribution of customers across the three clusters.

## Project Files

* `Project3.ipynb` — Complete Jupyter Notebook
* `Customer_Clusters.csv` — Final customer clustering results
* `README.md` — Project overview and methodology
* `Report.md` — Detailed project report
* `requirements.txt` — Required Python libraries

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Jupyter Notebook

## Conclusion

The project demonstrates how K-Means clustering can be used to segment customers according to their purchasing behavior. The resulting clusters provide different patterns of customer quantity, spending, order value, and cart activity.
