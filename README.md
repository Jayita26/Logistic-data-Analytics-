# Logistics Performance Analysis and Delivery Delay Prediction

## 📌 Project Overview

This project was developed as part of a **Logistics Data Analyst Internship** to analyze logistics and supply chain performance using Python, perform data cleaning and exploratory analysis, build a predictive model for shipping time, and propose data-driven optimization strategies.

The project follows an end-to-end analytics workflow:

**Data Collection → Data Cleaning → Exploratory Data Analysis → Visualization → Predictive Modeling → Model Evaluation → Optimization Recommendations**

The main objective is to understand delivery performance, identify potential bottlenecks, predict shipping time, and support better logistics decision-making.

---

## 🎯 Project Objectives

* Analyze logistics and delivery performance.
* Identify important logistics KPIs.
* Clean and preprocess raw supply-chain data.
* Explore shipping time, sales, profit, quantity, regions, and shipping modes.
* Identify relationships between logistics variables.
* Visualize operational trends and bottlenecks.
* Build a machine learning model to predict actual shipping time.
* Compare multiple regression models.
* Evaluate model performance using MAE, RMSE, and R².
* Perform cross-validation and hyperparameter tuning.
* Identify high-risk shipping modes and regions.
* Propose resource allocation, scheduling, route-planning, and cost-optimization strategies.

---

## 📊 Dataset

The project uses the **DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS** dataset.

The original dataset contains approximately:

* **180,519 records**
* **56 original columns**
* Order, customer, product, shipping, sales, profit, and delivery-related information.

Important variables include:

* `Days for shipping (real)`
* `Days for shipment (scheduled)`
* `Shipping Mode`
* `Order Region`
* `Market`
* `Order Item Quantity`
* `Order Item Product Price`
* `Order Item Discount`
* `Order Item Total`
* `Order Profit Per Order`
* `Delivery Status`
* `Late_delivery_risk`
* `Customer Segment`
* `Order Status`

### Dataset Sources

* DataCo SMART Supply Chain dataset — Mendeley Data
* DataCo SMART Supply Chain dataset — Kaggle

The raw dataset is not included in the GitHub repository because of file size and data-distribution considerations.

---

# 📅 Project Structure

The project is divided into four internship weeks.

## Week 1 — Strategic Planning and Data Exploration

### Objective

Understand the logistics business problem, define KPIs, and perform initial data exploration.

### KPIs

The following KPIs were considered:

1. On-Time Delivery / Non-Late-Risk Rate
2. Average Actual Shipping Time
3. Average Scheduled Shipping Time
4. Average Schedule Deviation
5. Shipment Volume
6. Total Sales
7. Average Order Profit

### Key Findings

* Total order records: **180,519**
* Unique orders: **65,752**
* Total quantity sold: **384,079**
* Total sales: **33,054,402.38**
* Average actual shipping time: **3.50 days**
* Average scheduled shipping time: **2.93 days**
* Average schedule deviation: **0.57 days**
* Non-late-risk rate: **45.17%**

Shipping-mode analysis showed that **Second Class** and **First Class** had larger average schedule deviations than Standard Class.

---

# 🧹 Week 2 — Data Cleaning and Preprocessing

## Data Quality Assessment

Initial dataset:

* Rows: **180,519**
* Columns: **56**
* Missing values: **336,209**
* Duplicate rows: **0**

### Missing Values

Major missing-value issues were found in:

* `Product Description`
* `Order Zipcode`
* `Customer Lname`
* `Customer Zipcode`

### Cleaning Strategy

* `Product Description` was removed because it was completely missing.
* `Order Zipcode` was removed because of a very high missing-value percentage.
* `Customer Lname` was filled with `"Unknown"`.
* `Customer Zipcode` was filled with `"Unknown"`.
* Duplicate rows were checked and none were found.
* Invalid values were checked.
* Date columns were converted to appropriate datetime formats.

### Feature Engineering

The following features were created:

* Order Year
* Order Month
* Order Day
* Day of Week
* Weekday/Weekend indicator
* Month Name
* Schedule Deviation

The schedule deviation was calculated as:

```text
Schedule Deviation =
Actual Shipping Days - Scheduled Shipping Days
```

### Outlier Analysis

IQR-based outlier detection was performed on important numerical variables.

