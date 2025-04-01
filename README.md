# Mint Classics Inventory Analysis: Data-Driven Warehouse Optimization

## Project Overview
Mint Classics is a fictional retailer of classic model cars and collectible vehicles. The company is evaluating the potential closure of one of its storage warehouses to reduce operational overhead and improve inventory efficiency.

This project involves conducting exploratory data analysis using MySQL Workbench on a relational database containing business-critical data such as inventory levels, sales records, employee assignments, and product information. The goal is to assess warehouse performance using key metrics like turnover rate, overstock ratio, inventory utilization, and revenue contribution to inform a data-driven recommendation on which warehouse should be considered for closure.

#### 🌐  Link to Coursera project: [Mint Classic Coursera Project](https://www.coursera.org/learn/showcase-analyze-data-model-car-database-mysql-workbench/home/welcome)
---
## Objectives

1. Explore products currently in inventory.
2. Determine important factors that may influence inventory reorganization/reduction.
3. Provide analytic insights and data-driven recommendations.
   
Guided by the objectives, SQL queries were developed and executed in MySQL Workbench to analyze the relational database and answer key questions, such as:

- Which warehouse is most/least efficient?
- Where are we overstocking vs. under-selling products?
- Can inventory be redistributed to avoid service disruptions?
- What is the revenue and operational performance of each warehouse?

---
## Data Model & Schema Overview
This project utilizes a structured relational database which included several interconeected tables:

`products` and `productLine` – Information on each model car, including quantity in stock, warehouse location, MSRP, and buy price.

`orders` and `orderdetails` – Sales transaction data, including order quantities, prices, and product references.

`employees` and `offices` – Organizational data linking staff to geographic regions.

`customers` – Customer and account details, linked to employees for sales tracking.

The relationships between these tables are illustrated in the EER (Enhanced Entity-Relationship) diagram below:
![EER Diagram](images/EERDiagram.JPG)
___
## 📊 Data Analysis and Key Insights
This section outlines the processes taken the analyze and to determine which Mint Classics warehouse may be closed with minimal disruption and maximum efficiency. Each subsection presents a key business question, a brieft description of the analysis performed with MySQL Workbench, and insights gathered.

## 1.) Which Warehouse Generates the Most Revenue?
💬 Question: What are the total sales figures by warehouse?

### Analysis:
To obtain the `total_revenue` per warehouse, `priceEach` and `quantityOrdered` from table `orderdetails` were multiplied. `join`, `ORDER BY` and `GROUP BY`clause were utilized in order to obtain the results per warehouse.

<details>
<summary>📜 Click to expand SQL Query</summary>
  
 ```sql
 SELECT p.warehouseCode, 
       SUM(od.quantityOrdered * od.priceEach) AS total_revenue
FROM orders o
JOIN orderdetails od ON od.orderNumber = o.orderNumber
JOIN products p ON od.productCode = p.productCode
GROUP BY p.warehouseCode;--
```
 </details> 

## Key Findings:

![TotalRevSQl SS](images/TotalRevSQL.png)

• Warehouse B generated the most revenue overall.

• Warehouse C had the lowest total revenue, suggesting inefficiencies in inventory usage despite comparable stock levels.

<p align="center"> <img src="images/TotalRevSQL.png" alt="SQL Query Screenshot" width="45%" /> <img src="images/TotalRevPerWarehosue.png" alt="Revenue Chart" width="45%" /> </p>

### Revenue Trends Over Time
A second query was written to track revenue changes over time. This reveals seasonal or operational trends across warehouses.

<details> <summary> Click to expand SQL Query</summary>
  
```sql

SELECT DATE_FORMAT(o.orderDate, '%Y-%m') AS 'year-month', p.warehouseCode,
       SUM(od.quantityOrdered * od.priceEach) AS total_revenue
FROM orders o
JOIN orderdetails od ON od.orderNumber = o.orderNumber
JOIN products p ON od.productCode = p.productCode
GROUP BY p.warehouseCode, DATE_FORMAT(o.orderDate, '%Y-%m')
ORDER BY 'year-month';
```

</details> <p align="center"> <img src="images/MonthlyRevenuePerWarehouse.png" alt="Monthly Revenue by Warehouse" width="80%" /> </p>
📌 Insights:

Revenue from Warehouse C stagnated over time, suggesting inefficiency.

Warehouse D rebounded steadily after a low point in early 2005.

Warehouse A saw a gradual decline, while B remained relatively consistent.



## 📊 Tools & Technologies
- **SQL**: MySQL Workbench
- **Skills Used**: `JOIN`, `GROUP BY`, `HAVING`, subqueries, `NTILE()`, filtering, calculations
- **Data**: 10+ relational tables including products, orders, customers, employees, order details, warehouses, and offices

---

## 📊 Key Insights

### 🏢 Warehouse Utilization & Efficiency
- **Warehouse B** has:
  - The highest revenue
  - The **lowest turnover rate (0.0061)**
  - The **most overstocked inventory (164x ratio)**
- **Warehouse C** is only **50% utilized**, the lowest among all.
- **Warehouse D** has the **highest turnover rate (0.0102)** and sells inventory efficiently.

### 👚 Overstock Analysis
- 71 products across all warehouses had an **overstock ratio > 100**.
- Most of these low-performing products are stored in **Warehouse B**.
- Products like the 1992 Ferrari 360 Spider Red were top-sellers, while the 1957 Ford Thunderbird performed worst.

### 📅 Revenue Insights
- Warehouse B generated the **most total revenue** ($3.85M), but holds much slow-moving inventory.
- **Warehouse C has the highest profit margins** but brings in the **least total revenue**.
- Warehouse A's revenue is **declining** based on time series trend plots.

### 👨‍💼 Employee/Customer Dependencies
- 15 employees are directly tied to sales fulfilled by **Warehouse C**.
- Customers from regions tied to Warehouse C contribute a **minor portion** of revenue.

### 🚚 Logistics Considerations
- Warehouse D is near capacity (75%) and handles fast-moving products like Trains/Ships.
- Warehouse C serves some unshipped orders, which would need to be redistributed if closed.

---

## ✅ Recommendation
After detailed SQL-based analysis, **Warehouse C** emerges as the top candidate for closure:
- Underutilized (50% capacity)
- Least revenue generation
- Lower sales throughput
- Fewest customer/employee dependencies

Redistributing slow-moving products from **Warehouse B** can further optimize the supply chain.

---

## 📄 Files in This Repository
| File | Description |
|------|-------------|
| `mintclassicsDB.sql` | SQL database dump of the Mint Classics schema |
| `analysis_queries.sql` | SQL scripts used for analysis |
| `Mint_Classics_Analysis_Report.pdf` | Full PDF report with visuals and narrative |
| `README.md` | Project overview and summary |

---

## 🚀 Future Improvements
- Include storage cost data for deeper operational cost analysis
- Integrate external sales forecasting tools (Python, Excel)
- Apply time-series models for seasonality adjustments

---

## 🎓 Author
**Clem117343** | Aspiring AI Engineer with a passion for SQL, data, and operational insights.

---

## 🌍 Connect
- [LinkedIn Profile](https://www.linkedin.com/in/clementchai117)
- [Portfolio Website](https://yourwebsite.com) _(optional)_

> “In God we trust. All others must bring data.” — W. Edwards Deming

