# Toys_Sales_Project_Analysis
This project is an end-to-end Power BI business intelligence solution built on the Maven Toys Sales dataset. It analyzes toy sales performance across products, categories, stores, locations, cities, and time (2022–2023), with a strong focus on revenue, profit, inventory efficiency, and store performance.

# 🧸 Maven Toys Sales Analysis — Power BI Dashboard

An end-to-end Power BI business intelligence project built on the **Maven Toys Sales dataset**, analyzing toy sales performance across products, categories, stores, locations, and time (2022–2023). The project focuses on revenue, profitability, inventory efficiency, and store performance — designed to showcase data modeling, DAX, dashboard design, and business storytelling skills.

**Author:** Sujal More

---

## 📌 Project Overview

This project transforms raw retail data into an interactive Power BI solution that helps stakeholders track revenue trends, evaluate profitability, monitor inventory health, and identify growth opportunities across stores and product categories.

## 🎯 Business Objectives

- Identify top-performing products and categories
- Analyze store and location-wise revenue contribution
- Track sales trends over time (Year → Quarter → Month)
- Evaluate profitability and margins
- Monitor inventory health and turnover
- Enable data-driven decisions for product planning and store optimization

---

## 🧩 Data Model

The project uses a **star-schema-inspired relational model** optimized for Power BI performance.

### Tables

| Table | Type | Key Fields |
|---|---|---|
| **Sales** | Fact | Sale_ID, Date, Year, Product_ID, Store_ID, Units |
| **Products** | Dimension | Product_ID, Product_Name, Product_Category, Product_Price, Product_Cost |
| **Stores** | Dimension | Store_ID, Store_Name, Store_City, Store_Location |
| **Inventory** | Bridge / Fact-like | Product_ID, Store_ID, Stock_On_Hand |

### Relationships

- Products (1) → Sales (*)
- Stores (1) → Sales (*)
- Products (1) → Inventory (*)
- Stores (1) → Inventory (*)

This model supports accurate aggregation, filtering, and time-based analysis across the entire report.

---

## 🧮 Key DAX Measures

```dax
Total_Revenue = 
SUMX ( Sales, Sales[Units] * RELATED ( Products[Product_Price] ) )

Total_Profit = 
SUMX ( 
    Sales, 
    Sales[Units] * ( RELATED ( Products[Product_Price] ) - RELATED ( Products[Product_Cost] ) ) 
)

Profit_Margin_% = 
DIVIDE ( [Total_Profit], [Total_Revenue], 0 )

Order_Count = 
DISTINCTCOUNT ( Sales[Sale_ID] )

Highest_Revenue_ProductName = 
VAR ProductRevenue =
    SUMMARIZE (
        Products,
        Products[Product_Name],
        "TotalRevenue",
            CALCULATE ( SUMX ( Sales, Sales[Units] * RELATED ( Products[Product_Price] ) ) )
    )
VAR TopProduct =
    TOPN ( 1, ProductRevenue, [TotalRevenue], DESC )
RETURN
    MAXX ( TopProduct, Products[Product_Name] )
```

---

## 📊 Dashboards

### 1️⃣ Executive Summary Dashboard

**Purpose:** High-level performance tracking for management

**Key KPIs**
| Metric | Value |
|---|---|
| Total Revenue | $14.44M |
| Total Profit | $4.01M |
| Total Units Sold | 1.09M |
| Profit Margin | 27.79% |
| Total Orders | 829K |

**Visuals**
- Revenue trend by Year / Quarter / Month
- Revenue share by Store Location (Downtown, Commercial, Residential, Airport)
- Revenue by Product Category
- Geographic distribution of sales by Store City (map visual)

**Insights**
- Downtown stores contribute the largest share of revenue (~57%)
- Toys is the top revenue-driving category
- Clear seasonal patterns are visible in monthly revenue
<img width="1252" height="716" alt="toy_sales_dashboard" src="https://github.com/user-attachments/assets/86d30bd1-195e-45a8-b08a-52c37f4d04ad" />


---

### 2️⃣ Category & Store Sales Analysis Dashboard

**Purpose:** Deep-dive analysis for category managers and operations teams

**Key Metrics**
| Metric | Value |
|---|---|
| Total Products | 35 |
| Highest Revenue Product | Lego Bricks |
| Total Stores | 50 |
| Sales per Store | ✅ |
| Inventory Turnover | ✅ |
| Average Inventory | ✅ |

**Visuals**
- Revenue trends by Product Category over time
- Revenue trends by Store Location over time
- Product-level table — Revenue, Profit, Profit Margin, Order Count, Cost
- Store-level table — Orders, Units Sold, Average Order Value, Store Location

**Insights**
- Lego Bricks is the highest revenue-generating product
- Certain stores show high order volume but lower AOV, indicating upsell opportunities
- Inventory turnover highlights fast- vs. slow-moving products
  <img width="1383" height="909" alt="Dashboard1" src="https://github.com/user-attachments/assets/140e85d8-b7b9-414a-9e91-7ef2dccd2c27" />


---

## 🎛️ Interactivity & Filters

- Year slicer (2022, 2023)
- Product Category slicer
- Store Location slicer
- Cross-filtering enabled across all visuals

Users can perform dynamic, self-service analysis without needing to write queries.

---

## 🛠 Tools & Technologies

- Power BI Desktop
- DAX (Data Analysis Expressions)
- Data Modeling & Relationships
- Power BI Maps (Bing)
- Maven Analytics Dataset

---

## 📈 Key Business Takeaways

- Focus inventory and promotions on high-margin products
- Expand or optimize Downtown store operations
- Improve performance of low-revenue store locations
- Use inventory turnover to reduce holding costs
- Leverage time trends for seasonal planning

---

## 📂 Repository Contents

```
├── Maven_Toys_Sales_Analysis_BI.pbix   # Power BI report file  #products.csv  #store.csv
└── README.md                           #inventory(1).csv       #sales.csv
```

The report includes both the **Executive Summary** and **Detailed Analysis** views described above.

---

## 👤 Author

**Sujal More**

Data Analyst | Power BI Developer

If you found this project useful, consider giving the repo a ⭐!