Outliers were identified in:

* Product Price
* Order Item Total
* Order Profit Per Order

The outliers were **not automatically deleted**, because extreme values may represent legitimate high-value orders or unusual but meaningful business cases.

### Normalization

Min-Max scaling was applied to selected numerical variables for modeling-related analysis.

The original business-analysis dataset was retained separately to preserve interpretability.

Final processed dataset:

* **180,519 rows**
* **58 columns**
* **0 missing values**
* **0 duplicate rows**

---

# 📈 Week 3 — Advanced Data Analysis and Visualization

## Exploratory Data Analysis

The following areas were analyzed:

* Central tendency
* Distributions
* Correlations
* Shipping modes
* Geographic regions
* Sales
* Profit
* Shipping performance
* Schedule deviation

### Central Tendency

| Variable                |   Mean | Median |
| ----------------------- | -----: | -----: |
| Actual Shipping Time    |   3.50 |   3.00 |
| Scheduled Shipping Time |   2.93 |   4.00 |
| Order Quantity          |   2.13 |   1.00 |
| Product Price           | 141.23 |  59.99 |
| Order Item Total        | 183.11 | 163.99 |
| Order Profit            |  21.97 |  31.52 |
| Schedule Deviation      |   0.57 |   1.00 |

### Correlation Analysis

Important correlations included:

* Schedule deviation ↔ Late delivery risk: **0.78**
* Product price ↔ Order total: **0.78**
* Actual shipping time ↔ Schedule deviation: **0.61**
* Actual shipping time ↔ Scheduled shipping time: **0.52**
* Actual shipping time ↔ Late delivery risk: **0.40**

Correlation indicates association and does not prove causation.

### Visualizations

The project includes visualizations for:

* Monthly order volume
* Monthly sales trend
* Shipping-time distribution
* Actual vs scheduled shipping time
* Correlation heatmap
* Shipping-mode delivery risk
* Regional delivery risk
* Numerical-variable distributions

---

# 🤖 Week 4 — Predictive Modeling and Optimization

## Prediction Problem

The predictive modeling problem was defined as:

> **Predict the actual number of days required for a shipment to be delivered.**

### Target Variable

```text
Days for shipping (real)
```

This is a **regression problem** because the target is a numerical value.

---

## Features

The following features were used:

```text
Days for shipment (scheduled)
Shipping Mode
Order Region
Market
Order Item Quantity
Order Item Product Price
Order Item Discount
Order Item Total
Order Profit Per Order
Customer Segment
Order Status
```

Categorical variables were processed using one-hot encoding, while numerical variables were handled separately using a preprocessing pipeline.

---

# 🧠 Machine Learning Models

Three regression models were evaluated:

1. Linear Regression
2. Decision Tree Regressor
3. Random Forest Regressor

### Why Random Forest?

Random Forest was selected as the main candidate because it can:

* Capture nonlinear relationships.
* Handle interactions between variables.
* Work with mixed feature types after preprocessing.
* Provide feature importance.
* Usually perform better than a single decision tree on complex datasets.

---

# 📊 Model Performance

| Model             |        MAE |       RMSE |         R² |
| ----------------- | ---------: | ---------: | ---------: |
| Decision Tree     |     0.9847 |     1.2697 |     0.3884 |
| Random Forest     | **0.9851** | **1.2651** | **0.3928** |
| Linear Regression |     0.9860 |     1.2662 |     0.3918 |

The **Random Forest model** achieved the best overall baseline performance because it had the lowest RMSE and highest R².

---

# 🔄 Cross-Validation

Five-fold cross-validation was performed.

| Model             | Mean CV R² | Std CV R² |
| ----------------- | ---------: | --------: |
| Linear Regression |     0.3917 |    0.0044 |
| Decision Tree     |     0.3878 |    0.0043 |
| Random Forest     | **0.3923** |    0.0046 |

The Random Forest model achieved the highest mean cross-validation R².

The relatively small standard deviation indicates stable performance across folds.

---

# ⚙️ Hyperparameter Tuning

RandomizedSearchCV was used to explore Random Forest hyperparameters.

The faster tuning configuration selected:

```text
n_estimators = 100
max_depth = 10
min_samples_split = 2
min_samples_leaf = 2
```

