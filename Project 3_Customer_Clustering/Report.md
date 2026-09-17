# Customer Clustering — Project Report

## 1. Introduction

Customer segmentation is an important data analysis technique used to understand different types of customers based on their purchasing behavior. Instead of treating all customers in the same way, clustering can group customers with similar characteristics.

In this project, K-Means clustering was applied to an e-commerce transaction dataset to identify customer segments based on their order frequency, quantity, spending, order value, and cart activity.

---

## 2. Objective

The main objective of this project was to:

* Analyze customer purchasing behavior.
* Convert order-level data into customer-level information.
* Create meaningful customer behavior features.
* Apply K-Means clustering.
* Determine a suitable number of customer clusters.
* Analyze the characteristics of each customer segment.
* Visualize the resulting clusters using PCA.

---

## 3. Dataset Description

The dataset contains **1,200 order records** and **14 columns**.

The main columns include:

* OrderID
* Date
* CustomerID
* Product
* Quantity
* UnitPrice
* ShippingAddress
* PaymentMethod
* OrderStatus
* TrackingNumber
* ItemsInCart
* CouponCode
* ReferralSource
* TotalPrice

The dataset contains **1,189 unique customers**, meaning that a small number of customers placed more than one order.

---

## 4. Data Preprocessing

### 4.1 Loading the Dataset

The Excel dataset was loaded using Pandas.

```python
import pandas as pd

df = pd.read_excel("Dataset for Data Analytics (1).xlsx")
```

The dataset was checked for its dimensions, columns, data types, missing values, and duplicate records.

### 4.2 Handling Missing Values

The `CouponCode` column contained 309 missing values.

These missing values were replaced with `No Coupon`.

```python
df['CouponCode'] = df['CouponCode'].fillna('No Coupon')
```

After this step, there were no missing values remaining in the dataset.

### 4.3 Duplicate Check

The dataset was checked for exact duplicate rows.

The result was:

```text
0 duplicate rows
```

Therefore, no exact duplicate records were removed.

---

## 5. Customer-Level Feature Engineering

The original dataset contained individual order records. For customer segmentation, the data was aggregated by `CustomerID`.

The following customer-level features were created:

### Total Orders

The total number of orders placed by each customer.

### Total Quantity

The total quantity of products purchased by each customer.

### Total Spending

The total amount spent by each customer.

### Average Order Value

The average spending per order for each customer.

### Average Items in Cart

The average number of items in the cart for each customer.

The resulting customer-level dataset contained **1,189 customers**.

---

## 6. Features Used for Clustering

The following five features were selected for K-Means clustering:

```python
features = [
    'TotalOrders',
    'TotalQuantity',
    'TotalSpending',
    'AvgOrderValue',
    'AvgItemsInCart'
]
```

These features were selected because they represent different aspects of customer purchasing behavior.

---

## 7. Feature Scaling

Since the selected features have different numerical ranges, StandardScaler was used to standardize them.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

Scaling prevents features with larger numerical values, such as total spending, from dominating the clustering process.

---

## 8. Selecting the Number of Clusters

Two methods were used to evaluate the suitable number of clusters:

1. Elbow Method
2. Silhouette Score

### 8.1 Elbow Method

The Elbow Method was used to calculate K-Means inertia for different values of K.

The analysis showed a noticeable change around the lower values of K, with K=2 appearing as an elbow point.

However, the final choice was also evaluated using the Silhouette Score and the interpretability of the resulting customer groups.

### 8.2 Silhouette Score

Silhouette scores were calculated for K=2 and K=3.

| Number of Clusters | Silhouette Score |
| ------------------ | ---------------: |
| 2                  |           0.4116 |
| 3                  |           0.4236 |

The score for K=3 was slightly higher than the score for K=2.

Considering both the clustering evaluation and the interpretability of the resulting groups, **3 clusters were selected** for the final analysis.

---

## 9. K-Means Clustering

The final K-Means model was created using three clusters.

```python
from sklearn.cluster import KMeans

final_kmeans = KMeans(
    n_clusters=3,
    random_state=42,
    n_init=10
)

customer_data['Cluster'] = final_kmeans.fit_predict(X_scaled)
```

Each customer was assigned to one of three clusters: Cluster 0, Cluster 1, or Cluster 2.

