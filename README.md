# ☕ Urban Coffee Chain Analysis

📌 Overview
This project simulates the operations of a fictional Urban Coffee Chain, focusing on customer behavior, product performance, and loyalty program insights.
It demonstrates SQL data cleaning, and analysis using realistic, messy datasets — designed to showcase recruiter‑friendly portfolio skills.

🗄️ Dataset - https://github.com/Rizwan-analytics/urban_coffee_chain_analysis/blob/main/urban_coffee_chain_dataset.xlsx
- Customers: first_name, last_name, email, phone and join_date
- Products: product_name, category, price and stock_quantity
- Orders & Order_Items: transaction details, order_date, store_status 
- Stores: urban locations with varied performance metrics
- Loyalty Programs: points and tiers

## 🎯 Business Questions & Insights
1. Product Performance
-	Find the top 5 products by total sales quantity. <img width="1459" height="735" alt="top5_products" src="https://github.com/user-attachments/assets/34c57e75-e1a8-4f9e-8b5f-ed1e081fb7a7" />
- Rank Products by Revenue Contribution. <img width="1096" height="847" alt="image" src="https://github.com/user-attachments/assets/f80b653b-721d-4222-83f4-3c4e24119077" />
2. Customer Behavior
 - Average Order Value per Store Location. <img width="1458" height="891" alt="image" src="https://github.com/user-attachments/assets/c943409e-5ae7-43ab-b2f4-87a3c901c9a8" />
 - Distribution of Customers Across Loyalty Tiers (Bronze, Silver, Gold, Platinum). <img width="1357" height="832" alt="image" src="https://github.com/user-attachments/assets/2f7b9ab3-366f-4f3c-9483-c003b797919f" />
- Identify Customers with More Than 20 Orders. <img width="1380" height="828" alt="image" src="https://github.com/user-attachments/assets/ffb0758d-4f34-4e4c-85e7-5c0844c5bca0" />
- Customer Lifetime Value (CLV). <img width="1372" height="836" alt="image" src="https://github.com/user-attachments/assets/6c0f512e-bbbb-4983-b691-e4be9dd7a57b" />

3. Revenue Analysis
- Month with Highest Revenue in 2025 - <img width="1416" height="471" alt="image" src="https://github.com/user-attachments/assets/9739b810-0155-40b6-b420-28b45410cd79" />

- Percentage of Refunded Orders per Store Location - <img width="1462" height="917" alt="image" src="https://github.com/user-attachments/assets/a38820e2-9214-40e5-94fe-86453e172f10" />

## SQL Techniques Used
- Joins → Combine Customers, Orders, Products, Loyalty tables
- Aggregations → SUM(), COUNT(), AVG() for KPIs
- Window Functions → RANK(), DENSE_RANK() for product ranking
- Conditional Logic → CASE WHEN for refund percentages

## power BI dashboard - <img width="1417" height="991" alt="image" src="https://github.com/user-attachments/assets/8d1e163b-823c-4c02-b524-100c225add51" />















  
