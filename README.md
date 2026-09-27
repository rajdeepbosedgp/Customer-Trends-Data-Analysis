# Customer Trends Data Analysis (SQL, Python & Power BI)

**Author:** Rajdeep Bose  
**Repository:** customer-trends-data-analysis-SQL-Python-PowerBI  
**Tools & Technologies:** Python (Pandas, NumPy, SciPy, Scikit-Learn, SQLAlchemy, PyPDF, python-pptx), SQL (PostgreSQL / MySQL / MS SQL Server), Power BI, PowerPoint.

---

## Project Overview

This project provides an enterprise-grade data analysis of customer shopping behavior using transactional data from **3,900 consumer purchases** across multiple product categories, demographics, and shipping channels.

Designed to demonstrate high-level data engineering and analytical skills, this project combines **Exploratory Data Analysis (EDA)**, **Statistical Hypothesis Testing**, **Unsupervised & Supervised Machine Learning**, **Advanced SQL Queries (Q1-Q14)**, **Star Schema Power BI Modeling**, and **Executive Presentation Artifacts**.

---

## Repository Structure

```text
customer-trends-data-analysis-SQL-Python-PowerBI/
│
├── Customer_Shopping_Behavior_Analysis.ipynb   # Python Notebook (EDA, Stat Testing, ML & SQL Ingestion)
├── customer_behavior_sql_queries.sql           # SQL Scripts (14 Business & Enterprise Analytics Queries)
├── customer_behavior_dashboard.pbix            # Interactive Power BI Dashboard
├── customer_shopping_behavior.csv             # Raw Transactional Dataset (3,900 rows)
├── Customer-Shopping-Behavior-Analysis.pptx    # Executive Presentation Slides
├── Customer Shopping Behavior Analysis.pdf     # Project Summary Documentation Report
├── Business Problem  Document.pdf              # Initial Business Requirements & Problem Statement
└── README.md                                  # Comprehensive Project Documentation
```

---

## Key Analytical Highlights & Methodologies

### 1. Data Cleaning & Feature Engineering (Python)
- **Dataset Ingestion:** 3,900 transaction records with 18 original features.
- **Missing Value Imputation:** Imputed 37 missing `Review Rating` values using category median transform.
- **Column Standardization:** Re-indexed all features into `snake_case` format.
- **Feature Engineering:**
  - `age_group`: Binned customer ages into `Young Adult`, `Adult`, `Middle-aged`, and `Senior`.
  - `purchase_frequency_days`: Mapped purchase frequency text (Weekly = 7 days, Fortnightly = 14 days, Annually = 365 days).
- **Automated Database Ingestion:** Configured `SQLAlchemy` engine to push clean DataFrames directly into PostgreSQL, MySQL, or SQL Server.

---

### 2. Statistical Hypothesis Testing
To validate business intuition with statistical rigor, hypothesis tests were conducted in Python (`scipy.stats`):

- **Two-Sample T-Test (Express vs Standard Shipping Spend)**:
  - *H0*: No difference in average purchase amount between Express and Standard shipping.
  - *Results*: T-Statistic = 1.5108, P-Value = 0.1311.
  - *Business Conclusion*: While Express users average slightly higher transaction values, the spending difference is not statistically significant at alpha = 0.05.
- **Chi-Square Test of Independence (Age Group vs Subscription Status)**:
  - *H0*: Subscription status is independent of customer age group.
  - *Results*: Chi2 = 2.4321, P-Value = 0.4877.
  - *Business Conclusion*: Subscription status is independent of age group; subscriber targeting should focus on behavioral triggers rather than demographic age brackets.

---

### 3. Advanced Machine Learning (Scikit-Learn)

#### A. Unsupervised K-Means Customer Clustering
Segmented 3,900 customers into 4 distinct operational clusters using scaled features (`age`, `purchase_amount`, `previous_purchases`, `review_rating`, `purchase_frequency_days`):
- **Cluster 0 (Young Mid-Spenders)**: Avg Age 41.5, Avg Spend $59.38, High purchase frequency.
- **Cluster 1 (Young High-Frequency Shoppers)**: Avg Age 30.3, Avg Spend $60.01, High engagement.
- **Cluster 2 (Annual Low-Frequency Buyers)**: Avg Age 44.7, Avg Spend $60.17, 365-day purchase interval.
- **Cluster 3 (Senior High-Spenders)**: Avg Age 58.6, Avg Spend $59.76.

#### B. Supervised Random Forest Subscription Classifier
Built a Random Forest model (`RandomForestClassifier`, 100 estimators) to predict customer subscription likelihood:
- **Model Accuracy**: **82.82%** test set accuracy.
- **Top Predictors**: Purchase frequency days, previous purchase count, review rating, and purchase amount.

---

### 4. Enterprise SQL Analytics (Q1 - Q14)
SQL queries written for PostgreSQL, MySQL, and MS SQL Server:

