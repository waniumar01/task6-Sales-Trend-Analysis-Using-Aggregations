# Monthly Sales Trend Analysis (SQL)

## Objective
Analyze monthly revenue and order volume to identify sales trends using SQL aggregation and date functions.

## Dataset
Table: `orders`  
Columns:
- `order_id`
- `order_date`
- `amount`
- `product_id`

## Steps Performed in SQL

1. Extracted year and month from `order_date` using the `EXTRACT()` function to enable month-wise analysis.

2. Filtered the dataset to include orders only from the 2024 calendar year using a `WHERE` clause.

3. Calculated total monthly revenue using the `SUM()` aggregation function on the `amount` column.

4. Calculated monthly order volume using `COUNT(DISTINCT order_id)` to avoid duplicate order counts.

5. Grouped the data by extracted year and month to aggregate results at a monthly level.

6. Sorted the output chronologically using `ORDER BY` for clear trend analysis.

7. Limited the results to 12 rows to display one full year of data.

## SQL Query Used

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS order_year,
    EXTRACT(MONTH FROM order_date) AS order_month,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS total_orders
FROM orders
WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31'
GROUP BY
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY
    order_year,
    order_month
LIMIT 12;