Tuned model performance:

```text
MAE  = 0.9826
RMSE = 1.2653
R²   = 0.3926
```

### Final Model Decision

The tuned model slightly improved MAE, but the original Random Forest had:

* Lower RMSE
* Higher R²

Therefore, the **original Random Forest model was retained as the final model**.

This avoids claiming that hyperparameter tuning improved overall performance when the improvement was only marginal and metric-specific.

---

# 🔍 Feature Importance

The most important feature in the tuned Random Forest was:

```text
Days for shipment (scheduled) ≈ 92.37%
```

Other important features included:

* Shipping Mode
* Order Profit Per Order
* Order Item Total
* Order Item Discount
* Product Price

Feature importance represents the model's predictive contribution and should not be interpreted as proof of causation.

---

# 🚚 Optimization Analysis

Predictions were used to estimate potential schedule deviations.

The following variables were calculated:

```text
Predicted Shipping Days
Scheduled Shipping Days
Predicted Schedule Deviation
Predicted Delay Days
Predicted Delay Risk
```

### Overall Test Set Results

* Test shipments: **36,104**
* Predicted delay shipments: **22,382**
* Predicted delay rate: **61.99%**
* Average predicted shipping time: **3.50 days**
* Average scheduled shipping time: **2.93 days**
* Average predicted delay: **0.57 days**

These are **model-based predictions**, not historical actual delay rates.

---

# 🚢 Shipping Mode Optimization

| Shipping Mode  | Avg Predicted Shipping | Avg Scheduled | Avg Predicted Delay |
| -------------- | ---------------------: | ------------: | ------------------: |
| First Class    |                   2.00 |          1.00 |                1.00 |
| Same Day       |                   0.48 |          0.00 |                0.48 |
| Second Class   |                   4.00 |          2.00 |                2.00 |
| Standard Class |                   3.99 |          4.00 |                0.01 |

### Key Finding

**Second Class** has the largest predicted schedule gap, approximately **2 days**.

The Same Day result should be interpreted carefully because the dataset uses a scheduled value of zero for this category. Therefore, a 100% predicted gap rate should not be interpreted as evidence that Same Day shipping is operationally 100% late.

---

# 🌍 Regional Optimization

Regions with high model-based predicted delay rates included:

* Central Asia
* Central Africa
* East of USA
* West Africa
* East Africa
* Western Europe
* Southern Africa
* North Africa
* South Asia
* US Center

These results identify areas for further operational investigation. They do not establish that geography itself causes delays.

---

# 💡 Optimization Recommendations

## 1. Dynamic Delivery Scheduling

Use predicted shipping time to create realistic delivery commitments instead of relying only on fixed schedules.

## 2. Risk-Based Shipment Prioritization

Flag shipments with high predicted schedule deviations for early intervention.

Example:

```text
Low Risk      → Normal monitoring
Medium Risk   → Additional monitoring
High Risk     → Priority intervention
```

## 3. Shipping Mode Optimization

Review shipping-mode policies, especially for services showing large predicted schedule gaps.

Second Class shipments should receive particular attention because of the high predicted schedule deviation.

## 4. Regional Resource Allocation

Additional operational resources can be considered for regions with consistently high predicted delay risk.

Possible actions include:

* Additional warehouse capacity
* Better staffing
* Inventory positioning
* Additional carrier capacity
* Improved dispatch planning

## 5. Route Planning

The current dataset does not contain detailed route coordinates, distance, traffic, or road-network information.

Therefore, route optimization is proposed as a future enhancement.

A future system could incorporate:

```text
Distance
Traffic
Weather
Route congestion
Vehicle capacity
Historical travel time
```

to identify efficient routes.

## 6. Cost Minimization

Cost optimization can be integrated by assigning additional resources only to high-risk shipments.

Instead of increasing resources for every shipment:

```text
High-risk shipment
        ↓
Predict delay
        ↓
Estimate operational impact
        ↓
Apply targeted intervention
        ↓
Reduce unnecessary resource cost
```

Actual monetary savings should be calculated only after reliable cost data is available.

## 7. Early-Warning System

The predictive model can be integrated into a logistics dashboard or operational system to identify potentially delayed shipments before delivery.

---

# 🔄 End-to-End Workflow

