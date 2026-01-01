# Customer Shopping Behavior Analysis

## Project Overview
This project focuses on analyzing customer purchasing patterns, segmentation, and revenue contribution using a dataset of consumer transactions. By leveraging Python for data processing, SQL for advanced querying, and Power BI for visualization, this project translates raw shopping data into actionable retail insights.

The goal is to understand how demographics (age, gender), subscription status, and shipping methods influence spending habits and product preferences.

## Project Structure
The repository contains the following core components:

* **Data Processing & ETL**
    * `CustomerShoppingBehavior.ipynb`: A Jupyter Notebook that loads the raw dataset using `pandas`, performs initial cleaning, and uses `SQLAlchemy` to migrate the data into a MySQL database for further analysis.
* **Database Engineering**
    * `customer_behavior.sql`: A comprehensive SQL script containing analytical queries designed to segment customers, calculate discount rates, and rank product categories by revenue.
* **Visualization**
    * `Customer Behavior Dashboard.pbix`: An interactive Power BI dashboard providing a high-level view of KPIs, including total revenue by gender, subscription impact, and shipping efficiency.

## Analytical Deep Dive
The project utilizes SQL to answer complex business questions, including:
1.  **Customer Segmentation**: Categorizing shoppers into *New*, *Returning*, and *Loyal* based on purchase history.
2.  **Revenue Analysis**: Comparing the lifetime value (LTV) and average spend of subscribers vs. non-subscribers.
3.  **Product Intelligence**: Ranking the top 3 most-purchased products within each category using window functions.
4.  **Discount Impact**: Identifying which product categories have the highest percentage of discounted sales to evaluate promotional effectiveness.



## SQL Logic Examples
The following logic illustrates how the project handles data categorization:

```sql
-- Segmenting customers based on purchase frequency
WITH customer_type AS (
    SELECT customer_id, previous_purchases,
    CASE 
        WHEN previous_purchases = 1 THEN 'New'
        WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
        ELSE 'Loyal'
    END AS customer_segment
    FROM customer
)
SELECT customer_segment, COUNT(*) AS "Number of Customers" 
FROM customer_type 
GROUP BY customer_segment;
