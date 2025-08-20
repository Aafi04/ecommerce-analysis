# E-commerce Sales Analysis Dashboard using Power BI

This repository contains the Power BI project file, documentation, and resources for an interactive E-commerce Sales Dashboard. The dashboard was developed as part of the **GUVI & HCL Data Analytics Internship** to analyze sales, logistics, and seller performance for a Brazilian e-commerce marketplace.

---

## 📊 Dashboard Preview

- **Page 1:** Sales & Orders Overview
- **Page 2:** Seller & Logistics Performance

> _Note: Upload your dashboard images to a service like Imgur and replace the placeholder links above with your actual image URLs._

---

## 🎯 Problem Statement

As a Business Intelligence Analyst, the primary objective was to design and develop an interactive Power BI dashboard to provide key insights into an e-commerce company's operations. The dashboard is intended for stakeholders (e.g., sales managers, logistics coordinators) to help them make informed, data-driven decisions by analyzing sales trends, top-performing products, seller performance, and shipping efficiency.

---

## 📦 Dataset

- **Source:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (Kaggle)
- **Details:** Over 100,000 orders placed between 2016 and 2018
- **Tables:** Orders, Products, Customers, Sellers, Shipping Logistics

---

## ⚙️ Project Workflow

1. **Data Import & Cleaning:**

   - Connected Power BI to raw CSV files
   - Used Power Query Editor for data cleaning (corrected data types, renamed columns, filtered nulls, translated text)

2. **Data Modeling:**

   - Established a star-schema model
   - Defined relationships between fact and dimension tables

3. **DAX Implementation:**

   - Created 4 calculated columns & 3 key measures

4. **Visualization & Reporting:**
   - Designed a two-page interactive dashboard
   - Included visuals, slicers, and drill-down capabilities

---

## ✨ Data Transformation Steps (Power Query)

- **Corrected Data Types:** Converted timestamp columns to Date/Time
- **Renamed Columns:** Fixed spelling errors in Products table
- **Filtered Null Values:** Removed rows with missing product categories
- **Translated Product Categories:** Merged external Excel translation map
- **Finalized Table Structure:** Removed redundant Portuguese category column

---

## 🔢 DAX Formulas

### Calculated Columns

- **Delivery Time (Days):**
  ```DAX
  Delivery Time (Days) = DATEDIFF(olist_orders_dataset[order_purchase_timestamp], olist_orders_dataset[order_delivered_customer_date], DAY)
  ```
- **Order Status Group:**
  ```DAX
  Order Status Group = IF(olist_orders_dataset[order_status] = "delivered", "Completed", "Incomplete")
  ```
- **On-Time Status:**
  ```DAX
  On-Time Status = IF(
      NOT ISBLANK(olist_orders_dataset[order_delivered_customer_date]),
      IF(
          olist_orders_dataset[order_delivered_customer_date] <= olist_orders_dataset[order_estimated_delivery_date],
          "On-Time",
          "Late"
      ),
      "In Transit"
  )
  ```
- **Estimated Delivery Time (Days):**
  ```DAX
  Estimated Delivery Time (Days) = DATEDIFF(olist_orders_dataset[order_purchase_timestamp], olist_orders_dataset[order_estimated_delivery_date], DAY)
  ```

### Measures

- **Total Revenue:**
  ```DAX
  Total Revenue = SUM(olist_order_items_dataset[price])
  ```
- **Average Delivery Time:**
  ```DAX
  Average Delivery Time = AVERAGE(olist_orders_dataset[Delivery Time (Days)])
  ```
- **On-Time Delivery %:**
  ```DAX
  On-Time Delivery % = DIVIDE(
      CALCULATE(COUNTROWS(olist_orders_dataset), olist_orders_dataset[On-Time Status] = "On-Time"),
      CALCULATE(COUNTROWS(olist_orders_dataset), olist_orders_dataset[order_status] = "delivered")
  )
  ```

---

## 💡 Key Insights & Actionable Solutions

### 1. Dominant Market Concentration

- **Insight:** São Paulo drives most revenue; a few categories (e.g., Health & Beauty) dominate sales.
- **Action:** Launch targeted campaigns in the next top 3 states to diversify revenue.

### 2. Significant Growth with Untapped Potential

- **Insight:** Strong year-over-year growth; other major markets underdeveloped.
- **Action:** Increase marketing for top categories and create a loyalty program for São Paulo customers.

### 3. Logistical Inconsistencies

- **Insight:** Overall on-time delivery is high (~92%), but some states lag.
- **Action:** Audit logistics in worst-performing states and consider new courier partnerships.

---

## 🛠️ Tools Used

- **Microsoft Power BI:** Data modeling, analysis, visualization
- **Microsoft Excel:** Translation map creation
- **DAX (Data Analysis Expressions):** Custom calculations

---

## 🚀 How to Use

1. Clone this repository to your local machine.
2. Open the `E-commerce Sales Dashboard.pbix` file in Power BI Desktop.
3. Interact with the dashboard using slicers and visual elements.

---

## 👨‍💻 Author & Acknowledgments

- **Author:** Mohd Aafi
- **Mentorship:** Mr. Santhosh Baskar (GUVI & HCL Data
