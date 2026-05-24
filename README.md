# Pizza-sales-analytics-dashboard



A business intelligence project analyzing pizza sales data for fiscal year 2015.  
This report highlights key revenue metrics, demand trends, product performance, and actionable recommendations for operational improvement.

## Project Overview

This project presents an executive-level summary of pizza sales performance using historical transaction data.  
The analysis focuses on revenue, order volume, customer purchasing patterns, product categories, pizza sizes, and best/worst-selling items.

## Key Metrics

- **Total Revenue:** $817,860
- **Average Order Value:** $38.31
- **Total Pizzas Sold:** 49,574
- **Total Orders:** 21,350
- **Average Pizzas per Order:** 2.32

## Insights

### Demand Trends
- Friday recorded the highest number of orders.
- Sunday had the lowest order volume.
- Demand peaks during:
  - **Lunch rush:** 12:00 PM – 1:00 PM
  - **Evening rush:** 5:00 PM – 8:00 PM

### Product Category Performance
- **Classic** pizzas led total sales volume.
- **Supreme** and **Chicken** followed closely.
- **Veggie** pizzas also maintained a strong share of sales.

### Size Performance
- **Large (L)** pizzas generated the highest revenue share.
- Medium and Regular sizes contributed moderate shares.
- X-Large and XXL sizes had very low revenue contribution.

### Best and Worst Sellers
- **Top seller:** The Classic Deluxe Pizza
- **Lowest seller:** The Brie Carre Pizza

## Strategic Recommendations

- Align staffing with lunch and evening peak hours.
- Improve inventory planning for high-demand pizza categories and large sizes.
- Review underperforming menu items for possible removal or redesign.
- Run promotions on Sundays and early weekdays to increase off-peak sales.

## Project Files

- `PIZZA_SALES.pdf` — Executive pizza sales performance report

## Tools Used

- Data analysis and reporting
- Business performance summary
- Dashboard-style executive insights

## SQL Queries used in this project 


select * from pizza_sales


select sum(total_price) AS Total_Revenue from pizza_sales


select * from pizza_sales

select sum(total_price) / count(distinct order_id) as Avg_Order_Value from pizza_sales


select sum(quantity) as Total_Pizza_Sold from pizza_sales

select count(distinct order_id) as Total_Orders from pizza_sales

select cast(sum(quantity) AS DECIMAL(10,2)) / count(distinct order_id) as Avg_Pizzas_Per_Order from pizza_sales

--Daily Trend

SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)


--Hourly Trend

SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as total_orders
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)


SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category



SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size


SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC


SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC


SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC


SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
WHERE MONTH(order_date) = 1
GROUP BY DATENAME(DW, order_date)


SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
WHERE DATEPART(QUARTER, order_date) = 1
GROUP BY DATENAME(DW, order_date)




## Dashboard 


<img width="1550" height="859" alt="image" src="https://github.com/user-attachments/assets/022810d4-1710-485d-a5ea-a21f38a30dde" />

