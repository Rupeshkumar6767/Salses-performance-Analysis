# 📊 Customer Sales Analysis

## 📌 Project Overview
The **Customer Sales Analysis** project focuses on analyzing customer purchasing behavior, sales trends, revenue generation, and customer segmentation using data-driven insights. 

By leveraging **SQL, Python, Excel, and Power BI**, this project helps businesses comprehensively understand customer spending patterns, product performance, discount effectiveness, and subscription behavior to optimize revenue strategies.

---

## 🎯 Project Objectives
* **Analyze** customer purchase behavior and demographic spending patterns.
* **Compare** revenue distribution by gender and age groups.
* **Identify** top-rated products and most frequently purchased items.
* **Study** the direct impact of discounts and subscription statuses on overall sales volume.
* **Segment** customers dynamically based on their lifetime purchasing history.
* **Design** and deploy an interactive, executive-ready dashboard using Power BI.

---

## 🛠️ Tech Stack & Tools

| Tool / Technology | Purpose |
|:---|:---|
| **MySQL** | Advanced data querying, aggregation, and analytical window functions |
| **Python (3.x)** | Exploratory Data Analysis (EDA), data cleaning, and preprocessing |
| **Pandas & NumPy** | High-performance data manipulation and numerical analysis |
| **Matplotlib & Seaborn** | Statistical data visualization and plotting |
| **Power BI** | Interactive dashboard creation, DAX modeling, and visual reporting |
| **Excel** | Initial dataset inspection and structure handling |
| **Jupyter Notebook** | Documented Python execution environment |

---

## 📂 Dataset Architecture

The underlying dataset captures comprehensive transaction logs with the following schema:

| Column Name | Data Type | Description |
|:---|:---|:---|
| `Customer ID` | Integer | Unique identifier for each customer |
| `Age` | Integer | Age of the customer |
| `Gender` | String | Demographic gender (Male/Female) |
| `Item Purchased` | String | Name of the purchased product |
| `Category` | String | Product classification category |
| `Purchase Amount` | Float/Decimal | Total fiat amount spent on the transaction |
| `Review Rating` | Float | Product review rating scaled from 1.0 to 5.0 |
| `Subscription Status` | String | Indicates membership status (Yes/No) |
| `Shipping Type` | String | Selected logistics/delivery method |
| `Discount Applied` | String | Indicates if a promotional discount code was used |
| `Previous Purchases` | Integer | Historical count of orders placed by the customer |
| `Payment Method` | String | Transaction medium used (e.g., Card, Cash, UPI) |

---

## 🗄️ SQL Analysis & Queries

### 1. Total Revenue Generation by Gender
```sql
SELECT 
    gender, 
    SUM(purchase_amount) AS total_revenue
FROM customer
GROUP BY gender;
```

### 2. High-Value Customers Utilizing Discounts
*Filters for customers who applied a discount code but still spent above the global average transaction size.*
```sql
SELECT 
    customer_id, 
    purchase_amount
FROM customer
WHERE discount_applied = 'Yes'
  AND purchase_amount >= (
      SELECT AVG(purchase_amount) 
      FROM customer
  );
```

### 3. Top 5 Highest Rated Products
```sql
SELECT 
    item_purchased,
    AVG(review_rating) AS average_rating
FROM customer
GROUP BY item_purchased
ORDER BY average_rating DESC
LIMIT 5;
```

### 4. Standard vs Express Shipping Financial Metrics
```sql
SELECT 
    shipping_type,
    ROUND(AVG(purchase_amount), 2) AS avg_purchase
FROM customer
WHERE shipping_type IN ('standard', 'express')
GROUP BY shipping_type;
```

### 5. Subscription Impact on Sales Metrics
```sql
SELECT 
    subscription_status,
    COUNT(customer_id) AS total_customers,
    ROUND(AVG(purchase_amount), 2) AS avg_spend,
    ROUND(SUM(purchase_amount), 2) AS total_revenue
FROM customer
GROUP BY subscription_status;
```

