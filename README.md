# Cyclistic Bike Share Analysis

This repository contains my capstone project for the **Google Data Analytics Professional Certificate**.
The objective of this case study is to analyze how **casual riders and annual members use Cyclistic bikes differently** and provide data-driven insights to help the marketing team convert casual riders into annual members.

The project follows the **Google Data Analytics framework**:

**[Ask](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/01_ASK_business_problem.md) → [Prepare](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/02_PREPARE_data_overview.md) → [Process](https://github.com/Swam80/Cyclistic-Bike-Share/tree/main/03_PROCESS_sql_cleaning) → [Analyze](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/04_ANALYZE/analysis_findings.md) → [Share](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/05_Share/BI%20working.md)**

The analysis was conducted using **Google BigQuery** for data processing and **Microsoft Power BI** for visualization.

---

# Business Objective

Cyclistic’s marketing team wants to increase revenue by converting **casual riders** into **annual members**.

This project analyzes historical ride data to answer the key question:

> **How do casual riders and annual members use Cyclistic bikes differently?**

Understanding these behavioral differences can help design targeted marketing strategies that encourage membership conversion.

---

# Tools Used

* **SQL** – Data cleaning and transformation
* **Google BigQuery** – Data storage and querying
* **Microsoft Power BI** – Dashboard creation and visualization
* **Markdown** – Documentation and reporting
* **GitHub** – Project version control and portfolio presentation

---

# Repository Structure

```
Cyclistic-Bike-Share
│
├── 01_ASK_business_problem.md
│   Defines the business problem and key analytical questions.
│
├── 02_PREPARE_data_overview.md
│   Describes the dataset, data sources, and credibility assessment.
│
├── 03_PROCESS_sql_cleaning/
│   SQL queries used to clean, validate, and prepare the dataset.
│
├── 04_ANALYZE/
│   Exploratory analysis, aggregated metrics, and insights derived from the data.
│
├── 05_Share/
│   Power BI dashboard development and visualization documentation.
│
└── README.md
    Project overview and documentation.
```

---

# Dataset

The dataset consists of **12 months of Cyclistic trip data**, containing millions of ride records with fields such as:

* Ride ID
* Bike type
* Start and end timestamps
* Start and end stations
* Rider type (member or casual)

The raw monthly CSV files were combined, cleaned, and transformed using SQL before analysis.

---

# Key Analysis Areas

The analysis focuses on identifying behavioral differences between rider types:

* Ride volume comparison
* Ride share distribution
* Average ride duration
* Temporal usage patterns

These insights help understand how casual riders differ from annual members in their usage behavior.

---

# Dashboard [Github Link](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/05_Share/BI%20working.md)

A dashboard was created in **Microsoft Power BI** to visualize key metrics such as:

* Ride share between members and casual riders
* Average ride duration comparison
* Behavioral insights for marketing strategy

The dashboard is designed to support data-driven decision-making for Cyclistic’s marketing team.

---

# Project Outcome

This project demonstrates an **end-to-end data analytics workflow**, including:

* Data preparation and validation
* SQL-based data transformation
* Exploratory data analysis
* Business-focused visualization
* Strategic insights and recommendations

---

# Author

**Swamesh Lotlikar**

This project is part of my portfolio showcasing practical applications of data analytics concepts and tools learned through the Google Data Analytics Professional Certificate.
