# ☕ Coffee Shop Sales Performance Dashboard | Power BI

## 📌 Project Overview
This project showcases an end-to-end **Power BI Sales Analytics Dashboard** built for a multi-location coffee shop.  
The dashboard provides actionable insights into **sales performance, customer demand patterns, product popularity, and store-level efficiency**, enabling data-driven business decisions.

---

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

## 🖼 Dashboard Preview
<img width="1209" height="735" alt="Coffee_Shop_Sales_Dashboard_img" src="https://github.com/user-attachments/assets/206b3a13-7ec1-41ca-a8da-b95d79887f30" />


---

## 📊 Key KPIs
- **Total Sales:** $119K (+20.3% vs Last Month)
- **Total Orders:** 25,335 (+19.3%)
- **Total Quantity Sold:** 36,469 (+19.9%)
- **Average Daily Sales:** $3,965
- **Weekday Contribution:** 66.9%
- **Weekend Contribution:** 33.1%

---

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
SUM(FactSales[SalesAmount])

Total Orders =
COUNT(FactSales[OrderID])

Total Quantity Sold =
SUM(FactSales[Quantity])

Sales Last Month =
CALCULATE(
    [Total Sales],
    DATEADD(DimDate[Date], -1, MONTH)
)

Sales MoM % =
DIVIDE(
    [Total Sales] - [Sales Last Month],
    [Sales Last Month]
)

Avg Daily Sales =
AVERAGEX(
    VALUES(DimDate[Date]),
    [Total Sales]
)
