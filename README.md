# E-commerce-Customer-Analytics

## Project Overview

This project builds an end-to-end data science pipeline for e-commerce customer analytics using the UCI Online Retail dataset.
The goal is to translate raw transactional data into actionable business insights that improve revenue growth, customer retention, and marketing efficiency.

Using a combination of lifecycle metrics, customer segmentation, predictive modeling, and churn analysis, the project demonstrates how data science can support real-world decision-making in an e-commerce setting.

## Business Questions Addressed

* How concentrated is revenue across customers?
* Are repeat customers more valuable than new customers?
* Which customer segments drive the most revenue?
* Which customers are likely to generate the highest future value?
* Which high-value customers are at risk of churn and should be prioritized for retention?

## Project Structure

ecommerce-online-retail/
│
├── data/
│   ├── raw/online_retail.xlsx
│   ├── processed/
│   │   ├── online_retail_clean.csv
│   │   └── rfm_segments.csv
│
├── notebooks/
│   ├── 01_cleaning_eda.ipynb
│   ├── 02_funnel_metrics.ipynb
│   ├── 03_rfm_segmentation.ipynb
│   ├── 04_clv_prediction.ipynb
│   └── 05_churn_model.ipynb
│
├── dashboard/           
├── README.md

## Dataset

Source: UCI Online Retail Dataset

Data Type: Transaction-level retail purchase data

Key Fields:
InvoiceNo, CustomerID, InvoiceDate, Quantity, UnitPrice, Revenue, Country

Note: The dataset does not contain web/session logs (page views, carts), so all analysis is based on transactional behavior not clickstream data.

## Methods & Workflow

**1. Data Cleaning & Exploratory Analysis**

Notebook: 01_cleaning_eda.ipynb

- Removed cancellations, invalid quantities, and missing customer IDs
- Created derived revenue metrics
- Analyzed revenue distribution, seasonality, and customer concentration

**2. Customer Lifecycle Funnel & Core Metrics**

Notebook: 02_funnel_metrics.ipynb

Because session data is unavailable, a transaction-based lifecycle funnel was constructed:
- New customers -> Repeat customers -> Retained customers -> High-value customers
- Key metrics: Revenue, AOV, Repeat Purchase Rate, Revenue per Customer
- Time-to-second-purchase used as a proxy for engagement

**3. RFM Customer Segmentation**

Notebook: 03_rfm_segmentation.ipynb

- Built order-level RFM features (Recency, Frequency, Monetary)
- Log-transformed skewed features and scaled inputs
- Clustered customers using K-Means
- Mapped clusters to business-friendly segments:
    * High-Value Loyal
    * Recent Big Spenders
    * At-Risk Customers
    * Low Engagement

**4. Customer Lifetime Value (CLV) Prediction**

Notebook: 04_clv_prediction.ipynb

- Defined CLV as future revenue over a fixed horizon
- Used time-based train/future split to avoid leakage
- Compared against a strong baseline (past spend)
- Trained an ML model to rank customers by predicted CLV

**5. Churn Modeling & Retention Risk**

Notebook: 05_churn_model.ipynb

- Defined churn behaviorally as prolonged inactivity (>90 days)
- Trained classification models using RFM features
- Evaluated using ROC-AUC due to class imbalance
- Translated churn probabilities into revenue at risk

**Summary**

- Identified that top customer segments generate a disproportionate share of revenue
- Ranked customers by future value, not just historical spend
- Quantified revenue at risk due to churn
- Enabled targeted retention strategies with higher ROI than broad campaigns

**Conclusion**

This project demonstrates how transaction-level e-commerce data can be transformed into actionable customer intelligence through careful data preparation, behavioral segmentation, and predictive modeling. By combining lifecycle metrics, RFM segmentation, customer lifetime value prediction, and churn modeling, the analysis shows that a small subset of customers drives a disproportionate share of revenue, and that targeted retention of high-value, high-risk customers offers the greatest business impact.

Rather than focusing solely on model accuracy, the project emphasizes business decision support—identifying who to prioritize, why they matter, and how interventions can improve long-term revenue outcomes. The workflow is fully reproducible, modular, and designed to reflect how data science is applied in real e-commerce organizations.

**Future Work**

Potential extensions of this project include:
- Incorporating session-level or clickstream data to build true conversion funnels
- Adding marketing cost data to estimate profit-based CLV
- Validating retention strategies using A/B testing or uplift modeling
- Deploying the models via an interactive dashboard or API for real-time decision support
