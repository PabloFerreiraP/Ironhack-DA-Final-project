# 🚲 Bike Store Demand Forecasting & Stock Optimization

An end-to-end Business Intelligence solution for bike retail inventory optimization, combining **XGBoost** demand forecasting with an interactive **Tableau** dashboard to prevent stockouts and reduce excess capital tied up in inventory.

---

## 📋 Table of Contents
- [Business Problem](#-business-problem)
- [Data Architecture](#-data-architecture)
- [Methodology & Pipeline](#-methodology--pipeline)
- [Key Inventory KPIs](#-key-inventory-kpis)
- [Tableau Dashboard Features](#-tableau-dashboard-features)
- [Key Insights & Recommendations](#-key-insights--recommendations)
- [Tech Stack](#-tech-stack)
- [Author](#-author)

---

## 🎯 Business Problem
Retail bike operations often struggle with an imbalance between supply and demand across different store locations, brands, and bicycle categories:
* **Stockouts** in high-demand segments lead to lost sales and lower customer satisfaction.
* **Overstock** in slow-moving categories ties up working capital and increases storage costs.

The goal of this project is to predict monthly product demand and establish an actionable **6-month Safety Stock** threshold to guide purchasing and inter-store stock transfers.

---

## 🗄️ Data Architecture
The data model integrates relational tables from a US multi-store bike retailer (operating in **Baldwin, NY**, **Santa Cruz, CA**, and **Rowlett, TX**):
* `df_merged.csv`: Core transactional and inventory dataset combining orders, order items, products, and current stock levels.
* `stores.csv`: Store metadata and geographical locations.
* `categories.csv`: Product classification (*Cruisers, Mountain, Children, Road, Comfort, Electric, Cyclocross*).
* `brands.csv`: Manufacturer details (*Electra, Trek, Surly, Sun Bicycles, Haro, Ritchey, Strider, Heller, Pure Cycles*).

---

## ⚙️ Methodology & Pipeline
1. **Data Cleaning & Feature Engineering (Python):**
   * Handled missing values, standardized date formats, and aggregated historical sales into monthly demand intervals.
   * Merged relational tables using primary/foreign keys (`store_id`, `product_id`, `category_id`, `brand_id`).
2. **Exploratory Data Analysis (EDA):**
   * Analyzed seasonality, brand performance, and inventory distribution across the three retail locations.
3. **Demand Forecasting (XGBoost):**
   * Trained a gradient boosting regression model (`XGBoost`) to forecast expected monthly demand per category, brand, and store.
4. **Inventory Optimization & BI Visualization (Tableau):**
   * Designed dynamic calculated fields to evaluate stock coverage and generate exact reorder quantities.

---

## 📊 Key Inventory KPIs
The dashboard tracks the following core supply chain metrics:

| Metric | Formula / Logic | Business Purpose |
| :--- | :--- | :--- |
| **Monthly Demand** | Predicted / Max Monthly Units Sold | Baseline consumption rate per segment. |
| **Current Stock** | `SUM([Stock Quantity])` | Real-time physical inventory available. |
| **Safety Stock (6m)** | 6-Month Coverage Target | Buffer stock required to prevent stockouts over a 6-month horizon. |
| **Safety Stock Cover** | `SUM([Stock Quantity]) / SUM([Safety Stock])` | Percentage of target buffer currently fulfilled (`<100%` indicates deficit). |
| **Ordering Quantity** | `MAX(0, SUM([Safety Stock]) - SUM([Stock Quantity]))` | Exact number of units to reorder to reach optimal safety levels. |
| **Months of Stock** | `SUM([Stock Quantity]) / [Monthly Demand]` | Estimated runway (in months) before current inventory depletes. |
| **Turnover Ratio** | Annualized Sales / Average Inventory | Measures how efficiently inventory is sold and replaced. |

---

## 📈 Tableau Dashboard Features
* **Executive Inventory Matrix:** Color-coded breakdown by *Category* and *Brand* highlighting critical reorder alerts (red) vs. healthy/overstocked items (green).
* **Demand vs. Stock Comparison Charts:** Side-by-side category bar charts comparing monthly demand pressure against total stock volume.
* **Cross-Filtering & Interactive Controls:** Global filters by *Store*, *Category Name*, and *Brand Name*, plus click-to-filter actions across all visual components.

---

## 💡 Key Insights & Recommendations
* **Immediate Reorder Priority:** Specific high-turnover segments—such as *Electric Bikes (Sun Bicycles)* and *Mountain Bikes (Ritchey)*—operate below 25% safety stock cover and require immediate replenishment (**1,051 total units** identified across deficit segments).
* **Overstock Mitigation:** Brands like *Trek* (in Road and Electric categories) and *Electra* (in Cruisers) hold over **50+ months of stock**, representing prime candidates for promotional campaigns or paused purchasing.
* **Inter-Store Balancing:** Leveraging store-level visibility allows management to transfer surplus stock between Baldwin, Santa Cruz, and Rowlett before placing external supplier orders.

---

## 🛠️ Tech Stack
* **Data Processing & ML:** Python (`Pandas`, `NumPy`, `Scikit-Learn`, `XGBoost`)
* **Business Intelligence & Visualization:** Tableau Public / Desktop
* **Documentation & Reporting:** Google Slides, Microsoft Word

---

## 👤 Author
**Pablo Ferreira Perales**  
*Business Intelligence & Data Analytics Project*