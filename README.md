# Logistics Performance Analysis and Delivery Delay Prediction

An end-to-end logistics data analytics project focused on analyzing supply chain performance, identifying delivery-risk patterns, and developing data-driven insights for logistics decision-making.

This project is being developed as part of a **Logistics Data Analyst Internship**.

---

## 📌 Project Objective

The main objective of this project is to analyze logistics and supply chain data to:

* Evaluate delivery performance
* Identify potential delivery-risk patterns
* Compare different shipping modes
* Analyze regional logistics performance
* Calculate important logistics KPIs
* Generate actionable business insights
* Build a foundation for predictive delivery-risk analysis

---

## 📊 Dataset

The project uses the **DataCo SMART Supply Chain for Big Data Analysis** dataset.

The dataset contains information related to:

* Orders
* Customers
* Products
* Sales
* Shipping
* Delivery performance
* Shipping modes
* Geographical regions

### Important Variables

Some of the variables used in the analysis include:

* `Order Id`
* `Order Region`
* `Shipping Mode`
* `Days for shipping (real)`
* `Days for shipment (scheduled)`
* `Delivery Status`
* `Late_delivery_risk`
* `Order Item Quantity`
* `Order Item Total`
* `Order Item Product Price`

### Dataset Source

The dataset is publicly available from:

* Mendeley Data: DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS
* Kaggle: DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS

The raw dataset is not included in this repository.

---

# 📈 Week 1 — Strategic Planning and Data Exploration

## Key Performance Indicators

The following KPIs were identified:

1. Total Orders
2. Total Order Records
3. Total Quantity Sold
4. Total Sales
5. Average Actual Shipping Time
6. Average Scheduled Shipping Time
7. Average Schedule Deviation
8. On-Time/Non-Late-Risk Rate

---

## 🔎 Initial Findings

The initial analysis produced the following results:

| Metric                          |        Result |
| ------------------------------- | ------------: |
| Unique Orders                   |        65,752 |
| Order Records                   |       180,519 |
| Total Quantity Sold             |       384,079 |
| Total Sales                     | 33.05 million |
| Average Actual Shipping Time    |     3.50 days |
| Average Scheduled Shipping Time |     2.93 days |
| Average Schedule Deviation      |     0.57 days |
| On-Time/Non-Late-Risk Rate      |        45.17% |

> **Note:** The 45.17% value is calculated using the `Late_delivery_risk` indicator. It should not be interpreted as a direct measurement of actual delivery status.

---

## 🚚 Shipping Mode Analysis

The initial analysis showed differences in late-delivery risk across shipping modes.

| Shipping Mode  | Shipments | Late-Risk Rate |
| -------------- | --------: | -------------: |
| First Class    |    27,814 |         95.32% |
| Same Day       |     9,737 |         45.74% |
| Second Class   |    35,216 |         76.63% |
| Standard Class |   107,752 |         38.07% |

First Class showed the highest late-delivery-risk rate in the dataset, while Standard Class showed the lowest among the four major shipping modes.

---

## 🌍 Regional Analysis

Regional performance was also analyzed to identify areas with relatively higher delivery risk.

The analysis highlighted regions such as:

* Central Africa
* South Asia
* East Africa
* Western Europe
* South of USA

as areas requiring further investigation.

---

## 📊 Visualizations

Week 1 includes visualizations for:

* Late Delivery Risk by Shipping Mode
* Top 10 Regions by Late Delivery Risk

Additional visualizations will be added in later stages of the project.

---

# 🧠 Data Science Approach

The project will progressively explore:

### Exploratory Data Analysis

Used to identify patterns, trends, and operational bottlenecks.

### Classification

Will be explored for predicting delivery-delay risk.

### Regression

Can be used to predict continuous outcomes such as delivery time or cost.

### Clustering

Can be used to group regions, customers, or orders with similar logistics characteristics.

### Optimization

Can be explored for shipping-mode selection, resource allocation, and delay reduction.

---

# 🗺️ Project Roadmap

| Stage  | Activity                              | Status         |
| ------ | ------------------------------------- | -------------- |
| Week 1 | Strategic Planning & Data Exploration | ✅ Completed    |
| Week 2 | Data Cleaning & Preprocessing         | 🔄 In Progress |
| Week 3 | Advanced Analysis & Visualization     | ⏳ Planned      |
| Week 4 | Predictive Modeling & Optimization    | ⏳ Planned      |

---

# 🛠️ Technologies

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

# 📁 Current Project Structure

```text
logistics-data-analytics/
│
├── data/
│   └── Raw dataset files
│
├── notebooks/
│   └── 01_strategic_planning.ipynb
│
├── visualizations/
│
├── reports/
│
├── .gitignore
└── README.md
```

---

# 👩‍💻 Author

**Jayita Maiti**

MSc Data Science — 2026

Interested in Data Analytics, Business Intelligence, Machine Learning, and AI/ML Engineering.

---

## 📌 Project Status

**Current Stage: Week 2 — Data Cleaning & Preprocessing**

Week 1 has been completed. The project will be updated as the remaining internship tasks are completed.
