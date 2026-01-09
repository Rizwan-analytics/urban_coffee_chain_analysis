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












