# 🛒 Super Store Sales Analysis (Power BI Project)
***Complex but interesting Power BI Use Case Questions***

This repository presents a complete Power BI project based on a **Superstore retail sales dataset**, designed to assist store managers in analyzing sales performance, customer behavior, cart values, delivery timelines, and profitability. This end-to-end project includes data extraction, transformation, modeling, and a range of insightful visualizations using DAX and Power Query.

## 📂 Files Included

- 📊 **Superstore Retail Business.pbix** – Power BI file containing all visualizations, data model, DAX measures, and transformations.
- 📄 **Super Store Project.docx** – Detailed project instructions, step-by-step logic, self-inference, and reasoning behind the applied solutions.
- 📈 **Superstore_Data_Fixed.xlsx** – Raw sales data including order, customer, product, shipping, and pricing details.

## 🧾 Dataset Overview

The dataset simulates a **multi-department superstore** offering diverse product categories across regions. Key data columns include:
- Order Date, Ship Date, Quantity, Discount, Price per Unit
- Address (to be split), Customer & Product Info
- Shipping Mode, Region, Order ID, Product ID, Customer ID

## ⚙️ Core Project Tasks

### 🧹 Data Preparation (Power Query)
- Loaded Excel data directly as a flat table.
- Cleaned dataset: removed nulls, checked column quality/distribution, set correct data types.
- Standardized `Ship Mode` values (e.g., "FC" → "First Class").
- Split `Address` into `City`, `State`, `Country`, and `Pincode`.

### 🧱 Data Modeling (Star Schema)
- Created 3 Dimension Tables from the main Orders table:
  - `Order Details`: Order ID, Ship Mode, Region, City, State, Country, Pincode
  - `Customer`: Customer ID, Name, Segment
  - `Product`: Product ID, Category, Sub-Category, Product Name
- Set up **One-to-Many relationships** using `Order ID`, `Customer ID`, and `Product ID`.
- Maintained necessary foreign keys and removed duplicate rows in dimension tables.

## 📐 DAX Measures & Calculations

### 💰 Sales Calculations
- `Sales` = `Quantity * Price Per Unit * (1 - Discount)`
- `Sales from Discounted Products` using `CALCULATE()` with `Discount > 0`

### 🛒 Cart Value Segmentation
- Created `Cart Value` column using nested `IF()`:
  - `< 1000 → Low`, `< 3500 → Medium`, `< 10000 → High`, `> 10000 → Very High`
- Built Pie Chart with Cart Value categories.

### 🔍 Focused Measures
- `Total Sales (Low Cart)` using:
  ```DAX
  CALCULATE(SUM(Orders[Sales]), Orders[Cart Value] = "Low")
  ```
- `Total Sales from Low Cart & High Discount (>=50%)` using:
  - `SUMX()` with `IF()` & `AND()`
  - or `CALCULATE()` with multiple filters

### 📦 Delivery Time Calculation
- `Delivery Days` = `DATEDIFF(Order Date, Ship Date, DAY)`
- Visualized average delivery days by `Ship Mode`.

### 📈 Time Intelligence
- `Sales YTD` using:
  ```DAX
  TOTALYTD(SUM(Orders[Sales]), Orders[Order Date].[Date])
  ```
- Built Matrix visualization with:
  - Order Date hierarchy
  - Sales and Sales YTD values

### 📊 Monthly Cumulative Sales & YoY Growth
- `Monthly Cumulation` using:
  ```DAX
  CALCULATE(SUM(Orders[Sales]), FILTER(ALLSELECTED(Orders[Order Date]), Orders[Order Date] <= MAX(Orders[Order Date])))
  ```
- Created **YoY Sales Growth** using **Quick Measures**

## 📊 Visualizations Built

- Card visuals for Total Sales, Discounted Sales, Low Cart Category
- Pie chart of Cart Value Categories
- Clustered column chart of Delivery Time by Ship Mode
- Matrix with Date Hierarchy, Sales, and Sales YTD
- Monthly YoY Sales Growth with cumulative comparison

## 🧠 Key Learnings & Insights

- Real-world transformation of messy Excel into a structured Star Schema model
- Handling non-obvious relationships (e.g., linking Order Details using Order ID)
- Use of both **Power Query** and **DAX** for calculation logic
- Difference in row-level vs column-level aggregation (`SUMX` vs `SUM`)
- Visual analytics to identify sales trends, performance bottlenecks, and seasonal patterns

## 🛠 Tools & Technologies

- **Power BI Desktop**
- **Power Query Editor**
- **DAX (Data Analysis Expressions)**
- **Excel (.xlsx)**

## 🏷 Tags

`Power BI` `Sales Dashboard` `Star Schema` `Power Query` `DAX`  
`Retail Analytics` `Cart Analysis` `Delivery Time` `YoY Sales Growth`

## 👤 Author

**Bidarth Kr. Singh**

## 📌 Credits

        This project was created by Bidarth Kr. Singh and is distributed under the "Apache License" license.

---