### 6. Products with Highest Discount Penetration Rate
```sql
SELECT 
    item_purchased,
    ROUND(100.0 * SUM(CASE WHEN discount_applied = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS discount_rate
FROM customer
GROUP BY item_purchased
ORDER BY discount_rate DESC
LIMIT 5;
```

### 7. Advanced Analytical Scripts (Included in Script File)
* **Customer Segmentation:** Cohort categorization into *New*, *Returning*, and *Loyal* buyers based on transaction count.
* **Category Window Functions:** Dynamic ranking (`DENSE_RANK()`) of the most purchased items partitioned by category.
* **Repeat Buyer Behavior:** Correlation matrix checking if historical repeat buyers gravitate towards active subscriptions.
* **Age Group Cohorts:** Generational revenue analysis segmented into discrete age buckets.

---

## 🐍 Python Exploratory Data Analysis (EDA)

Python was deployed to handle automated data pipelines, addressing null values, outlier filtering, and generating static distribution curves.

### Core Libraries
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns # Added for professional styling
```

---

## 📈 Power BI Dashboard Visuals
The business intelligence layer converts abstract numbers into functional executive charts, covering:
* **Sales KPI Blocks:** Total Revenue, Average Order Value (AOV), and Total Transactions.
* **Performance Matrix:** Product category vs revenue yield.
* **Behavioral Segmentation:** Interactive slicing by Subscription Status and Discount Impact.

### 📷 Dashboard Preview
![Dashboard Preview](dashboard.png)

---

## 📁 Repository Structure

| File / Folder Name | Description |
|:---|:---|
| 📄 `customer_sales.sql` | Well-commented SQL scripts containing all analytical queries |
| 📊 `customer_sales.xlsx` | Cleaned transaction source data |
| 📓 `analysis.ipynb` | Comprehensive Jupyter Notebook containing Python EDA and charts |
| 📉 `dashboard.pbix` | Power BI Desktop file with interactive dashboard visuals |
| 🖼️ `dashboard.png` | Static screen capture of the main dashboard viewport |

---

## ▶️ Execution & Deployment Guide

### Phase 1: Database Setup
1. Initialize your local or cloud MySQL instance.
2. Create a target database and import `customer_sales.xlsx` or execute a custom DDL schema setup.
3. Open and run `customer_sales.sql` to verify analytical queries.

### Phase 2: Python Environment Run
1. Ensure Python 3.x and `pip` are locally installed.
2. Initialize requirements via terminal: `pip install pandas numpy matplotlib seaborn`
3. Launch `jupyter notebook` and open `analysis.ipynb` to step through the data workflow.

### Phase 3: Dashboard View
1. Install **Power BI Desktop**.
2. Open `dashboard.pbix`.
3. *(Optional)* Modify the source data connection parameter to point to your updated localized data store and click **Refresh**.

---

## 🚀 Strategic Key Insights
* **Subscription Lift:** Customers with active subscriptions hold a significantly higher Lifetime Value (LTV) and average spend metrics compared to non-subscribers.
* **Promotional Velocity:** Targeted discount campaigns demonstrated a clear positive elasticity curve, successfully moving low-velocity product stock.
* **Demographic Target:** Specific mid-tier age cohorts contributed to the highest net revenue margins, defining the target persona for future marketing spend.

---

## 📌 Future Enhancements
- [ ] Build a predictive machine learning model to calculate Customer Churn Risk.
- [ ] Implement a product Recommendation Engine using collaborative filtering.
- [ ] Transition static processing pipelines into a real-time ETL workflow.

---

## 👨‍💻 Author
**Rupesh Kumar**
* 📧 **Email:** [your.email@example.com](mailto:your.email@example.com)
* 💼 **LinkedIn:** [://linkedin.com](https://://linkedin.com)
* 🐙 **GitHub:** [@yourusername](https://github.com)

---

## ⭐ Support
If this framework helped you analyze retail data or structural templates, please give this repository a ⭐ on GitHub!
