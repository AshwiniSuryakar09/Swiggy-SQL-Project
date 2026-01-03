# 🍔 Swiggy Data Analysis using SQL Server

📌 Project Overview

This project focuses on cleaning, validating, modeling, and analyzing Swiggy food order data using Microsoft SQL Server.
The raw dataset is transformed into a Star Schema (Fact & Dimension tables) and used to generate business-ready insights such as revenue, average pricing, and order trends.

> ## 🎯 Objectives

  1. Clean and validate raw Swiggy order data

  2. Identify and remove duplicate records

  3. Design a Star Schema for analytics

  4. Build a Fact table with multiple dimensions

  5. Perform business KPI analysis using SQL queries


> ## 🛠 Tools & Technologies


Database : 
  
  1. Microsoft SQL Server
  2. Language: SQL (T-SQL)


Concepts Used :

  1. CTEs

  2. Window Functions (ROW_NUMBER)

  3. Joins

  4. Aggregations

  5. Date functions

  6. Star Schema Modeling




> ## 🧹 Data Cleaning & Validation
  
✔ Null Value Checks

   1. State

   2. City

   3. Order Date

   4. Restaurant Name

   5. Location

   6. Category

   7. Dish Name

   8. Price

   9. Rating

   10. Rating Count




✔ Empty String Detection

   Handled invalid empty values in text columns and NULL checks for numeric fields.



   

✔ Duplicate Detection & Removal

  Duplicates were identified using:

  GROUP BY + HAVING COUNT(*) > 1

  Removed safely using ROW_NUMBER() with CTE.


>  ##  🏗 Data Modeling (Star Schema)

 
📘 Dimension Tables

   dim_date

   dim_location

   dim_restaurant

   dim_category

   dim_dish




📕 Fact Table

   fact_swiggy_orders

   Each order record is linked using surrogate keys, enabling fast analytical queries.




> ## 🔗 Schema Relationship


 fact_swiggy_orders
 
 │
 
 ├── dim_date
 
 ├── dim_location
 
 ├── dim_restaurant
 
 ├── dim_category
 
 └── dim_dish




> ## 📊 Key Business Queries & Insights

 
     💰 Total Revenue (INR Million)
                SELECT 
                FORMAT(SUM(Price_INR) / 1000000, 'N2') + ' INR Million' AS Total_Revenue
                FROM fact_swiggy_orders;
                


      🍽 Average Dish Price
                SELECT 
                FORMAT(AVG(Price_INR), 'N2') + ' INR' AS Average_Dish_Price
                FROM fact_swiggy_orders;          



      📅 Orders by Day of Week
                SELECT 
                DATENAME(WEEKDAY, d.Full_Date) AS Day_Name,
                COUNT(*) AS Total_Orders
                FROM fact_swiggy_orders f
                JOIN dim_date d 
                ON f.date_id = d.date_id
                GROUP BY 
                DATENAME(WEEKDAY, d.Full_Date),
                DATEPART(WEEKDAY, d.Full_Date)
                ORDER BY DATEPART(WEEKDAY, d.Full_Date);





> ## 🚀 Key Learnings

 1. Importance of dimension data completeness before loading fact tables

 2. How INNER JOIN failures can silently drop records

 3. Correct usage of aggregations vs unit conversions

 4. Designing scalable analytics-ready schemas

 5. Writing performance-friendly SQL queries





> ## 📂 Repository Structure

  
  📁 Swiggy-SQL-Analysis
  
  │
  
  ├── SQLQuerySwiggyFullcode.sql
  
  ├── README.md 




> ## 📈 Future Enhancements

  * City-wise & restaurant-wise revenue analysis

  * Monthly revenue trends

  * Top 10 restaurants & dishes

  * Power BI / Excel dashboard integration





 > ## Author
   [Ashwini Suryakar](https://www.linkedin.com/in/ashwini-suryakar/)
