# ☕ Urban Coffee Chain Analysis

📌 Overview
This project simulates the operations of a fictional Urban Coffee Chain, focusing on customer behavior, product performance, and loyalty program insights.
It demonstrates SQL data cleaning, and analysis using realistic, messy datasets — designed to showcase recruiter‑friendly portfolio skills.

🗄️ Dataset
- Customers: first_name, last_name, email, phone and join_date
- Products: product_name, category, price and stock_quantity
- Orders & Order_Items: transaction details, order_date, store_status 
- Stores: urban locations with varied performance metrics
- Loyalty Programs: points and tiers 

**🔍 Query Levels
# ☕ Urban Coffee Chain Analysis

## 🟢 Basic Queries

**1. List all customers who joined in 2024**
```sql
SELECT CONCAT(first_name, ' ', last_name) AS customer_name
FROM Customers
WHERE YEAR(join_date) = 2024;

--2.Find the total number of products in each category
SELECT category, COUNT(product_id) AS total_num
FROM Products
GROUP BY category;
--3.Show all orders placed in Delhi with payment method = "UPI"
SELECT order_id
FROM Orders
WHERE store_location = 'delhi' AND payment_method = 'upi';

--4.Retrieve the top 10 customers by loyalty points
SELECT TOP 10 
       CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
       l.points
FROM Customers AS c
JOIN Loyalty AS l ON c.customer_id = l.customer_id
ORDER BY l.points DESC;

--5.Count how many orders were cancelled in 2025
SELECT COUNT(order_id) AS cancelled_order
FROM Orders
WHERE order_status = 'cancelled'
  AND YEAR(order_date) = 2025;

---
# intermediate query

--1.Find the top 5 products by total sales quantity
SELECT TOP 5 
       SUM(oi.quantity * p.price) AS total_sale,
       p.product_name
FROM Order_Items AS oi
JOIN Products AS p ON p.product_id = oi.product_id
GROUP BY p.product_name
ORDER BY total_sale DESC;

--2.Calculate the average order value per store location
SELECT o.store_location,
       AVG(oi.quantity * p.price) AS average_order_value
FROM Order_Items AS oi
JOIN Orders AS o ON oi.order_id = o.order_id
JOIN Products AS p ON oi.product_id = p.product_id
GROUP BY o.store_location;

--3.Show the distribution of customers across loyalty tiers
SELECT tier, COUNT(customer_id) AS total_customer
FROM Loyalty
GROUP BY tier
ORDER BY total_customer DESC;

--4.Identify customers who have placed more than 20 orders
SELECT CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
       COUNT(o.order_id) AS total_orders
FROM Orders AS o
JOIN Customers AS c ON o.customer_id = c.customer_id
GROUP BY CONCAT(c.first_name, ' ', c.last_name)
HAVING COUNT(o.order_id) >= 20
ORDER BY total_orders DESC;

--5.Find the month with the highest revenue in 2025
SELECT DATENAME(month, o.order_date) AS month_,
       SUM(oi.quantity * p.price) AS total_revenue
FROM Order_Items AS oi
JOIN Orders AS o ON oi.order_id = o.order_id
JOIN Products AS p ON oi.product_id = p.product_id
WHERE YEAR(o.order_date) = 2025
GROUP BY DATENAME(month, o.order_date)
ORDER BY total_revenue DESC;

 **advance level query **

--1.Calculate Customer Lifetime Value (CLV): total revenue per customer across all orders.

select 
c.customer_id,
concat(c.first_name,'',c.last_name) as customer_name,
sum(oi.quantity * oi.price) as total_revenue
from customers c 
join Orders  as o
on c.customer_id = o.customer_id
join Order_Items as oi
on o.order_id = oi.order_id
group by c.customer_id, concat(c.first_name,'',c.last_name)
order by sum(oi.quantity * oi.price) desc

--2.Rank products by revenue contribution using RANK() or DENSE_RANK().
select 
p.product_id,
p.product_name,
sum(oi.quantity*oi.price) as total_revenue,
rank() over(order by sum(oi.quantity*oi.price) desc) as product_rank
from products as p 
join order_items as oi
on p.product_id = oi.product_id
group by p.product_id, p.product_name
order by sum(oi.quantity*oi.price) desc

--3. -- find duplicate customer bu email
select 
email,
count(*) as duplicate_email
from customers 
group by email
having count(*)>1
-- there is not duplicate found 

-- find duplicate customer through phone number 
select 
phone,
count(*) as duplicate_phone
from Customers
group by phone
having count(*)>1

-- there is not duplicate phone found

--4.Find the percentage of refunded orders per store location.
select 
store_location,
concat(count(case when order_status = 'refunded' then 1 end)*100/count(*),'%') as refunded_percentage
from orders 
group by store_location 
order by count(case when order_status = 'refunded' then 1 end)*100/count(*)  desc

--5.Build a query that shows year-over-year growth in total sales.

WITH customers_2024 AS (
    SELECT 
        customer_id,
        CONCAT(first_name, ' ', last_name) AS customer_name
    FROM Customers
    WHERE YEAR(join_date) = 2024
),
orders_2025 AS (
    SELECT DISTINCT customer_id
    FROM Orders
    WHERE YEAR(order_date) = 2025
)
SELECT 
    COUNT(*) AS total_customers_2024,
    COUNT(CASE WHEN o.customer_id IS NULL THEN 1 END) AS churned_customers,
    ROUND(
        COUNT(CASE WHEN o.customer_id IS NULL THEN 1 END) * 100.0 / COUNT(*), 
        2
    ) AS churn_rate_percentage
FROM customers_2024 c
LEFT JOIN orders_2025 o 
    ON c.customer_id = o.customer_id; '''

## Dashboard
<img width="1459" height="735" alt="top5_products" src="https://github.com/user-attachments/assets/19deb4ca-0e4b-4c77-8daf-5c48e24d4034" />


