# Monthly Sales Trend Analysis Using SQL

## Objective
Analyze monthly revenue and order volume to identify sales trends using SQL aggregation and date functions.

## Dataset
Database: `online_sales`  
Table: `orders`

Columns used:
- `order_id` – Unique identifier for each order
- `order_date` – Date when the order was placed
- `amount` – Revenue generated per order
- `product_id` – Identifier of the product sold

## Steps Performed in SQL

1. Extracted the year and month from the `order_date` column using the `EXTRACT()` function to enable month-wise analysis.

2. Filtered the dataset to include orders only from a specific time period (2024) using a `WHERE` clause.

3. Calculated total monthly revenue using the `SUM()` aggregation function on the `amount` column.

4. Calculated monthly order volume using `COUNT(DISTINCT order_id)` to ensure each order is counted only once.

5. Grouped the data by extracted year and month to aggregate results at a monthly level.

6. Sorted the results chronologically using `ORDER BY` to clearly display sales trends over time.

7. Limited the output to 12 rows to represent one full year of monthly data.

## SQL Query Used

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS order_year,
    EXTRACT(MONTH FROM order_date) AS order_month,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS total_orders
FROM online_sales.orders
WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31'
GROUP BY
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY
    order_year,
    order_month
LIMIT 12;


