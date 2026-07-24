# Identifying High-Risk Credit Card Customers

Banks issuing credit cards cannot easily tell which customers are quietly
accumulating debt they are unlikely to repay.

This analysis examined **8,636 credit card customers** and found that
**1,156 (13.4%)** rely heavily on cash advances — averaging **$4,586** per
customer — while clearing their balance in full only **3.5% of the time**.

**🔗 [View the interactive dashboard on Tableau Public](https://public.tableau.com/app/profile/monica.qiao/viz/CreditCardCustomerSegmentationAnalysis_17846397126950/CreditCardCustomerAnalysisDashboard)**


---

## Dataset
- 8,950 credit card customers
- 17 behavioral features (excluding customer ID)
- Key variables include:
  - BALANCE
  - PURCHASES
  - CREDIT_LIMIT
  - PAYMENTS
  - CASH_ADVANCE
  - FREQUENCY features

After cleaning, the final dataset contains **8,636 customers**.

The dataset has no default flag, so I used heavy cash-advance reliance combined with a low full-payment rate as a **risk proxy**.

---

## Project Workflow
- Data understanding and exploratory analysis
- Data cleaning and preprocessing
- Feature preparation for clustering
- Feature scaling (Standardization)
- Customer segmentation using KMeans clustering
- Model evaluation (Elbow Method & Silhouette Score)
- Dimensionality reduction using PCA
- Business interpretation of customer segments

---

## 🤖 Machine Learning Model
- Algorithm: KMeans Clustering
- Type: Unsupervised Learning
- Number of clusters: 4 (silhouette favours K=3; K=4 retained for business interpretability — see notebook §9.1)


---

## 📈 Results

| Segment | Customers | Avg purchases | Avg cash advance | Avg balance | Pays in full |
|---|---|---|---|---|---|
| Regular Active | 3,281 (38.0%) | $1,265 | $218 | $913 | 27.4% of the time |
| High-Value | 394 (4.6%) | $7,816 | $658 | $3,586 | 29.2% of the time |
| Low-Activity | 3,805 (44.1%) | $274 | $607 | $1,061 | 8.4% of the time |
| **Cash Advance** | **1,156 (13.4%)** | **$506** | **$4,586** | **$4,655** | **3.5% of the time** |

The **Cash Advance** segment stands out as the highest-risk customer group, averaging **$4,586** in cash advances—nearly **7×** more than the next-highest segment (**$658**)—while paying their balance in full only **3.5% of the time**, the lowest rate among all customer segments.



---

## Recommendation

The Cash Advance segment represents **1,156 customers (13.4%)** who demonstrate high reliance on cash advances, averaging **$4,586** in cash advances over the six-month observation period. This group also carries the highest average outstanding balance at **$4,655**, representing approximately **$5.38 million in outstanding balances** across the segment.

Assuming a **29.99% APR** on revolving credit card balances, this represents approximately **$1.61 million in potential annual interest exposure**. As an illustrative risk-mitigation scenario, refinancing these balances at a **12% rate** would reduce the potential annual interest yield by approximately **$968K** ($1.61M at 29.99% APR versus $646K at 12% APR). The actual financial impact would depend on customer repayment behavior, refinancing adoption, and credit performance outcomes.

This trade-off would be financially justified if preventing credit losses creates more than **$968K in annual value** — equivalent to preventing more than **18% of the $5.38M in refinanced balances from becoming losses**. This threshold should be validated against the bank’s historical delinquency and loss data before implementing such a strategy.

This dataset does not include **default or delinquency indicators**, so repayment risk is inferred from behavioral patterns such as cash advance usage, outstanding balances, and full-payment frequency rather than directly observed credit outcomes.


---

## Tools Used
- Python
- pandas — data loading and manipulation
- scikit-learn — StandardScaler, KMeans, PCA, silhouette score
- Matplotlib — elbow plot
- Seaborn — cluster scatter plot
- Tableau Public — interactive segment dashboard
