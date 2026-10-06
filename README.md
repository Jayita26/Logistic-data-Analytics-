# Logistics Data Analytics

## 📌 Project Overview

This project is an end-to-end **Logistics Data Analytics and Delivery Performance Analysis** project developed as part of a Logistics Data Analyst Internship.

The project focuses on analyzing logistics and supply-chain data to identify delivery performance issues, understand operational patterns, and prepare the dataset for further exploratory analysis, predictive modeling, and optimization.

The project is being developed progressively across four stages:

1. Strategic Planning and Data Exploration
2. Data Collection, Cleaning, and Preprocessing
3. Advanced Data Analysis and Visualization
4. Predictive Modeling and Optimization

---

## 🎯 Project Objectives

The main objectives of this project are to:

* Analyze logistics and supply-chain performance.
* Identify factors associated with delivery delays.
* Calculate important logistics KPIs.
* Clean and preprocess real-world logistics data.
* Handle missing values, duplicates, invalid values, and outliers.
* Perform feature engineering for logistics analysis.
* Prepare data for machine-learning applications.
* Develop visualizations to communicate business insights.
* Build predictive models for delivery-related outcomes.
* Provide data-driven recommendations for logistics improvement.

---

## 📊 Dataset

This project uses the publicly available:

**DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS** dataset.

The dataset contains logistics and supply-chain information including:

* Order information
* Customer information
* Product information
* Shipping modes
* Delivery status
* Shipping time
* Scheduled shipping time
* Sales and profit
* Order regions and countries
* Product quantities
* Delivery-risk indicators

### Dataset Source

DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS:

https://data.mendeley.com/datasets/8gx2fvg2k6/5

The raw dataset is **not included in this GitHub repository** because of its size. It is stored locally and excluded using `.gitignore`.

---

# 📁 Project Structure

```text
logistics-data-analytics/
│
├── data/
│   ├── DataCoSupplyChainDataset.csv
│   ├── DescriptionDataCoSupplyChain.csv
│   └── processed_logistics_data.csv
│
├── notebooks/
│   ├── 01_strategic_planning.ipynb
│   └── 02_data_cleaning_preprocessing.ipynb
│
├── visualizations/
│   ├── late_delivery_risk_by_shipping_mode.png
│   ├── top_10_regions_by_late_delivery_risk.png
│   └── product_price_outliers.png
│
├── reports/
│   ├── Week_1_Strategic_Planning_Report.docx
│   └── Week_2_Data_Cleaning_Preprocessing_Report.docx
│
├── src/
│
├── .gitignore
└── README.md
```

> **Note:** The CSV files are stored locally and are excluded from GitHub through `.gitignore`.

---

# 📅 Week 1 — Strategic Planning and Data Exploration

### Status: ✅ Completed

The first stage focused on understanding the logistics problem, defining KPIs, exploring the dataset, and identifying potential areas for improvement.

## Key Performance Indicators

The following KPIs were defined and analyzed:

* Total Orders
* Total Order Records
* Total Quantity Sold
* Total Sales
* Average Actual Shipping Time
* Average Scheduled Shipping Time
* Schedule Deviation
* On-Time/Non-Late-Risk Rate

## Initial Results

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

> The 45.17% figure is calculated from the `Late_delivery_risk` indicator and represents the non-late-risk category in the dataset. It should not be interpreted as a direct measurement of confirmed on-time delivery.

## Week 1 Analysis

The following analyses were performed:

* Shipping mode analysis
* Regional delivery-risk analysis
* Shipping-time comparison
* Schedule deviation analysis
* KPI calculation
* Initial logistics performance assessment

## Visualizations

### Late Delivery Risk by Shipping Mode

![Late Delivery Risk by Shipping Mode](visualizations/late_delivery_risk_by_shipping_mode.png)

### Top 10 Regions by Late Delivery Risk

![Top 10 Regions by Late Delivery Risk](visualizations/top_10_regions_by_late_delivery_risk.png)

---

# 🧹 Week 2 — Data Collection, Cleaning and Preprocessing

### Status: ✅ Completed

Week 2 focused on preparing the logistics dataset for reliable downstream analytics and machine-learning applications.

## Data Quality Assessment

Initial dataset:

* **Rows:** 180,519
* **Columns:** 56
* **Missing values:** 336,209
* **Duplicate rows:** 0

## Missing Value Handling

Missing values were identified in:

* `Product Description`
* `Order Zipcode`
* `Customer Lname`
* `Customer Zipcode`

The following strategies were applied:

* Dropped `Product Description` because it was completely missing.
* Dropped `Order Zipcode` because of a very high proportion of missing values.
* Filled missing `Customer Lname` values with `"Unknown"`.
* Filled missing `Customer Zipcode` values with `"Unknown"`.

