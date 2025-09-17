📊 SQL Data Analysis Repository

Welcome to my SQL Data Analysis repository! 🚀 This project showcases my expertise in SQL, from basic to advanced techniques, for core data analysis tasks. It covers data cleaning, EDA, handling duplicates, NULLs, updates, CTEs, window functions, and optimization. Perfect for data analyst roles, it demonstrates my ability to transform large datasets into actionable insights. Explore below! 🔍



📋 Table of Contents





🧹 Data Cleaning



🔎 Finding Duplicates



✏️ Updating Data



🛠️ Handling NULL Values



📈 Exploratory Data Analysis (EDA)



🗂️ Common Table Expressions (CTEs)



📅 Window Functions



⚡ Query Optimization



🧹 Data Cleaning

Cleaning ensures data quality by addressing inconsistencies and errors.

Example: Standardize text by trimming spaces.

SELECT TRIM(customer_name) AS cleaned_name, customer_id
FROM customers;

Output:







cleaned_name



customer_id





John Doe



101





Jane Smith



102



🔎 Finding Duplicates

Identifying duplicates ensures data integrity by detecting repeated records.

Example: Find duplicate emails in a customer table.

SELECT email, COUNT(*) AS count
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;

Output:







email



count





john.doe@email.com



2





jane.smith@email.com



2



✏️ Updating Data

Updating corrects or modifies data to maintain accuracy.

Example: Update missing region values to 'Unknown'.

UPDATE customers
SET region = 'Unknown'
WHERE region IS NULL;

Output (after update):







customer_id



region





101



Unknown





102



West



🛠️ Handling NULL Values

NULL handling replaces or manages missing data for analysis.

Example: Replace NULL sales amounts with 0.

SELECT customer_id, COALESCE(amount, 0) AS amount
FROM sales;

Output:







customer_id



amount





101



500





102



0



📈 Exploratory Data Analysis (EDA)

EDA uncovers patterns using aggregations.

Example: Calculate total sales by region.

SELECT region, SUM(amount) AS total_sales
FROM sales
GROUP BY region
ORDER BY total_sales DESC;

Output:







region



total_sales





West



15000





East



12000



🗂️ Common Table Expressions (CTEs)

CTEs simplify complex queries with temporary result sets.

Example: Find customers with multiple orders.

WITH repeat_customers AS (
  SELECT customer_id, COUNT(*) AS order_count
  FROM orders
  GROUP BY customer_id
  HAVING COUNT(*) > 1
)
SELECT customer_id, order_count
FROM repeat_customers
ORDER BY order_count DESC;

Output:







customer_id



order_count





101



5





103



3



📅 Window Functions

Window functions calculate across rows without collapsing data.

Example: Rank employees by salary within departments.

SELECT employee_id, department, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS salary_rank
FROM employees;

Output:







employee_id



department



salary



salary_rank





1



Sales



80000



1





2



Sales



75000



2





3



IT



90000



1



⚡ Query Optimization

Optimized queries improve performance for large datasets.

Example: Filter sales data efficiently.

SELECT customer_id, amount
FROM sales
WHERE order_date >= '2023-01-01'
AND region = 'West';
-- Index on order_date, region recommended

Output:







customer_id



amount





101



500





104



700





