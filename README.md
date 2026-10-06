# Logistics Data Analytics

## 📌 Project Overview

This project is an end-to-end logistics data analytics project developed as part of the **YuvaIntern Logistics Data Analyst Internship**.

The project analyzes supply-chain and logistics data to understand delivery performance, shipping efficiency, regional patterns, sales, profitability, and delivery-risk indicators. The project progressively moves from **strategic planning and data exploration → data cleaning and preprocessing → advanced analysis and visualization → predictive modeling and optimization**.

### Project Title

**Logistics Performance Analysis and Delivery Delay Prediction**

---

## 🎯 Project Objectives

* Analyze logistics and supply-chain performance using Python.
* Identify delivery delays and operational bottlenecks.
* Evaluate shipping-mode and regional performance.
* Perform data cleaning and preprocessing.
* Conduct exploratory and advanced data analysis.
* Build meaningful logistics visualizations.
* Identify relationships between operational variables.
* Develop predictive models for delivery risk in Week 4.
* Support data-driven logistics decision-making.

---

## 📊 Dataset

The project uses the publicly available:

**DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS**

Dataset source:

https://data.mendeley.com/datasets/8gx2fvg2k6/5

The dataset contains information related to:

* Orders
* Customers
* Products
* Shipping
* Delivery performance
* Sales
* Profit
* Regions
* Shipping modes
* Delivery-risk indicators
* Order dates and shipping dates

### Dataset Size

After preprocessing:

* **Rows:** 180,519
* **Columns:** 58
* **Missing values:** 0
* **Duplicate rows:** 0

> Raw and processed CSV files are excluded from GitHub to avoid unnecessarily committing large datasets.

---

# 📁 Project Structure

```text
logistics-data-analytics/
│
├── data/
│   └── Dataset files (stored locally and excluded from GitHub)
│
├── notebooks/
│   ├── 01_strategic_planning.ipynb
│   ├── 02_data_cleaning_preprocessing.ipynb
│   └── 03_advanced_analysis_visualization.ipynb
│
├── visualizations/
│   ├── late_delivery_risk_by_shipping_mode.png
│   ├── top_10_regions_by_late_delivery_risk.png
│   ├── product_price_outliers.png
│   ├── monthly_order_volume.png
│   ├── monthly_sales_trend.png
│   ├── shipping_time_distribution.png
│   ├── actual_vs_scheduled_shipping.png
│   ├── logistics_correlation_heatmap.png
│   ├── distribution_days_for_shipping_real.png
│   ├── distribution_order_item_quantity.png
│   ├── distribution_order_item_product_price.png
│   ├── distribution_order_item_total.png
│   ├── distribution_order_profit_per_order.png
│   ├── week3_shipping_mode_risk.png
│   └── week3_top_regions_late_risk.png
│
├── reports/
│   ├── Week_1_Strategic_Planning_Report.docx
│   ├── Week_2_Data_Cleaning_Preprocessing_Report.docx
│   └── Week_3_Advanced_Data_Analysis_and_Visualization_Report.docx
│
├── src/
│
├── .gitignore
└── README.md
```

---

# 📅 Week 1 — Strategic Planning and Data Exploration

### Status: ✅ Completed

Week 1 focused on understanding the logistics problem, defining KPIs, exploring the dataset, and developing an analytical roadmap.

### Key KPIs

* Total Orders
* Total Order Records
* Total Quantity Sold
* Total Sales
* Average Actual Shipping Time
* Average Scheduled Shipping Time
* Schedule Deviation
* On-Time/Non-Late-Risk Rate

### Key Results

| KPI                             |        Result |
| ------------------------------- | ------------: |
| Total Orders                    |        65,752 |
| Total Order Records             |       180,519 |
| Total Quantity Sold             |       384,079 |
| Total Sales                     | 33,054,402.38 |
| Average Actual Shipping Time    |     3.50 days |
| Average Scheduled Shipping Time |     2.93 days |
| Average Schedule Deviation      |     0.57 days |
| On-Time/Non-Late-Risk Rate      |        45.17% |

The Week 1 analysis also compared shipping modes and regions to identify potential delivery-performance issues.

---

# 🧹 Week 2 — Data Cleaning and Preprocessing