After treatment:

* **Missing values:** 0

## Duplicate Detection

No duplicate rows were found.

```text
Duplicate rows: 0
```

## Invalid Data Detection

The following checks were performed:

* Negative actual shipping days
* Negative scheduled shipping days
* Non-positive order quantities
* Non-positive product prices
* Non-positive order totals

No invalid values were identified.

## Outlier Detection

The **Interquartile Range (IQR)** method was used to identify potential outliers.

Potential outliers were detected in:

* `Order Item Product Price`
* `Order Item Total`
* `Order Profit Per Order`

The outliers were **not automatically removed**, because extreme values may represent legitimate high-value orders, profits, or losses.

## Date Preprocessing

The following date columns were converted to datetime format:

* `order date (DateOrders)`
* `shipping date (DateOrders)`

Additional date features were created:

* `order_year`
* `order_month`
* `order_day`
* `order_day_of_week`
* `order_weekday`
* `order_month_name`

## Schedule Deviation

A new feature was created:

```python
schedule_deviation = (
    df["Days for shipping (real)"]
    - df["Days for shipment (scheduled)"]
)
```

Interpretation:

* Negative value → shipment was faster than scheduled
* Zero → shipment matched the scheduled time
* Positive value → shipment took longer than scheduled

### Final Schedule Deviation

| Statistic |     Value |
| --------- | --------: |
| Mean      | 0.57 days |
| Median    |     1 day |
| Minimum   |   -2 days |
| Maximum   |    4 days |

The average schedule deviation of approximately **0.57 days** indicates that actual shipping time was, on average, higher than the scheduled shipping time.

## Data Normalization

Min-Max normalization was applied to selected numerical features:

```python
from sklearn.preprocessing import MinMaxScaler

scaling_columns = [
    "Days for shipping (real)",
    "Days for shipment (scheduled)",
    "Order Item Product Price",
    "Order Item Quantity",
    "Order Item Total"
]

scaler = MinMaxScaler()

df_scaled = df.copy()

df_scaled[scaling_columns] = scaler.fit_transform(
    df_scaled[scaling_columns]
)
```

Min-Max normalization was selected because the numerical variables have different ranges. Scaling them to a common range of **0 to 1** can help machine-learning algorithms that are sensitive to feature magnitude.

The normalized dataset was maintained separately from the original cleaned dataset so that business analysis can still use the original units.

## Final Week 2 Validation

```text
Rows: 180519
Columns: 58
Missing values: 0
Duplicate rows: 0

Missing order dates: 0
Missing shipping dates: 0
```

The final processed dataset contains **180,519 rows and 58 columns** with no missing values or duplicate rows.

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

# 📈 Project Progress

| Stage                                          | Status      |
| ---------------------------------------------- | ----------- |
| Week 1 — Strategic Planning & Data Exploration | ✅ Completed |
| Week 2 — Data Cleaning & Preprocessing         | ✅ Completed |
| Week 3 — Advanced Analysis & Visualization     | 🔄 Upcoming |
| Week 4 — Predictive Modeling & Optimization    | 🔄 Upcoming |

---

# 🔮 Future Work

The next stages of the project will focus on:

### Week 3 — Advanced Data Analysis and Visualization

Planned activities:

* Exploratory Data Analysis
* Trend analysis
* Regional performance analysis
* Product-level analysis
* Delivery-risk analysis
* Correlation analysis
* Advanced business visualizations
* Identification of operational patterns

### Week 4 — Predictive Modeling and Optimization

Planned activities:

* Feature selection
* Train/test split
* Classification modeling
* Model evaluation
* Delivery-risk prediction
* Feature importance analysis
* Logistics optimization
* Business recommendations

Potential machine-learning models include:

* Logistic Regression
* Decision Tree
* Random Forest
* Other suitable classification algorithms

---

# 📄 Reports

The project documentation is maintained in the `reports/` directory.

### Completed Reports

* `Week_1_Strategic_Planning_Report.docx`
* `Week_2_Data_Cleaning_Preprocessing_Report.docx`

Additional reports will be added as the project progresses.

---

# 📌 Key Learning Outcomes

Through this project, I am developing practical experience in:

* Real-world data cleaning
* Missing-value treatment
* Outlier detection
* Feature engineering
* Data validation
* Exploratory data analysis
* Logistics KPI development
* Data visualization
* Machine-learning preparation
* Business-oriented data interpretation

---

# 👩‍💻 Author

**Jayita Maiti**

MSc Data Science

Aspiring Data Analyst | Data Science | Machine Learning

---

## ⭐ Project Goal

The overall goal of this project is to transform raw logistics data into **actionable business insights and predictive intelligence** that can support better delivery performance, operational efficiency, and supply-chain decision-making.