- **Q1 - Gender Revenue Breakdown**: Compared revenue contribution between male and female segments.
- **Q2 - High-Spending Discount Users**: Filtered discount users spending above the dataset mean ($59.76).
- **Q3 - Top 5 Rated Products**: Extracted items with highest average review rating.
- **Q4 - Shipping Type Spend Comparison**: Compared average transaction amount across shipping tiers.
- **Q5 - Subscriber Value Analysis**: Compared annual spend and total revenue between subscribers and non-subscribers.
- **Q6 - Discount-Dependent Items**: Calculated top 5 products by discount application percentage.
- **Q7 - Customer Loyalty Segmentation**: Binning users into `New` (1), `Returning` (2-10), and `Loyal` (>10) tiers.
- **Q8 - Top 3 Products per Category**: Used `ROW_NUMBER() OVER (PARTITION BY category)` window functions.
- **Q9 - Repeat Buyer Subscription Conversion**: Analyzed subscription rate for customers with >5 purchases.
- **Q10 - Age Group Revenue Contribution**: Calculated aggregated revenue by age demographic.
- **Q11 - RFM Percentile Scoring (`NTILE(5)`)**: Computed Recency, Frequency, and Monetary scores (1-5) and classified customers into `Champions`, `Loyal`, `Promising`, and `At Risk`.
- **Q12 - Cumulative Category Revenue & Share of Wallet**: Calculated running total revenue using `SUM() OVER (ORDER BY category_revenue DESC)`.
- **Q13 - Shipping Tier Density & Discount Usage**: Evaluated discount rates across shipping methods.
- **Q14 - Customer Lifetime Value (CLV) & Risk Tiering**: Segmented customers into CLV Tiers 1-4 based on historical purchases and transaction size.

---

### 5. Power BI Architecture & DAX Measures

#### Data Architecture: Star Schema Model
The Power BI data model is structured using an enterprise Star Schema:
- **Fact Table**: `fact_transactions` (contains transaction metrics: purchase amount, review rating, previous purchases).
- **Dimension Tables**: `dim_customer` (demographics), `dim_product` (item, category, size, color), `dim_shipping` (type, location), `dim_date` (purchase interval).

#### Key DAX Measures
```dax
-- Total Revenue
Total Revenue = SUM(fact_transactions[purchase_amount])

-- Average Order Value (AOV)
Average Order Value = AVERAGE(fact_transactions[purchase_amount])

-- Subscriber Revenue Contribution %
Subscriber Rev Share % = 
DIVIDE(
    CALCULATE([Total Revenue], fact_transactions[subscription_status] = "Yes"),
    [Total Revenue],
    0
)

-- Express Shipping Premium %
Express Premium % = 
VAR ExpressAOV = CALCULATE([Average Order Value], fact_transactions[shipping_type] = "Express")
VAR StandardAOV = CALCULATE([Average Order Value], fact_transactions[shipping_type] = "Standard")
RETURN DIVIDE(ExpressAOV - StandardAOV, StandardAOV, 0)
```

---

## How to Run & Reproduce

### 1. Python Environment Setup
Install required Python dependencies:
```bash
pip install pandas numpy scipy scikit-learn sqlalchemy psycopg2-binary pymysql pyodbc pypdf python-pptx
```

### 2. Run Data Pipeline & Machine Learning
Open and run all cells in [`Customer_Shopping_Behavior_Analysis.ipynb`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/Customer_Shopping_Behavior_Analysis.ipynb):
```bash
jupyter notebook Customer_Shopping_Behavior_Analysis.ipynb
```

### 3. Execute Enterprise SQL Queries
Load the dataset into your database engine and run [`customer_behavior_sql_queries.sql`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/customer_behavior_sql_queries.sql).

### 4. Power BI Dashboard
Open [`customer_behavior_dashboard.pbix`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/customer_behavior_dashboard.pbix) in Power BI Desktop to interact with the visualizations.

---

## Strategic Recommendations

1. **Deploy Subscription Propensity Scoring**: Use the Random Forest classification model to target high-probability non-subscribers with personalized incentive offers.
2. **Automate RFM Customer Workflows**: Leverage SQL RFM scoring (`Q11`) to automatically trigger retention campaigns for `At Risk` customers before churn occurs.
3. **Optimize Discount Policy**: Rationalize discount usage on top-rated items like Blouses and Dresses, retaining discounts for high-margin upsells.
4. **Capitalize on Express Shipping Demand**: Express shipping users demonstrate high purchasing density; introduce express delivery perks as a primary subscription benefit.

---

## Behavioral Interview STAR Method Walkthrough

- **Situation**: A retail company with 3,900 customer records wanted to optimize marketing spend, increase subscription conversion, and reduce customer churn.
- **Task**: Build an end-to-end analytical framework covering data cleaning, statistical testing, customer ML segmentation, enterprise SQL queries, and Power BI dashboards.
- **Action**: Cleaned dataset in Python, performed T-Tests and Chi-Square tests, built K-Means clustering and Random Forest prediction models (82.82% accuracy), authored 14 enterprise SQL queries (RFM scoring, cumulative revenue window functions), and structured a Star Schema in Power BI with custom DAX measures.
- **Result**: Delivered actionable business insights including predictive subscription scoring, statistical shipping validation, and customer lifetime value tiering.

---

## Author & Contact

**Rajdeep Bose**  
*Data Analyst & Machine Learning Specialist*  
GitHub: [rajdeepbosedgp](https://github.com/rajdeepbosedgp)
