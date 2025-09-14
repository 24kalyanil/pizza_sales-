create database pizza_pro;
use pizza_pro;
select * from pizza_sales;

select* from pizza_sales order by pizza_id;

select sum(total_price)as total_revenue from pizza_sales;

select sum(total_price) / count(distinct order_id ) from pizza_sales;

select sum(total_price)/ count(distinct order_id)as avg_order_value from pizza_sales;

select sum(quantity) as toal_pizza_sold from pizza_sales;

select count(distinct order_id) as total_orders from pizza_sales;

SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 

CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))

AS Avg_Pizzas_per_order

FROM pizza_sales;

## HOURLY TRENDS FOR ORDERS ##
SELECT hour(order_time)as order_hours, sum(quantity) as total_pizza_sold from pizza_sales group by
hour(order_time) order by hour(order_time);

## % of Sales by Pizza Category ##
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;

## % of Sales by Pizza Size ##
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;

## Total Pizzas Sold by Pizza Category ##
 select pizza_category,sum(quantity) as total_pizza_sold 
 from pizza_sales
 group by pizza_category;
 
 ## Top 5 Best Sellers by Total Pizzas Sold ##
 select top5  pizza_name, sum(quantity)as total_pizzas_sold
 from pizza_sales
 group by pizza_name 
 order by sum(quantity) desc;

## Bottom 10 Best Sellers by Total Pizzas Sold##
select TOP10 pizza_name, sum(quantity)as total_pizzas_sold
from pizza_sales group by pizza_name order by sum(quantity) asc;