```text
Raw Logistics Dataset
        ↓
Data Quality Assessment
        ↓
Missing Value Handling
        ↓
Duplicate & Invalid Value Checks
        ↓
Outlier Analysis
        ↓
Feature Engineering
        ↓
Exploratory Data Analysis
        ↓
Data Visualization
        ↓
Feature Preprocessing
        ↓
Train/Test Split
        ↓
Model Training
        ↓
Model Evaluation
        ↓
Cross-Validation
        ↓
Hyperparameter Tuning
        ↓
Final Model Selection
        ↓
Shipping-Time Prediction
        ↓
Delay-Risk Analysis
        ↓
Optimization Recommendations
```

---

# 🛠️ Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Scikit-learn**
* **Jupyter Notebook**
* **Git**
* **GitHub**

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
│   ├── 02_data_cleaning_preprocessing.ipynb
│   ├── 03_advanced_analysis_visualization.ipynb
│   └── 04_predictive_modeling_optimization.ipynb
│
├── visualizations/
│   ├── monthly_order_volume.png
│   ├── monthly_sales_trend.png
│   ├── shipping_time_distribution.png
│   ├── actual_vs_scheduled_shipping.png
│   ├── logistics_correlation_heatmap.png
│   ├── week3_shipping_mode_risk.png
│   ├── week3_top_regions_late_risk.png
│   ├── actual_vs_predicted_shipping_time.png
│   ├── top_15_feature_importance.png
│   ├── predicted_delay_risk_by_shipping_mode.png
│   ├── top_10_predicted_delay_regions.png
│   └── scheduled_vs_predicted_shipping_time.png
│
├── reports/
│   ├── Week_1_Report.docx
│   ├── Week_2_Report.docx
│   ├── Week_3_Report.docx
│   └── Week_4_Report.docx
│
├── src/
│
├── .gitignore
└── README.md
```

---

# 📌 Important Note About Data Files

Large CSV files should not be committed to GitHub.

Add the following to `.gitignore`:

```gitignore
data/*.csv
```

This keeps the repository lightweight while allowing the notebooks and analysis code to remain available.

---

# 📈 Key Business Insights

1. Actual shipping time averages approximately **3.50 days**, compared with a scheduled average of **2.93 days**.
2. Average schedule deviation is approximately **0.57 days**.
3. Schedule deviation has a strong positive association with late-delivery risk.
4. Second Class shipping has the largest predicted schedule gap.
5. Standard Class has the smallest average predicted schedule deviation among the major shipping modes.
6. The Random Forest model achieved the best overall baseline performance among the tested models.
7. Scheduled shipping duration is the dominant predictive feature in the current model.
8. Several regions show high model-based predicted delay risk and should be prioritized for operational investigation.
9. The current model has moderate predictive performance, indicating that additional operational features could improve forecasting.
10. Route, traffic, distance, weather, and carrier information could improve future logistics optimization.

---

# ⚠️ Limitations

* The dataset does not provide detailed route information.
* Traffic and weather information is unavailable.
* Carrier-level information is limited.
* The model predicts shipping duration rather than directly optimizing delivery routes.
* Model-based delay rates should not be treated as actual historical delay rates.
* Feature importance does not establish causal relationships.
* Additional operational features may be required for higher predictive accuracy.

---

# 🚀 Future Improvements

Future versions of the project can include:

* XGBoost or LightGBM regression
* Gradient Boosting models
* Hyperparameter optimization with larger search spaces
* Route optimization algorithms
* Traffic and weather data
* Real-time shipment tracking
* Carrier performance analysis
* Cost-aware optimization
* Power BI logistics dashboard
* FastAPI prediction API
* Automated model monitoring
* Real-time delay alert system

---

# 👩‍💻 Author

**Jayita Maiti**

MSc Data Science Graduate

Project: **Logistics Performance Analysis and Delivery Delay Prediction**

---

## 📜 Internship Context

This project was completed as part of a **Logistics Data Analyst Internship** and demonstrates practical skills in:

* Data Analytics
* Data Cleaning
* Exploratory Data Analysis
* Data Visualization
* Machine Learning
* Regression Modeling
* Model Evaluation
* Predictive Analytics
* Logistics Optimization
* Business Insight Generation
* Python Programming
