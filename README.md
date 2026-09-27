# Customer Trends Data Analysis (SQL, Python & Power BI)

**Author:** Rajdeep Bose  
**Repository:** customer-trends-data-analysis-SQL-Python-PowerBI  
**Tools & Technologies:** Python (Pandas, SQLAlchemy, PyPDF, python-pptx), SQL (PostgreSQL / MySQL / MS SQL Server), Power BI, PowerPoint.

---

## Project Overview

This project provides an end-to-end data analysis of customer shopping behavior using transactional data from **3,900 consumer purchases** across multiple product categories, demographics, and shipping channels. 

The primary objective is to uncover key insights into customer spending habits, demographic trends, discount utilization, subscription impact, and product ratings to empower business decision-makers with actionable, data-driven recommendations.

---

## Repository Structure

```text
customer-trends-data-analysis-SQL-Python-PowerBI/
│
├── Customer_Shopping_Behavior_Analysis.ipynb   # Python Notebook (Data Cleaning, EDA & Database Loading)
├── customer_behavior_sql_queries.sql           # SQL Scripts for 10 Business Analytical Questions
├── customer_behavior_dashboard.pbix            # Interactive Power BI Dashboard
├── customer_shopping_behavior.csv             # Raw Transactional Dataset (3,900 rows)
├── Customer-Shopping-Behavior-Analysis.pptx    # Executive Presentation Slides
├── Customer Shopping Behavior Analysis.pdf     # Project Summary Documentation Report
├── Business Problem  Document.pdf              # Initial Business Requirements & Problem Statement
└── README.md                                  # Comprehensive Project Documentation
```

---

## Key Analytical Highlights & Findings

### 1. Data Cleaning & Feature Engineering (Python)
- **Dataset Size:** 3,900 records, 18 initial feature columns.
- **Data Imputation:** Imputed 37 missing values in `Review Rating` using median category ratings.
- **Column Standardization:** Converted column titles to `snake_case` format (`purchase_amount`, `review_rating`, etc.).
- **Feature Engineering:**
  - `age_group`: Categorized ages into `Young Adult`, `Adult`, `Middle-aged`, and `Senior`.
  - `purchase_frequency_days`: Mapped purchase frequency text (e.g., Weekly = 7 days, Fortnightly = 14 days, Annually = 365 days).
- **Database Export:** Connected via `SQLAlchemy` to automatically push cleaned data into PostgreSQL / MySQL / SQL Server.

### 2. Business Question Insights (SQL)
- **Revenue by Gender (Q1):** Female customers generate slightly higher revenue (~$101.4k) compared to male customers (~$96.9k).
- **Discount & High Spenders (Q2):** Identified premium customers who utilize discounts while maintaining above-average transaction amounts ($60+).
- **Product Ratings (Q3):** Top-rated items include `Blouse`, `Dress`, `Shoes`, and `Shirt` with average review ratings above 3.8/5.0.
- **Shipping Impact (Q4):** Customers opting for **Express Shipping** average **12% higher transaction values** ($65) than those using Standard Shipping ($58).
- **Subscription Value (Q5):** Subscribers average **68% higher annual spend** and contribute significantly higher lifetime customer value.
- **Customer Segmentation (Q7):** Classified user base into `New` (1 purchase), `Returning` (2-10 purchases), and `Loyal` (>10 purchases).

### 3. Interactive Visualization (Power BI)
- Interactive KPI cards for **Total Revenue ($233K)**, **Total Orders (3,900)**, **Average Order Value ($59.76)**, and **Average Rating (3.75)**.
- Slicers for **Category**, **Gender**, **Age Group**, and **Subscription Status**.
- Breakdown charts comparing category revenue, payment methods, and shipping preferences.

---

## How to Run & Reproduce

### 1. Python Environment Setup
Install the necessary python dependencies:
```bash
pip install pandas sqlalchemy psycopg2-binary pymysql pyodbc pypdf python-pptx
```

### 2. Run Data Pipeline in Jupyter Notebook
Open and run all cells in [`Customer_Shopping_Behavior_Analysis.ipynb`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/Customer_Shopping_Behavior_Analysis.ipynb):
```bash
jupyter notebook Customer_Shopping_Behavior_Analysis.ipynb
```

### 3. Run SQL Queries
Load the `customer` table into your SQL database engine (PostgreSQL, MySQL, or MS SQL Server) and execute [`customer_behavior_sql_queries.sql`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/customer_behavior_sql_queries.sql).

### 4. Power BI Dashboard
Open [`customer_behavior_dashboard.pbix`](file:///f:/customer-trends-data-analysis-SQL-Python-PowerBI-main/customer_behavior_dashboard.pbix) in Power BI Desktop to interact with the visualizations.

---

## Strategic Recommendations

1. **Promote Subscription Perks:** Expand subscriber base by offering free express shipping or early access to sales.
2. **Target High-Value Express Shoppers:** Express shipping users spend 12% more per transaction; tailor premium upsell campaigns for them.
3. **Reward Loyal Customers:** Develop a structured loyalty program targeting the `Returning` segment to transition them into `Loyal` buyers.
4. **Optimize Discount Margins:** Rationalize discount strategies on low-margin products while retaining targeted promos for high spenders.

---

## Author & Contact

**Rajdeep Bose**  
*Data Analyst & Machine Learning Enthusiast*  
GitHub: [rajdeepbosedgp](https://github.com/rajdeepbosedgp)
