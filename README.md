# <img width="30" height="30" alt="coffee-cup" src="https://github.com/user-attachments/assets/def9a39e-e460-43a8-b533-a6b8a5486ef2" /> Coffee Shop Sales Performance Dashboard | Power BI

## 📌 Project Overview
This project showcases an end-to-end **Power BI Sales Analytics Dashboard** built for a multi-location coffee shop.  
The dashboard provides actionable insights into **sales performance, customer demand patterns, product popularity, and store-level efficiency**, enabling data-driven business decisions.



<img width="1209" height="735" alt="Coffee_Shop_Sales_Dashboard_img" src="https://github.com/user-attachments/assets/206b3a13-7ec1-41ca-a8da-b95d79887f30" />


## 🔍 Business Problem
The coffee shop management faced challenges in:
- Tracking daily and monthly sales trends
- Identifying peak sales hours and days
- Understanding product and category performance
- Comparing revenue across store locations
- Monitoring month-over-month growth

Manual reporting made it difficult to gain quick and reliable insights.

---

## 🎯 Objectives
- Monitor **Total Sales, Orders, and Quantity Sold**
- Analyze **sales trends over time**
- Identify **top-performing products and categories**
- Compare **weekday vs weekend performance**
- Discover **peak sales hours**
- Track **store-wise contribution**
- Measure **month-over-month (MoM) growth**

---

## 📊 Key KPIs & Visual Highlights
- **Total Sales:** $119K (+20.3% vs previous month)
- **Total Orders:** 25,335 (+19.3%)
- **Total Quantity Sold:** 36,469 (+19.9%)

- **Calendar Heat Map:**  
  Visualizes daily sales performance using gradient color intensity to quickly identify high- and low-performing days.

- **Average Daily Sales:**  
  Displays average daily revenue segmented by product category and product type to understand demand patterns.

- **Sales by Store Location:**  
  Custom double bar chart where the first bar acts as a label placeholder, enabling clear display of store names alongside their corresponding sales values.


## 🧠 Data Model & Architecture
- **Star Schema** design for optimized analytics
  - FactSales
  - Date Table
  - DimProduct
  - DimStore
- Optimized relationships and cardinality
- Power Query used for:
  - Data cleaning
  - Date table generation
  - Standardizing categorical fields

---

## 📐 Key DAX Measures
```DAX
Total Sales = 
SUM(Transactions[Sales])

Total Orders = 
DISTINCTCOUNT(Transactions[transaction_id])

Total Quantity Sold = 
SUM(Transactions[transaction_qty])

Sales Last Month =
CALCULATE( [CM Orders], DATEADD('Date Table'[Date],-1,MONTH) )

Sales MoM for Sales =
    VAR month_diff = [CM Sales] - [PM Sales]
    VAR MoM = ([CM Sales]-[PM Sales])/[PM Sales]
    VAR _sign = IF(month_diff > 0, "+", "")
    VAR _sign_trend = IF(month_diff > 0, "▲", "▼")
    RETURN
    IF (ISBLANK([PM Sales]) || [PM Sales] = 0,"No Value", 
    _sign_trend & " " & _sign & FORMAT(MoM,"#0.0%"))

Avg Daily Sales =
AVERAGEX(
    VALUES(DimDate[Date]),
    [Total Sales]
)
