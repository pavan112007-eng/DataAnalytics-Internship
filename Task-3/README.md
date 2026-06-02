# Task 3 - SQL for Data Analysis

## Internship
Data Analyst Internship

---

# Objective

The objective of this task was to use SQL queries to extract, manipulate, and analyze structured data from an e-commerce dataset using PostgreSQL. The task focused on applying SQL concepts such as filtering, sorting, aggregation, joins, subqueries, views, and query optimization.

---

# Dataset Used

**Olist Customers Dataset** (`olist_customers_dataset.csv`)

The dataset contains customer-related information including:

- Customer ID
- Customer Unique ID
- ZIP Code Prefix
- Customer City
- Customer State

---

# Tools Used

- PostgreSQL
- pgAdmin 4
- SQL
- GitHub

---

# Database Setup

### Created Database

```sql
CREATE DATABASE ecommerce_db;
```

### Created Customers Table

```sql
CREATE TABLE customers (
    customer_id VARCHAR(50),
    customer_unique_id VARCHAR(50),
    customer_zip_code_prefix INT,
    customer_city VARCHAR(100),
    customer_state VARCHAR(10)
);
```

### Imported Dataset

Imported the CSV dataset into PostgreSQL using pgAdmin's Import/Export feature.

---

# SQL Operations Performed

## 1. SELECT Queries

Retrieved all records and specific columns from the dataset.

```sql
SELECT * FROM customers;
```

---

## 2. WHERE Clause

Filtered records based on specific conditions.

```sql
SELECT *
FROM customers
WHERE customer_state = 'SP';
```

---

## 3. ORDER BY

Sorted records in ascending and descending order.

```sql
SELECT *
FROM customers
ORDER BY customer_city;
```

---

## 4. GROUP BY

Grouped data to perform analysis on customer counts by state.

```sql
SELECT customer_state,
       COUNT(*) AS total_customers
FROM customers
GROUP BY customer_state;
```

---

## 5. Aggregate Functions

Used:

- COUNT()
- AVG()
- MAX()
- MIN()

Example:

```sql
SELECT COUNT(*) AS total_customers
FROM customers;
```

---

## 6. HAVING Clause

Filtered grouped data using aggregate conditions.

```sql
SELECT customer_state,
       COUNT(*) AS total_customers
FROM customers
GROUP BY customer_state
HAVING COUNT(*) > 1000;
```

---

## 7. Subqueries

Used nested queries for advanced data retrieval.

```sql
SELECT *
FROM customers
WHERE customer_state =
(
    SELECT customer_state
    FROM customers
    GROUP BY customer_state
    ORDER BY COUNT(*) DESC
    LIMIT 1
);
```

---

## 8. Views

Created a view for state-wise customer analysis.

```sql
CREATE VIEW state_customer_count AS
SELECT customer_state,
       COUNT(*) AS total_customers
FROM customers
GROUP BY customer_state;
```

---

## 9. Index Creation

Created indexes to improve query performance.

```sql
CREATE INDEX idx_state
ON customers(customer_state);
```

---

## 10. Joins

Created an additional table to demonstrate SQL joins.

### INNER JOIN

```sql
SELECT c.customer_city,
       c.customer_state,
       s.region
FROM customers c
INNER JOIN states s
ON c.customer_state = s.state_code;
```

### LEFT JOIN

```sql
SELECT c.customer_city,
       c.customer_state,
       s.region
FROM customers c
LEFT JOIN states s
ON c.customer_state = s.state_code;
```

### RIGHT JOIN

```sql
SELECT c.customer_city,
       c.customer_state,
       s.region
FROM customers c
RIGHT JOIN states s
ON c.customer_state = s.state_code;
```

---

# Key Learnings

Through this task, the following concepts were learned:

- SQL Fundamentals
- Data Retrieval using SELECT
- Data Filtering using WHERE
- Data Sorting using ORDER BY
- Grouping Data using GROUP BY
- Aggregate Functions
- HAVING Clause
- Subqueries
- SQL Views
- Indexing
- INNER JOIN, LEFT JOIN, and RIGHT JOIN

---

# Outcome

Successfully used SQL to analyze and manipulate structured e-commerce customer data. Developed practical experience in writing queries, performing data analysis, creating views, using joins, and optimizing database performance.

---

# Files Included

- olist_customers_dataset.csv
- task3.sql
- Query Output Screenshots
- README.md

---

# Author

**Pavan Kalyan**

Data Analyst Intern