# Task 6 - Sales Trend Analysis Using SQL Aggregations

## Internship
Data Analyst Internship

---

# Objective

The objective of this task was to analyze sales performance using SQL aggregate functions and grouping techniques. The analysis focused on identifying monthly revenue trends, order volume, regional performance, and product category sales.

---

# Dataset Used

**Online Sales Data.csv**

The dataset contains sales transaction records with the following attributes:

- Transaction ID
- Order Date
- Product Category
- Product Name
- Units Sold
- Unit Price
- Total Revenue
- Region
- Payment Method

---

# Tools Used

- PostgreSQL
- pgAdmin 4
- SQL
- GitHub

---

# Database Creation

A new database was created:

```sql
CREATE DATABASE sales_analysis;
```

A table named `online_sales` was created to store the sales records.

```sql
CREATE TABLE online_sales (
    transaction_id INT,
    order_date DATE,
    product_category VARCHAR(100),
    product_name VARCHAR(200),
    units_sold INT,
    unit_price NUMERIC(10,2),
    total_revenue NUMERIC(12,2),
    region VARCHAR(100),
    payment_method VARCHAR(50)
);
```

---

# Data Import

The CSV dataset was imported into PostgreSQL using pgAdmin Import/Export functionality.

Steps followed:

1. Created the table.
2. Opened Import/Export Data.
3. Selected Import mode.
4. Chose the CSV file.
5. Enabled Header option.
6. Imported the dataset successfully.

---

# SQL Queries Performed

## 1. Total Revenue

```sql
SELECT
SUM(total_revenue) AS total_sales
FROM online_sales;
```

### Purpose

Calculates overall revenue generated from all sales transactions.

---

## 2. Total Orders

```sql
SELECT
COUNT(*) AS total_orders
FROM online_sales;
```

### Purpose

Calculates the total number of sales transactions.

---

## 3. Monthly Revenue Analysis

```sql
SELECT
EXTRACT(MONTH FROM order_date) AS month,
SUM(total_revenue) AS monthly_revenue
FROM online_sales
GROUP BY month
ORDER BY month;
```

### Purpose

Analyzes revenue generated each month.

---

## 4. Monthly Order Volume

```sql
SELECT
EXTRACT(MONTH FROM order_date) AS month,
COUNT(DISTINCT transaction_id) AS order_volume
FROM online_sales
GROUP BY month
ORDER BY month;
```

### Purpose

Measures monthly sales activity.

---

## 5. Monthly Revenue and Order Volume

```sql
SELECT
EXTRACT(YEAR FROM order_date) AS year,
EXTRACT(MONTH FROM order_date) AS month,
SUM(total_revenue) AS monthly_revenue,
COUNT(DISTINCT transaction_id) AS order_volume
FROM online_sales
GROUP BY year, month
ORDER BY year, month;
```

### Purpose

Provides a complete monthly sales trend analysis.

---

## 6. Revenue by Product Category

```sql
SELECT
product_category,
SUM(total_revenue) AS revenue
FROM online_sales
GROUP BY product_category
ORDER BY revenue DESC;
```

### Purpose

Identifies the highest-performing product categories.

---

## 7. Revenue by Region

```sql
SELECT
region,
SUM(total_revenue) AS revenue
FROM online_sales
GROUP BY region
ORDER BY revenue DESC;
```

### Purpose

Compares sales performance across regions.

---

## 8. Top 3 Months by Sales

```sql
SELECT
EXTRACT(MONTH FROM order_date) AS month,
SUM(total_revenue) AS revenue
FROM online_sales
GROUP BY month
ORDER BY revenue DESC
LIMIT 3;
```

### Purpose

Identifies the three best-performing sales months.

---

# SQL Concepts Used

- SELECT
- SUM()
- COUNT()
- COUNT(DISTINCT)
- GROUP BY
- ORDER BY
- LIMIT
- EXTRACT()
- Aggregate Functions

---

# Key Findings

- Monthly revenue trends were identified successfully.
- Order volume was calculated for each month.
- Product categories were ranked based on revenue.
- Regional sales performance was analyzed.
- Top-performing months were identified using aggregate functions.
- SQL grouping techniques enabled trend analysis and business reporting.

---

# Skills Learned

- SQL Query Writing
- Aggregate Functions
- Data Grouping
- Time-Series Analysis
- Revenue Analysis
- PostgreSQL
- Business Reporting

---

# Outcome

Successfully performed sales trend analysis using SQL aggregate functions and grouping techniques. The analysis provided insights into revenue patterns, order volume, category performance, and regional sales trends.

---

# Files Included

- Online Sales Data.csv
- task6.sql
- Query Results Screenshots
- README.md

---

# Interview Questions Covered

1. How do you group data by month and year?
2. Difference between COUNT(*) and COUNT(DISTINCT)?
3. How do you calculate monthly revenue?
4. What are aggregate functions?
5. How are NULL values handled in aggregates?
6. Difference between ORDER BY and GROUP BY?
7. How do you get the top 3 months by sales?

---

# Author

**Pavan Kalyan**

Data Analyst Intern