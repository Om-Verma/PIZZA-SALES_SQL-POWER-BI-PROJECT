# PIZZA-SALES_SQL-POWER-BI-PROJECT
Created Power BI dashboard and ran SQL Queries to verify the data shown on dashboard



--FOLLOWING SQL QUERIES WERE IMPLEMENTED
--A: KPIs

1: Total Revenue:

SELECT SUM(total_price) as Total_Revenue from pizza_sales;




2: Average Order Value:


SELECT SUM(total_price)/COUNT(distinct(order_id)) as 'Avg_Order_Value' from pizza_sales;

3: Total pizzas sold

SELECT SUM(quantity) as 'Total_Pizza_Sold' from pizza_sales;

4: Total Orders

SELECT COUNT(DISTINCT(order_id)) AS 'Total Orders' FROM pizza_sales;




5. Average order value:

SELECT SUM(total_price)/ COUNT(DISTINCT ORDER_id) as 'avg order value' from pizza_sales



6. Total pizzas sold:

SELECT SUM(quantity) as 'Total pizzas sold' from pizza_sales


7. Average pizzas per order

SELECT CAST(
CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(distinct order_id) AS DECIMAL(10,2)) 
as decimal(10,2)) 
as 'AVG_PIZZAS_PER_ORDER'
from pizza_sales;




8. Daily trends for total orders:

select DATENAME(DW,order_date) as order_day, 
count(DISTINCT order_id) as Total_orders
from pizza_sales
group by DATENAME(DW,order_date);







9. Monthly trends for total orders:

select DATENAME(MONTH,order_date) as Month_Name, 
count(DISTINCT order_id) as Total_orders
from pizza_sales
group by DATENAME(MONTH,order_date);



For descending order:

select DATENAME(MONTH,order_date) as Month_Name, 
count(DISTINCT order_id) as Total_orders
from pizza_sales
group by DATENAME(MONTH,order_date)
Order by total_orders DESC;
10: % of sales by pizza category:

SELECT Pizza_Category , 
sum(total_price) as total_sales,
sum(total_price)*100/(SELECT sum(total_price) from pizza_sales) as '% total sales'
from pizza_sales
group by pizza_category;




applying the where clause to get the monthly data:
SELECT Pizza_Category , 
sum(total_price) as total_sales,
sum(total_price)*100/(SELECT sum(total_price) from pizza_sales where MONTH(order_date)=1) as '% total sales' 
from pizza_sales
where MONTH(order_date)=1
group by pizza_category;


–Note: month (order_date)=1 means january














11.  Percentage sales by pizza size: (WHERE clause for selecting quarter)

SELECT Pizza_size , 
cast(sum(total_price) as decimal (10,3)) as total_sales ,
cast(sum(total_price)*100/
    (SELECT sum(total_price) from pizza_sales) as decimal(10,3)) as PCT
from pizza_sales
where DATEPART(quarter,order_date)=1
group by pizza_size
order by PCT desc;




12: top 5 pizza by total revenue:

SELECT TOP 5 pizza_name, sum(total_price) AS Total_Revenue 
from pizza_sales
group by pizza_name
ORDER BY Total_Revenue desc;






13: top 5 pizza by total quantity :

SELECT TOP 5 pizza_name, sum(quantity) AS Total_Quantity 
from pizza_sales
group by pizza_name
ORDER BY Total_Quantity  desc;


14: top 5 pizza by total_orders :

SELECT TOP 5 pizza_name, sum(quantity) AS Total_Quantity 
from pizza_sales
group by pizza_name
ORDER BY Total_Quantity  desc;


