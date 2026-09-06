Project 1: Advanced EDA & Feature
Engineering
Dataset: Titanic Dataset (891 rows, 12 original columns)
Submitted by: Muqaddas — Data Science Intern, DecodeLabs
1. Objective
Transform the raw Titanic dataset into a mathematically clean, ML￾ready dataset by handling missing values, neutralizing outliers, and
engineering new predictive features.
2. Handling Missing Values
Column
Missing
Count
%
Missing
Strategy Used Reasoning
Age 177 ~20%
Median
Imputation
Age was
moderately
missing; median
avoids distortion
from skew, unlike
mean.
Embarked 2 ~0.2%
Row Deletion
(dropna)
Negligible missing
count — dropping
preserves data
integrity without
adding synthetic
bias.
Column
Missing
Count
%
Missing
Strategy Used Reasoning
Cabin 687 ~77%
Converted to
binary feature
( Has_Cabin ),
original
column
dropped
Missingness was
too extreme
(>75%) to impute
reliably;
presence/absence
of a cabin record
is itself
informative.
df['Age'] = df['Age'].fillna(df['Age'].median())
df = df.dropna(subset=['Embarked'])
df['Has_Cabin'] = df['Cabin'].notnull().astype(int)
df = df.drop('Cabin', axis=1)
3. Handling Outliers
Column checked: Fare
Mean fare ≈ 32, but maximum fare was 512.33 — a clear
statistical anomaly compared to the 75th percentile (~31).
Method used: Interquartile Range (IQR) capping (Winsorization)
instead of row deletion, to preserve all 889 rows.
Q1 = df['Fare'].quantile(0.25)
Q3 = df['Fare'].quantile(0.75)
IQR = Q3 - Q1
lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
df['Fare'] = df['Fare'].clip(lower, upper)
Result: Maximum fare reduced from 512.33 → 65.66, while row
count remained unchanged (no data loss).
4. Feature Engineering (3 New Features)
Feature Formula / Logic Purpose
FamilySize
SibSp + Parch +
1
Captures total family
members aboard,
potentially correlated
with survival.
IsAlone
1 if FamilySize
== 1 else 0
Flags solo travelers, who
may have had different
survival odds than
families.
Title
Extracted from
Name (e.g., Mr, Mrs,
Miss, Master)
Captures social
status/age group not
directly present in other
columns.
df['FamilySize'] = df['SibSp'] + df['Parch'] + 1
df['IsAlone'] = (df['FamilySize'] == 1).astype(int)
df['Title'] = df['Name'].str.extract(r',\s*([^\.]+)\.')
5. Final Dataset
Rows: 889 (2 dropped due to missing Embarked )
All missing values resolved
Outliers capped, not deleted
3 new engineered features added
Saved as titanic_cleaned.csv
6. Key Learnings
Choice of imputation strategy should depend on the percentage
of missingness, not applied uniformly.
Capping (clip) is preferable to deletion when preserving row
count/sequence matters.
Feature engineering from existing columns (like extracting titles
from names) can surface predictive signal that raw columns
don't expose directly
