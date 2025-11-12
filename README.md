# SQL-EXCEL_pizzasales
# Pizza Sales Analysis Project

📊 Project Overview
This project analyzes pizza sales data through SQL queries and an interactive Excel dashboard. The analysis provides insights into sales performance, customer behavior, and product popularity to support data-driven business decisions.

## Key Features
- **Data Cleaning & Preparation**: Performed data cleaning on CSV files before importing to Excel
- **SQL Data Analysis**: Wrote complex SQL queries to extract meaningful insights
- **Interactive Excel Dashboard**: Created dynamic visualizations with filters and interactive elements
- **Sales Performance Metrics**: Analyzed revenue, order patterns, and product performance

## 🛠 Technical Skills Demonstrated
- **SQL**: Data querying, aggregation, filtering, and analysis
- **Excel**: Advanced charting, pivot tables, interactive dashboards, data visualization
- **Data Cleaning**: CSV file preparation and validation
- **Data Analysis**: Trend analysis, performance metrics, KPI tracking

## 📈 SQL Queries and Analysis

### Basic Metrics
```sql
-- 1. Total orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;

-- 2. Total revenue
SELECT sum(total_price) AS Total_Revenue FROM pizza_sales;

-- 3. Average pizzas per order
SELECT CAST(CAST(sum(quantity) AS DECIMAL(10,2))/ 
CAST(count(distinct order_id) AS DECIMAL (10,2))AS decimal(10,2)) 
AS Avg_Pizzas_per_Order from pizza_sales;

-- 4. Average order value
SELECT sum(total_price)/ count(DISTINCT order_id) 
AS Average_order_value FROM pizza_sales;
```

### Product Analysis
```sql
-- 5. Total pizza sold by category
select pizza_category, sum(quantity) AS Total_Pizzas_Sold 
from pizza_sales group by pizza_category;

-- 6. Top 5 best-selling pizzas
SELECT pizza_name, sum(quantity) as Total_Pizzas_Sold 
from pizza_sales group by pizza_name 
order by sum(quantity) DESC limit 5;

-- 7. Bottom 5 worst-selling pizzas
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold 
FROM pizza_sales GROUP BY pizza_name 
ORDER BY Total_Pizza_Sold ASC limit 5;
```

### Sales Performance
```sql
-- 8. Sales percentage by size (Q1)
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_Sales, 
CAST( SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales WHERE quarter(order_date)=1) 
AS DECIMAL(10,2) ) AS PCT FROM pizza_sales 
WHERE quarter(order_date)=1 GROUP BY pizza_size ORDER BY PCT DESC;

-- 9. Sales percentage by category (January)
SELECT pizza_category,SUM(total_price) AS total_Sales, 
(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales WHERE MONTH(order_date)=1)) AS PCT 
FROM pizza_sales WHERE MONTH(order_date)=1 GROUP BY pizza_category;
```

### Time-based Analysis
```sql
-- 10. Hourly order trends
SELECT hour(order_time) as order_hours, count(distinct order_id) as total_orders 
from pizza_sales group by hour(order_time) order by hour(order_time);

-- 11. Daily order trends
SELECT DAYNAME(order_date) AS order_day, COUNT(DISTINCT order_id) AS Total_orders 
FROM pizza_sales GROUP BY DAYNAME(order_date);
```

## 📊 Excel Dashboard Features
The interactive Excel dashboard includes:

### Key Metrics Display
- Total Revenue
- Total Orders
- Average Order Value
- Average Pizzas per Order
- Total pizzas sold

### Visualizations
- **% Sales by Category**: doughnut chart showing percentage of revenue distribution across pizza categories
- **Total pizas sold by pizza category**: funnel chart showing number of pizzas sold across pizza categories
- **Top/Bottom Performers**: bar Charts highlighting best and worst-selling pizzas
- **Time-based Trends**:
  - Hourly sales patterns (line chrts)
  - Daily order trends (bar charts)
  - Seasonal performance (Timeline)
- **Size Analysis**: pie chart showing percentage of revenue distribution by pizza size



## Dashboard Screenshot
<img width="936" height="634" alt="dashboard_excel" src="https://github.com/user-attachments/assets/6cb5d363-926c-4953-b9ab-55ab8b904150" />





---

