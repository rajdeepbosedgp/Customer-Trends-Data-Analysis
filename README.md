# Customer Analytics & Behavioral Intelligence (SQL, Python & Power BI)

**Author:** Rajdeep Bose  
**Repository:** customer-trends-data-analysis-SQL-Python-PowerBI  
**Tools & Technologies:** Python (Pandas, NumPy, SciPy, Scikit-Learn, SQLAlchemy, PyPDF, python-pptx), SQL (PostgreSQL / MySQL / MS SQL Server), Power BI, PowerPoint.

---

## Project Overview

This project provides an end-to-end data analysis of customer shopping behavior using transactional data from **3,900 consumer purchases** across multiple product categories, demographics, and shipping channels.

Designed as a comprehensive **Customer Analytics & Behavioral Intelligence** portfolio project, it combines **Exploratory Data Analysis (EDA)**, **Statistical Hypothesis Testing**, **Unsupervised K-Means Customer Clustering**, **Supervised Machine Learning Comparison**, **Advanced Analytical SQL Queries (Q1-Q14)**, **Star Schema Power BI Modeling**, and **Executive Presentation Artifacts**.

---

## Repository Structure

```text
customer-trends-data-analysis-SQL-Python-PowerBI/
│
├── Customer_Shopping_Behavior_Analysis.ipynb   # Python Notebook (EDA, Stat Testing, ML & SQL Ingestion)
├── customer_behavior_sql_queries.sql           # SQL Scripts (14 Business & Behavioral Analytics Queries)
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
- **Secure Database Ingestion:** Configured `SQLAlchemy` engine using environment variable authentication (`os.getenv("DB_PASSWORD")`) to safely push clean DataFrames directly into PostgreSQL, MySQL, or SQL Server.

---

### 2. Statistical Hypothesis Testing
To validate business intuition with statistical rigor, hypothesis tests were conducted in Python (`scipy.stats`):

- **Two-Sample T-Test (Express vs Standard Shipping Spend)**:
  - *H0*: No difference in average purchase amount between Express and Standard shipping.
  - *Results*: T-Statistic = 1.5108, P-Value = 0.1311.
  - *Business Conclusion*: Fail to reject H0. While Express users average slightly higher transaction values ($65 vs $58), the difference is not statistically significant at alpha = 0.05.
- **Chi-Square Test of Independence (Age Group vs Subscription Status)**:
  - *H0*: Subscription status is independent of customer age group.
  - *Results*: Chi2 = 2.4321, P-Value = 0.4877.
  - *Business Conclusion*: Fail to reject H0. Subscription status is independent of age group; subscriber targeting should focus on behavioral triggers rather than demographic age brackets.

---

### 3. Unsupervised K-Means Customer Clustering & K Optimization

#### Cluster Evaluation & K Selection Justification
Candidate cluster counts (K=2 to 6) were evaluated using **Inertia (Elbow Method)** and **Silhouette Score** on standardized behavioral features (`age`, `purchase_amount`, `previous_purchases`, `review_rating`, `purchase_frequency_days`):

| K (Clusters) | Inertia | Silhouette Score |
| :---: | :---: | :---: |
| K = 2 | 15895.72 | 0.2979 |
| K = 3 | 13357.41 | 0.1948 |
| **K = 4 (Selected)** | **11819.85** | **0.1820** |
| K = 5 | 10564.51 | 0.1897 |
| K = 6 | 9634.72 | 0.1935 |

**Justification for K=4**: Evaluated candidate cluster counts using inertia and silhouette scores. K=4 was selected as it provides an optimal balance between cluster separation and practical business interpretability.

#### Cluster Behavioral Profiles
- **Cluster 0 (Young Mid-Spenders)**: Avg Age 41.5, Avg Spend $59.38, High order frequency (~41 days).
- **Cluster 1 (Young High-Frequency Shoppers)**: Avg Age 30.3, Avg Spend $60.01, High engagement (~42 days).
- **Cluster 2 (Annual Low-Frequency Buyers)**: Avg Age 44.7, Avg Spend $60.17, 365-day purchase interval.
- **Cluster 3 (Senior High-Spenders)**: Avg Age 58.6, Avg Spend $59.76.

---

### 4. Supervised Machine Learning Model Comparison

Target Variable: `subscription_status` (1 = Subscriber, 0 = Non-Subscriber)  
Dataset Split: 80% Train, 20% Test (`stratify=y`)

#### Model Evaluation Matrix
| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Logistic Regression (Baseline)** | **85.00%** | **77.12%** | **72.49%** | **0.7473** | **0.9109** |
| Random Forest Classifier | 82.82% | 72.08% | 66.67% | 0.6927 | 0.9074 |

#### Model Comparison Conclusion
Logistic Regression established a strong baseline with **85.00% accuracy** and an **ROC-AUC of 0.9109**, outperforming Random Forest on recall and F1-score due to linear separability across engineered frequency features.

---

### 5. Advanced SQL Analytics (Q1 - Q14)
SQL queries written for PostgreSQL, MySQL, and MS SQL Server:

- **Q1 - Gender Revenue Breakdown**: Compared revenue contribution between male and female segments.
- **Q2 - High-Spending Discount Users**: Filtered discount users spending above the dataset mean ($59.76).
- **Q3 - Top 5 Rated Products**: Extracted items with highest average review rating.
- **Q4 - Shipping Type Spend Comparison**: Compared average transaction amount across shipping tiers.
- **Q5 - Subscriber Value Analysis**: Compared annual spend and total revenue between subscribers and non-subscribers.
- **Q6 - Discount-Dependent Items**: Calculated top 5 products by discount application percentage.
- **Q7 - Customer Loyalty Segmentation**: Binned users into `New` (1), `Returning` (2-10), and `Loyal` (>10) tiers.
- **Q8 - Top 3 Products per Category**: Used `ROW_NUMBER() OVER (PARTITION BY category)` window functions.
- **Q9 - Repeat Buyer Subscription Conversion**: Analyzed subscription rate for customers with >5 purchases.
- **Q10 - Age Group Revenue Contribution**: Calculated aggregated revenue by age demographic.
- **Q11 - Behavioral Customer Segmentation (RFM-Inspired)**: Computed Recency proxy, Frequency, and Monetary scores (1-5) via `NTILE(5)` window functions to classify customers into `Champions`, `Loyal`, `Promising`, and `At Risk`.
- **Q12 - Cumulative Category Revenue & Share of Wallet**: Calculated running total revenue using `SUM() OVER (ORDER BY category_revenue DESC)`.
- **Q13 - Shipping Tier Density & Discount Usage**: Evaluated discount rates across shipping methods.
- **Q14 - High-Value Customer Tiering**: Segmented customers into Customer Value Tiers 1-4 based on historical purchases and transaction size.

---

### 6. Power BI Architecture & DAX Measures

#### Data Architecture: Star Schema Model
Structured using an enterprise Star Schema:
- **Fact Table**: `fact_transactions` (purchase amount, review rating, previous purchases).
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

### 3. Execute SQL Queries
Load the dataset into your database engine and run [`customer_behavior_sql_queries.sql`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/customer_behavior_sql_queries.sql).

### 4. Power BI Dashboard
Open [`customer_behavior_dashboard.pbix`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/customer_behavior_dashboard.pbix) in Power BI Desktop to interact with the visualizations.

---

## Resume Bullet Points

- **Customer Analytics & Behavioral Intelligence** | Python, SQL, PostgreSQL, Power BI, Scikit-learn
  - Analyzed **3,900 customer transactions across 18 behavioral and demographic attributes**, performing data cleaning, feature engineering, exploratory analysis, and statistical hypothesis testing (T-Test, Chi-Square) using Python.
  - Developed **14 SQL analytics queries** using CTEs, window functions (`ROW_NUMBER`, `NTILE`, `SUM OVER`), conditional aggregation, and customer segmentation to analyze revenue, purchasing behavior, subscription patterns, and customer value tiers.
  - Applied **K-Means clustering** to segment customers based on purchasing behavior and built supervised classifiers (Logistic Regression baseline vs Random Forest) to predict subscription likelihood, achieving **85.00% accuracy** and an **ROC-AUC of 0.9109**.
  - Built an interactive **Power BI dashboard** translating customer segments, revenue drivers, subscription behavior, and purchasing trends into actionable business insights.

---

## Author & Contact

**Rajdeep Bose**  
*Data Analyst & Machine Learning Specialist*  
GitHub: [rajdeepbosedgp](https://github.com/rajdeepbosedgp)
