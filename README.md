# Customer Shopping Behavior Analysis & Business Intelligence Pipeline

An end-to-end data analytics project examining customer shopping behavior, purchasing drivers, and subscription trends across 3,900 retail transactions[cite: 2]. Built with **Python**, **PostgreSQL/MySQL/SQL Server**, **Power BI**, and **Gamma AI**[cite: 1, 10].

---

## 📌 Project Overview

Retail management needed to evaluate shifting purchasing patterns across customer demographics, product categories, and fulfillment methods to uncover what factors drive consumer decisions and repeat purchases[cite: 1].

### Objectives

* Clean, impute, and enrich raw customer transaction data using Python[cite: 1, 2].
* Establish a database pipeline to load data into PostgreSQL (with support for MySQL and MS SQL Server)[cite: 10].
* Run targeted SQL business queries extracting insights on high-value cohorts, discount sensitivity, and loyalty tiers[cite: 1, 2].
* Build a Power BI dashboard tracking revenue, customer segments, and review benchmarks[cite: 1, 8].
* Synthesize actionable business strategies into an executive report and a Gamma presentation deck[cite: 1, 8].

---

## 📂 Dataset Summary

The project analyzes `customer_shopping_behavior.csv`, capturing consumer demographic profiles and transaction-level attributes[cite: 2, 10].

* **Total Records:** 3,900 rows[cite: 2]
* **Attributes:** 18 raw columns[cite: 2]
* **Primary Features:**
* **Demographics:** `Customer ID`, `Age`, `Gender`, `Location`, `Subscription Status`[cite: 2]
* **Transaction Details:** `Item Purchased`, `Category`, `Purchase Amount (USD)`, `Size`, `Color`, `Season`[cite: 2]
* **Behavior & Logistics:** `Review Rating`, `Shipping Type`, `Discount Applied`, `Promo Code Used`, `Previous Purchases`, `Payment Method`, `Frequency of Purchases`[cite: 2]


* **Data Quality Issue:** 37 missing values in the `Review Rating` attribute[cite: 2].

---

## 🛠️ Tools & Technologies

| Category | Tool / Library | Purpose |
| --- | --- | --- |
| **Data Processing & EDA** | Python (`pandas`, `numpy`) | Data profiling, categorical grouping, column standardization, median imputation[cite: 2, 10] |
| **Database Engine** | PostgreSQL (`psycopg2`, `sqlalchemy`) | Relational staging, aggregations, window functions, and cohort segmentation[cite: 2, 10, 12] |
| **Alternative DBs** | MySQL (`pymysql`), MS SQL Server (`pyodbc`) | Multi-database connectivity support[cite: 10] |
| **Data Visualization** | Microsoft Power BI | KPI scorecards, donut distribution charts, sales & revenue category bars, horizontal demographic charts[cite: 8] |
| **Executive Reporting** | Gamma AI & Markdown | Stakeholder slide deck design and executive summary reporting[cite: 1] |

---

## 🔄 Project Workflow

```mermaid
graph LR
    A[📄 Raw CSV: 3,900 Rows] --> B[🐍 Python: EDA, Cleaning & Imputation]
    B --> C[(🗄️ Database: PostgreSQL / MySQL / SQL Server)]
    C --> D[🔍 SQL: 10 Business Transaction Queries]
    D --> E[📊 Power BI: Interactive Dashboard]
    E --> F[📑 Gamma AI: Stakeholder Presentation]

```

### 1. Python Data Cleaning & Feature Engineering

* **Missing Value Imputation:** Imputed missing values in `Review Rating` using the median rating of the respective product category via `groupby('Category')['Review Rating'].transform()`[cite: 2, 10].
* **Column Formatting:** Cleaned names to lowercase snake_case (e.g., `purchase_amount_(usd)` $\rightarrow$ `purchase_amount`)[cite: 2, 10].
* **Redundancy Reduction:** Validated that `discount_applied` and `promo_code_used` were 100% identical; dropped `promo_code_used` to remove redundancy[cite: 2, 10].
* **Feature Engineering:**
* `age_group`: Segmented age into four quantiles: `Young Adult`, `Adult`, `Middle-aged`, and `Senior`[cite: 2, 8, 10].
* `purchase_frequency_days`: Mapped purchase frequencies (`Weekly` = 7, `Fortnightly` = 14, `Monthly` = 30, `Quarterly`/`Every 3 Months` = 90, `Annually` = 365)[cite: 2, 10].


* **Automated Ingestion:** Pushed the prepared dataset to PostgreSQL table `customer` using `sqlalchemy`[cite: 2, 10].

### 2. SQL Analysis & Business Queries

Ten business questions answered in PostgreSQL[cite: 2, 12]:

1. **Gender Revenue:** Male customers contributed $157,890 vs. Female customers at $75,191[cite: 3, 4].
2. **High-Spending Discount Users:** Identified 839 customers who used a discount but still spent above the $59.76 store average[cite: 2, 4].
3. **Top-Rated Products:** Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), and Skirt (3.78) received the highest average ratings[cite: 5].
4. **Shipping Value Comparison:** Express shipping orders averaged slightly higher ($60.48) than Standard shipping ($58.46)[cite: 5].
5. **Subscription Financials:** 1,053 subscribers generated $62,645 ($59.49 avg spend); 2,847 non-subscribers generated $170,436 ($59.87 avg spend)[cite: 5].
6. **Discount-Reliant Inventory:** Hat (50.00%), Sneakers (49.66%), Coat (49.07%), Sweater (48.17%), and Pants (47.37%) had the highest percentage of discounted purchases[cite: 6].
7. **Customer Loyalty Tiers:** Segmented purchase history into Loyal (3,116 customers), Returning (701 customers), and New (83 customers)[cite: 6].
8. **Top 3 Products by Category:** Ranked using `ROW_NUMBER() OVER (PARTITION BY category ORDER BY count DESC)`:
* *Accessories:* Jewelry (171), Sunglasses (161), Belt (161)[cite: 7].
* *Clothing:* Blouse (171), Pants (171), Shirt (169)[cite: 7].
* *Footwear:* Sandals (160), Shoes (150), Sneakers (145)[cite: 7].
* *Outerwear:* Jacket (163), Coat (161)[cite: 7].


9. **Repeat Buyer Subscriptions:** Among customers with >5 previous purchases, 2,518 were non-subscribers and 958 were subscribers[cite: 7].
10. **Revenue by Age Group:** Young Adults led total spend at $62,143, followed by Middle-aged ($59,197), Adults ($55,978), and Seniors ($55,763)[cite: 8].

---

## 📊 Power BI Dashboard

The interactive Power BI dashboard provides an executive overview of core performance metrics[cite: 1, 8]:

* **Top KPIs:** Total Customers (3.9K) | Average Purchase Amount ($59.76) | Average Review Rating (3.75)[cite: 8].
* **Subscription Breakdown:** Donut visual indicating 27% Subscribed vs. 73% Non-Subscribed customers[cite: 8].
* **Category Performance:** Revenue and Sales volume by Category (`Clothing` leading, followed by `Accessories`, `Footwear`, and `Outerwear`)[cite: 2, 8].
* **Age Demographics:** Horizontal bar charts displaying Revenue and Order Volume across `Young Adult`, `Middle-aged`, `Adult`, and `Senior` tiers[cite: 8].
* **Interactive Slicers:** Filters for `Subscription Status`, `Gender`, `Category`, and `Shipping Type`[cite: 8].

---

## 📈 Key Business Recommendations

* **Revamp Subscription Perks:** Subscribers average nearly identical order values ($59.49) to non-subscribers ($59.87)[cite: 5]. Offer subscriber-only bundles, early access drops, and free shipping thresholds to increase basket sizes[cite: 8].
* **Capitalize on Repeat Non-Subscribers:** 2,518 customers with >5 previous orders do not subscribe[cite: 7]. Target this high-intent segment with introductory membership promotions[cite: 8].
* **Protect Margins on Discount-Sensitive Goods:** Five staple products (Hats, Sneakers, Coats, Sweaters, Pants) have ~50% discount dependency[cite: 6]. Adjust discount thresholds toward minimum cart minimums rather than flat markdowns[cite: 9].
* **Spotlight Top-Rated Inventory:** Feature top-rated products (Gloves, Sandals, Boots) across digital and email marketing campaigns to drive conversion[cite: 5, 9].

---

## 🗂️ Repository Structure

```text
├── data/
│   ├── customer_shopping_behavior.csv    # Raw transaction data (3,900 rows)
│   └── cleaned_customer_behavior.csv     # Cleaned and engineered dataset
├── notebooks/
│   └── customer_behavior_eda.ipynb       # Pandas EDA, imputation, and DB loader
├── sql/
│   └── customer_behavior_queries.sql     # 10 PostgreSQL analytical queries
├── powerbi/
│   └── customer_behavior_dashboard.pbix  # Power BI dashboard file
├── presentation/
│   ├── Business_Problem_Document.pdf     # Scope and business problem statement
│   └── Customer_Shopping_Behavior_Deck.pdf # Gamma AI executive presentation
├── README.md
└── requirements.txt

```

---

## 🚀 How to Run

### 1. Clone & Set Up Environment

```bash
git clone https://github.com/[your-username]/customer-shopping-behavior-analysis.git
cd customer-shopping-behavior-analysis
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

```

*Required packages:* `pandas`, `sqlalchemy`, `psycopg2-binary` (or `pymysql` / `pyodbc`)[cite: 10].

### 2. Run Cleaning & Database Ingestion

Run the Jupyter notebook `notebooks/customer_behavior_eda.ipynb`[cite: 10]. Configure your database credentials in the connection block:

```python
from sqlalchemy import create_engine

# Example: PostgreSQL connection
engine = create_engine("postgresql+psycopg2://postgres:your_password@localhost:5432/customer_behavior")
df.to_sql("customer", engine, if_exists="replace", index=False)

```

### 3. Run SQL Queries

Open your SQL client (e.g., pgAdmin, DBeaver) and run `sql/customer_behavior_queries.sql` against the loaded `customer` table to reproduce all metrics[cite: 10, 12].

### 4. View Dashboard

Open `powerbi/customer_behavior_dashboard.pbix` in Microsoft Power BI Desktop to inspect the visualizations, data model, and slicers[cite: 8].

---

## 👤 Author

* **Project Analyst:** `Piyush Jadhav`
* **LinkedIn:** `https://www.linkedin.com/in/piyush-jadhav-97359a2bb/`
* **Portfolio / GitHub:** `https://github.com/piyush-x`
