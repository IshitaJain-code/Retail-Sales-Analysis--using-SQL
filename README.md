# 🛒 Retail Sales Analysis Using SQL

This project explores a retail sales dataset using SQL to answer real-world business questions related to customer behavior, product performance, and sales trends.

The goal of this project is to demonstrate practical SQL skills such as:

- Data cleaning
- Aggregations
- Filtering
- Common Table Expressions (CTEs)
- Window Functions
- Date and Time Functions
- Business-focused analysis

---

## 📂 Dataset Overview

The dataset contains retail transaction records with the following fields:

- `transactions_id`
- `sale_date`
- `sale_time`
- `customer_id`
- `gender`
- `age`
- `category`
- `quantiy`
- `price_per_unit`
- `cogs`
- `total_sale`

---

## 🛠️ Database Schema

```sql
CREATE TABLE retail_sale (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantiy INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
````

---

## 🧹 Data Cleaning

### Check for Null Values

```sql
SELECT *
FROM retail_sale
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantiy IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

### Remove Null Records

```sql
DELETE FROM retail_sale
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantiy IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

---

## 📊 Exploratory Analysis

### Total Number of Sales

```sql
SELECT COUNT(*) AS total_sales
FROM retail_sale;
```

### Total Unique Customers

```sql
SELECT COUNT(DISTINCT customer_id) AS total_customer
FROM retail_sale;
```

### Product Categories

```sql
SELECT DISTINCT category
FROM retail_sale;
```

---

# 📈 Business Questions and SQL Solutions

---

## Q1. Retrieve all sales made on `2022-11-05`

```sql
SELECT *
FROM retail_sale
WHERE sale_date = '2022-11-05';
```

---

## Q2. Retrieve Clothing transactions with quantity sold more than 4 in November 2022

```sql
SELECT *
FROM retail_sale
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantiy >= 4;
```

---

## Q3. Calculate total sales for each category

```sql
SELECT
    category,
    SUM(total_sale) AS net_sale
FROM retail_sale
GROUP BY category;
```

---

## Q4. Find the average age of customers who purchased Beauty products

```sql
SELECT
    ROUND(AVG(age), 2) AS avg_age
FROM retail_sale
WHERE category = 'Beauty';
```

---

## Q5. Find all transactions where total sales exceeded 1000

```sql
SELECT *
FROM retail_sale
WHERE total_sale > 1000;
```

---

## Q6. Find the total number of transactions by gender in each category

```sql
SELECT
    category,
    gender,
    COUNT(*) AS total_number_of_transaction
FROM retail_sale
GROUP BY category, gender
ORDER BY category;
```

---

## Q7. Find the best-selling month in each year based on average sales

```sql
SELECT
    year,
    month,
    avg_sale
FROM (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sale
    GROUP BY 1, 2
) AS t1
WHERE rank = 1;
```

---

## Q8. Find the top 5 customers based on total sales

```sql
SELECT
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sale
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

---

## Q9. Find the number of unique customers who purchased from each category

```sql
SELECT
    category,
    COUNT(DISTINCT customer_id) AS unique_customer
FROM retail_sale
GROUP BY category;
```

---

## Q10. Create sales shifts and count the number of orders in each shift

* Morning: Before 12 PM
* Afternoon: 12 PM to 5 PM
* Evening: After 5 PM

```sql
WITH hourly_sales AS (
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sale
)
SELECT
    shift,
    COUNT(*) AS total_orders
FROM hourly_sales
GROUP BY shift;
```

---

# 🧠 Key SQL Concepts Used

* `SELECT`, `WHERE`, `ORDER BY`
* `GROUP BY`
* `COUNT()`, `SUM()`, `AVG()`
* `DISTINCT`
* `CASE WHEN`
* `CTE (WITH clause)`
* `Window Functions (RANK())`
* `EXTRACT()`
* `TO_CHAR()`

---

# 📌 Key Business Insights Generated

This analysis helps answer questions such as:

* Which product categories generate the highest revenue?
* Which customers contribute the most to sales?
* Which month performs best each year?
* How does purchasing behavior vary by gender?
* What time of day sees the highest number of orders?

---

# 🚀 Tools Used

* PostgreSQL
* SQL
* GitHub

---

# 📁 Project Structure

```text
retail-sales-sql-analysis/
│── sql_query_project.sql
│── README.md
```

---

# 🎯 Project Objective

The purpose of this project is to strengthen SQL skills by solving practical business problems using a real-world retail dataset.

This project is ideal for aspiring Data Analysts who want to demonstrate proficiency in SQL and business analysis.

---
Connect with me on
 [LinkedIn] https://www.linkedin.com/in/ishita-jain-5a178a3b0?

```

---





