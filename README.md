# Customer-Segmentation---KMeans-Hierarchical-GMM
Credit Card Customer Analytics

# Customer Segmentation of AllLife Bank Credit-Card Customers

## Overview

This is an **academic data science project** completed as part of my Post Graduate Program in Data Science & Generative AI.

The objective of this project is to segment credit-card customers based on their credit profile and interaction behaviour with the bank, and to identify actionable customer groups that can support more targeted marketing and service strategies. The dataset contains 660 customer records and five behavioural features used for clustering.

The project applies and compares multiple unsupervised learning approaches, with **K-Means selected as the final segmentation model** based on interpretability, computational efficiency, scalability, and consistency with alternative clustering methods.

---

## Business Problem

The bank has limited visibility into how customers differ in value and in the way they interact with different service channels.

The goal is to identify meaningful customer segments that can help the bank:

- tailor marketing campaigns
- improve service delivery
- encourage digital adoption
- identify high-value customers
- reduce unnecessary servicing effort
- support retention and cross-selling strategies

The available dataset does not contain actual transaction or spending values, so customer value is interpreted using credit-limit and card-ownership information together with interaction behaviour.

---

## Dataset

The dataset contains **660 customer records**.

The main features used for clustering are:

| Feature | Description |
|---|---|
| `Avg_Credit_Limit` | Average credit limit of the customer |
| `Total_Credit_Cards` | Number of credit cards held |
| `Total_visits_bank` | Number of branch visits |
| `Total_visits_online` | Number of online visits |
| `Total_calls_made` | Number of calls made to the bank |

Identifier columns were excluded before modelling.

---

## Exploratory Data Analysis

EDA indicated several meaningful behavioural patterns:

- Average credit limit is strongly right-skewed and multimodal.
- Customers with higher credit limits generally hold more credit cards.
- Higher-value customers tend to engage more through online channels.
- Lower-credit customers tend to show greater phone-based interaction.
- Online visits and branch visits show an inverse relationship, suggesting different preferred interaction channels.
- The data visually suggested the presence of distinct customer groups before clustering was applied.

---

## Data Preprocessing

The following preprocessing steps were applied:

- No missing-value imputation was required.
- Genuine extreme credit-limit values were retained because they may represent meaningful high-value customers.
- `Avg_Credit_Limit` was transformed using `log1p()` to reduce right skew.
- All clustering features were standardized using `StandardScaler`.
- A feature-engineered pipeline was also tested using:
  - `Total_interactions`
  - `bank_share`
  - `online_share`
  - `calls_share`

The baseline feature representation ultimately produced the stronger clustering solution.

---

## Models Evaluated

### 1. K-Means Clustering

K-Means was evaluated across multiple values of `k` using:

- inertia / elbow method
- silhouette score
- silhouette diagram
- business interpretability

The final K-Means solution used:

- **k = 3**
- **Silhouette Score = 0.493**

The three-cluster solution provided a clear and actionable customer segmentation.

---

### 2. Hierarchical Clustering

Hierarchical clustering was evaluated using multiple linkage methods and distance metrics.

The final hierarchical configuration used:

- **Average linkage**
- **Cityblock / Manhattan distance**
- **k = 3**
- **Silhouette Score = 0.533**
- **Cophenetic Correlation ≈ 0.86**

Although hierarchical clustering achieved slightly stronger separation on this small dataset, K-Means was retained as the final practical model because it identified the same broad segments while being substantially more scalable.

---

### 3. Gaussian Mixture Model — Exploratory Extension

A Gaussian Mixture Model was explored as an additional clustering approach after PCA suggested that some clusters were not perfectly spherical.

Unlike K-Means, GMM provides **probabilistic membership**, making it possible to identify customers near segment boundaries.

This was used as a supplementary robustness check rather than as the final segmentation model.

---

## Final Customer Segments

The final K-Means solution identified three customer groups:

| Segment | Approx. Size | Description |
|---|---:|---|
| High-value digital-first | 50 customers (~8%) | Very high credit limits, more cards, strong online engagement, minimal branch and phone interaction |
| Moderate-value branch-oriented | 385 customers (~58%) | Moderate credit limits and card ownership, stronger branch preference, relatively low digital and phone engagement |
| Low-value call-heavy | 225 customers (~34%) | Lower credit limits, fewer cards, high call activity, moderate online engagement |

These profiles were consistent across K-Means and Hierarchical Clustering.

---

## Cross-Method Stability

A cross-tabulation of K-Means and Hierarchical Clustering assignments showed that **657 of 660 customers (99.5%)** were assigned to equivalent business segments across the two approaches.

This provided additional evidence that the three-segment structure was robust and not merely an artifact of one clustering algorithm.

The high-value digital-first segment was especially stable across methods.

---

## PCA Visualization

Principal Component Analysis was used as a visualization and diagnostic tool.

The first three principal components explained approximately:

- PC1: 47.0%
- PC2: 32.7%
- PC3: 8.4%

Together, they retained approximately **88.2% of the total variance**.

The 3D PCA projection visually supported the presence of three broad customer groups, while also showing that some observations lie near cluster boundaries.

PCA was used for interpretation and visualization only, not as the primary clustering input.

---

## Key Business Recommendations

### High-value digital-first customers

**Marketing**
- premium cards
- travel and rewards offers
- personalized digital campaigns
- relevant cross-sell opportunities

**Service**
- seamless app and web experience
- proactive digital support
- premium digital servicing

### Moderate-value branch-oriented customers

**Marketing**
- relevant credit products
- gradual digital-adoption incentives

**Service**
- maintain strong branch support
- assisted digital onboarding
- hybrid service options

### Low-value call-heavy customers

**Marketing**
- avoid aggressive premium-product targeting
- focus on simple and relevant products
- provide financial education where appropriate

**Service**
- improve call-center support
- identify common call reasons
- offer self-service options for repetitive service requests

These recommendations were derived from the behavioural profiles of the final customer segments.

---

## Final Model Choice

**K-Means with k = 3** was selected as the final segmentation model.

Although Hierarchical Clustering achieved a slightly higher silhouette score, K-Means:

- identified essentially the same customer structure
- was computationally faster
- is easier to operationalize
- scales better to large customer datasets
- produced highly interpretable business segments

For a real-world banking environment with potentially millions of customers, this scalability advantage becomes important.

---

## Tools & Libraries

- Python
- pandas
- NumPy
- matplotlib
- seaborn
- scikit-learn
- SciPy

---

## Project Type

**Academic Project**

This repository was created for educational purposes as part of my postgraduate coursework in Data Science & Generative AI.

The analysis is intended to demonstrate:

- exploratory data analysis
- preprocessing for distance-based models
- K-Means clustering
- hierarchical clustering
- silhouette analysis
- cophenetic correlation
- PCA-based visualization
- exploratory Gaussian Mixture Models
- cluster profiling
- business interpretation and recommendations

The project should not be interpreted as a production banking model or as a real customer decisioning system.

---

## Author

**Priyanka Manoj**  
Post Graduate Program in Data Science & Generative AI
