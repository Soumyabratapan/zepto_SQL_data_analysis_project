Here’s a **professionally written and corrected version** of your entire project overview — perfect for uploading to **GitHub README.md** or a portfolio:

---

# 🛒 E-Commerce Inventory Analysis Using SQL

## 📌 Project Overview

This project simulates how real-world **data analysts** in the **e-commerce/retail industry** use SQL to clean, explore, and extract business insights from messy inventory datasets.

The core objectives were to:

✅ Set up a messy, real-world e-commerce inventory database
✅ Perform **Exploratory Data Analysis (EDA)** to understand product categories, availability, and pricing issues
✅ Implement **data cleaning** to handle nulls, remove invalid entries, and convert pricing from **paise to rupees**
✅ Write **business-driven SQL queries** to uncover insights related to pricing, inventory, stock status, revenue, and more

---

## 📁 Dataset Overview

The dataset was sourced from **Kaggle**, originally scraped from **Zepto’s official product listings**. It closely mimics real e-commerce catalog data where products often appear multiple times due to different sizes, weights, categories, and discounts.

### 🧾 Columns:

* **sku\_id**: Unique identifier for each product entry (Synthetic Primary Key)
* **name**: Product name as shown on the app
* **category**: Product category (e.g., Fruits, Snacks, Beverages)
* **mrp**: Maximum Retail Price (converted from paise to ₹)
* **discountPercent**: Discount applied on MRP
* **discountedSellingPrice**: Final price after discount (₹)
* **availableQuantity**: Units available in inventory
* **weightInGms**: Product weight in grams
* **outOfStock**: Boolean indicating stock availability
* **quantity**: Units per package (sometimes mixed with weight)

---

## 🔧 Project Workflow

### 1️⃣ Database & Table Creation

We begin by creating the SQL table with appropriate column types:

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);
```

---

### 2️⃣ Data Import

The CSV file was imported using **pgAdmin's import feature**.

If not using pgAdmin, use the following `\copy` command in PostgreSQL:

```sql
\copy zepto(category, name, mrp, discountPercent, availableQuantity,
            discountedSellingPrice, weightInGms, outOfStock, quantity)
FROM 'data/zepto_v2.csv' WITH (
  FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8'
);
```

⚠️ Note: Encoding issues (UTF-8 errors) were resolved by saving the file as **CSV UTF-8** format.

---

### 3️⃣ 🔍 Data Exploration

* Counted total number of records
* Previewed sample rows to understand data structure
* Checked for **null values** in all columns
* Identified **unique product categories**
* Compared **in-stock vs out-of-stock** products
* Found **duplicate product names** across different SKUs

---

### 4️⃣ 🧹 Data Cleaning

* Removed rows where `mrp = 0` or `discountedSellingPrice = 0`
* Converted `mrp` and `discountedSellingPrice` from **paise to rupees** for consistency
* Ensured logical consistency in pricing and availability fields

---

### 5️⃣ 📊 Business Insights via SQL

* 🏷️ Identified **Top 10 best-value products** by highest discount percentage
* ❌ Listed **high-MRP products** that are currently out of stock
* 📈 Estimated **potential revenue** by product category
* 🔍 Filtered **premium products (MRP > ₹500)** with low discounts
* 🥇 Ranked **Top 5 categories** by average discount
* 💰 Calculated **price per gram** to identify value-for-money products
* ⚖️ Grouped products by weight into:

  * Low (< 250g)
  * Medium (250g–1kg)
  * Bulk (> 1kg)
* 🧮 Calculated **total inventory weight** by category

---

## ✅ Key Learnings

* Practical exposure to **SQL-based data cleaning and EDA**
* Experience with **realistic e-commerce datasets**
* Developed an understanding of **retail business metrics** and their SQL implementation
* Reinforced the importance of **data integrity and preprocessing**

---

## 🛠️ Tech Stack

* SQL (PostgreSQL)
* pgAdmin
* Excel (for verification & preprocessing)
* Dataset: [Kaggle – Zepto Products]