### Status: ✅ Completed

Week 2 focused on building a reliable preprocessing pipeline for logistics analysis.

### Data Quality Checks

Initial dataset:

* Rows: 180,519
* Columns: 56
* Missing values: 336,209
* Duplicate rows: 0

### Missing-Value Handling

The following issues were identified:

* `Product Description` — 100% missing
* `Order Zipcode` — high percentage of missing values
* `Customer Lname` — small number of missing values
* `Customer Zipcode` — small number of missing values

The preprocessing workflow:

* Removed unsuitable high-missing-value columns.
* Replaced remaining missing categorical/value entries with `"Unknown"`.
* Checked for duplicate records.
* Checked for invalid numerical values.
* Investigated numerical outliers using the IQR method.
* Converted date columns to datetime format.
* Created useful time-based features.
* Created `schedule_deviation`.

### Final Validation

* **Rows:** 180,519
* **Columns:** 58
* **Missing values:** 0
* **Duplicate rows:** 0
* **Missing order dates:** 0
* **Missing shipping dates:** 0

### Schedule Deviation

```text
schedule_deviation =
Days for shipping (real)
-
Days for shipment (scheduled)
```

Interpretation:

* Negative → shipment was faster than scheduled
* Zero → shipment matched schedule
* Positive → shipment took longer than scheduled

Final average schedule deviation:

**0.57 days**

---

# 📈 Week 3 — Advanced Data Analysis and Visualization

### Status: ✅ Completed

Week 3 focused on advanced exploratory analysis, visualization, and business interpretation.

### Analysis Performed

* Descriptive statistics
* Mean, median, and standard deviation
* Distribution analysis
* Monthly trend analysis
* Correlation analysis
* Shipping-mode performance analysis
* Regional performance analysis
* Sales and profitability analysis
* Schedule-deviation analysis
* Delivery-risk analysis

### Overall EDA Results

| Metric                       |        Result |
| ---------------------------- | ------------: |
| Total Orders                 |        65,752 |
| Total Sales                  | 33,054,402.38 |
| Average Shipping Time        |     3.50 days |
| Average Scheduled Time       |     2.93 days |
| Average Schedule Deviation   |     0.57 days |
| Average Order Quantity       |          2.13 |
| Average Product Price        |        141.23 |
| Average Order Profit         |         21.97 |
| Late Delivery Risk Indicator |        54.83% |

> The 54.83% value is based on the dataset's `Late_delivery_risk` indicator and is interpreted as a risk indicator rather than independent confirmation of actual late deliveries.

---

## 🚚 Shipping Mode Analysis

| Shipping Mode  | Actual Days | Scheduled Days | Schedule Deviation | Late-Risk Indicator |
| -------------- | ----------: | -------------: | -----------------: | ------------------: |
| First Class    |        2.00 |           1.00 |              +1.00 |              95.32% |
| Same Day       |        0.48 |           0.00 |              +0.48 |              45.74% |
| Second Class   |        3.99 |           2.00 |              +1.99 |              76.63% |
| Standard Class |        4.00 |           4.00 |              ~0.00 |              38.07% |

### Key Insight

First Class and Second Class show substantially higher risk indicators and positive schedule deviations.

Second Class has the largest average schedule deviation:

**+1.99 days**

Standard Class has the largest shipment volume and shows close alignment between actual and scheduled shipping time.

---

## 🌍 Regional Analysis

The top-risk regional analysis identified:

| Region         | Shipments | Avg. Deviation | Late-Risk |
| -------------- | --------: | -------------: | --------: |
| Central Africa |     1,677 |           0.64 |    57.96% |
| South Asia     |     7,731 |           0.60 |    56.27% |
| East Africa    |     1,852 |           0.57 |    55.94% |
| Western Europe |    27,109 |           0.60 |    55.85% |
| South of USA   |     4,045 |           0.58 |    55.77% |

Central Africa has the highest late-risk indicator among the top 10 regions.

Western Europe is particularly important because of its high shipment volume and approximately **5.30 million** in sales.

---

## 🔗 Correlation Analysis

Important relationships identified:

| Variables                               | Correlation |
| --------------------------------------- | ----------: |
| Schedule Deviation ↔ Late Delivery Risk |    **0.78** |
| Product Price ↔ Order Total             |    **0.78** |
| Actual Shipping ↔ Schedule Deviation    |    **0.61** |
| Actual Shipping ↔ Scheduled Shipping    |    **0.52** |
| Product Price ↔ Discount                |    **0.49** |
| Actual Shipping ↔ Late Delivery Risk    |    **0.40** |

### Key Insight

The strongest identified operational relationship was between:

**Schedule Deviation and Late_delivery_risk → 0.78**

This indicates a strong positive association, although correlation alone does not establish causation.

---

# 📊 Week 3 Visualizations

The project includes visualizations covering:

* Monthly order volume
* Monthly sales trend
* Shipping-time distribution
* Order quantity distribution
* Product-price distribution
* Order-total distribution
* Profit distribution
* Actual vs scheduled shipping time
* Correlation heatmap
* Late-delivery risk by shipping mode
* Top regions by late-delivery risk

These visualizations were created using **Matplotlib and Seaborn**.

---

# 💡 Business Insights

The analysis identified several important operational insights:

1. Shipping-mode performance varies considerably.
2. First Class has a very high delivery-risk indicator relative to its one-day schedule.
3. Second Class has the largest positive schedule deviation.
4. Standard Class shows comparatively strong schedule alignment despite handling the largest volume.
5. Schedule deviation has a strong association with the delivery-risk indicator.
6. High-volume regions should be prioritized because improvements can affect a larger number of shipments.
7. Product price has a strong positive relationship with order total.
8. Profit per order shows substantial variability, suggesting opportunities for deeper profitability analysis.

---

# 🎯 Recommendations

Based on the analysis:

* Review First Class and Second Class scheduling assumptions.
* Monitor schedule deviation as an important logistics KPI.
* Investigate high-risk shipping modes.
* Prioritize high-volume regions for operational improvements.
* Evaluate delivery performance together with shipment volume and sales.
* Investigate profitability and pricing patterns.
* Use the Week 3 findings as features and business context for predictive modeling.

---

# 🤖 Week 4 — Predictive Modeling and Optimization

### Status: 🔜 Upcoming

The next stage of the project will focus on:

* Feature selection
* Preparing data for machine learning
* Delivery-risk prediction
* Classification models
* Model evaluation
* Feature importance
* Predictive insights
* Logistics optimization recommendations

Potential models include:

* Logistic Regression
* Decision Tree
* Random Forest
* Other suitable classification algorithms

The objective is to move from **descriptive analytics to predictive analytics and decision support**.

---

# 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook
* Git
* GitHub

---

# 📚 Project Learning Outcomes

Through this project, I developed practical experience in:

* Logistics data analysis
* Data cleaning
* Missing-value handling
* Outlier detection
* Feature engineering
* Exploratory Data Analysis
* Statistical summaries
* Correlation analysis
* Data visualization
* Business KPI analysis
* Operational bottleneck identification
* Data-driven decision-making
* Machine-learning preparation

---

# 📑 Reports

The project reports are maintained in the `reports/` directory:

* **Week 1:** Strategic Planning and Data Exploration
* **Week 2:** Data Cleaning and Preprocessing
* **Week 3:** Advanced Data Analysis and Visualization

---

# 📌 Project Progress

| Week   | Task                                  | Status      |
| ------ | ------------------------------------- | ----------- |
| Week 1 | Strategic Planning & Data Exploration | ✅ Completed |
| Week 2 | Data Cleaning & Preprocessing         | ✅ Completed |
| Week 3 | Advanced Analysis & Visualization     | ✅ Completed |
| Week 4 | Predictive Modeling & Optimization    | 🔜 Upcoming |

---

# 👩‍💻 Author

**Jayita Maiti**

MSc Data Science Graduate

### Career Goal

Aspiring **Data Analyst / Data Science Professional**, with a focus on Python, SQL, Power BI, data analytics, machine learning, and business intelligence.

---

## ⭐ Project Goal

The long-term goal of this project is to develop an end-to-end logistics analytics solution that can transform raw supply-chain data into **actionable insights, predictive delivery-risk models, and optimization-oriented business recommendations**.