---

## 10. Cluster Distribution

The final customer distribution was:

| Cluster   | Number of Customers | Percentage |
| --------- | ------------------: | ---------: |
| Cluster 0 |                 744 |     62.57% |
| Cluster 1 |                 434 |     36.50% |
| Cluster 2 |                  11 |      0.93% |

The majority of customers belong to Cluster 0, while Cluster 2 is a very small group.

---

## 11. Cluster Analysis

### Cluster 0

Cluster 0 contains **744 customers**.

Average characteristics:

* Total Orders: 1.00
* Total Quantity: 2.22
* Total Spending: 558.32
* Average Order Value: 558.32
* Average Items in Cart: 4.59

This cluster represents customers with relatively lower purchasing quantity and spending.

---

### Cluster 1

Cluster 1 contains **434 customers**.

Average characteristics:

* Total Orders: 1.00
* Total Quantity: 4.21
* Total Spending: 1,912.07
* Average Order Value: 1,912.07
* Average Items in Cart: 7.05

This group shows higher purchasing activity, spending, and cart size compared with Cluster 0.

---

### Cluster 2

Cluster 2 contains **11 customers**.

Average characteristics:

* Total Orders: 2.00
* Total Quantity: 5.45
* Total Spending: 1,775.98
* Average Order Value: 887.99
* Average Items in Cart: 5.05

This small cluster is characterized by repeat orders. Its average total spending is high, while its average order value is lower than Cluster 1 because customers in this group placed multiple orders.

---

## 12. Cluster Summary

| Feature           | Cluster 0 | Cluster 1 | Cluster 2 |
| ----------------- | --------: | --------: | --------: |
| Total Orders      |      1.00 |      1.00 |      2.00 |
| Total Quantity    |      2.22 |      4.21 |      5.45 |
| Total Spending    |    558.32 |   1912.07 |   1775.98 |
| Avg Order Value   |    558.32 |   1912.07 |    887.99 |
| Avg Items in Cart |      4.59 |      7.05 |      5.05 |

The table shows clear differences in customer purchasing behavior across the three groups.

---

## 13. PCA Visualization

Principal Component Analysis (PCA) was used to reduce the five-dimensional standardized feature space to two dimensions.

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)
```

A scatter plot was then created using the first two principal components.

The PCA visualization provides a two-dimensional representation of the customer clusters and helps visually examine the distribution of the segmented customers.

---

## 14. Key Findings

The clustering analysis identified three distinct customer groups based on purchasing behavior.

### Finding 1

Cluster 0 represents the largest customer group, containing 62.57% of customers. These customers generally have lower spending and purchasing quantities.

### Finding 2

Cluster 1 contains 36.50% of customers and shows higher spending, quantity, and average cart activity.

### Finding 3

Cluster 2 contains only 0.93% of customers and is characterized by repeat orders. These customers placed an average of two orders.

### Finding 4

Customer spending and quantity were important characteristics for distinguishing between the larger customer groups.

---

## 15. Business Relevance

Customer clustering can help businesses understand different purchasing patterns.

The identified segments can be used as a starting point for:

* Customer behavior analysis
* Personalized marketing
* Customer retention analysis
* Promotional campaign planning
* Understanding purchasing patterns
* Identifying repeat customers

These potential applications would require additional business information before making specific marketing decisions.

---

## 16. Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Jupyter Notebook
* VS Code

---

## 17. Project Output

The project produced the following outputs:

* `Project3.ipynb` — Complete analysis notebook
* `Customer_Clusters.csv` — Customer-level clustering results
* `README.md` — Project overview
* `Report.md` — Detailed project report

---

## 18. Conclusion

This project demonstrated the use of unsupervised machine learning for customer segmentation.

The transaction-level dataset was transformed into customer-level behavioral features, standardized, and analyzed using K-Means clustering. After comparing clustering evaluation measures and examining the resulting groups, three clusters were selected for the final analysis.

The resulting segments showed differences in customer spending, quantity, order value, cart activity, and order frequency. PCA was also used to visualize the clusters in two dimensions.

Overall, the project demonstrates how customer transaction data can be transformed into meaningful behavioral segments using data preprocessing, feature engineering, scaling, K-Means clustering, and visualization.
