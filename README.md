
# 🚖 Navit Transfers — End-to-End Data Engineering & BI Analytics 

## 📌 Project Overview

**Navit Transfers** is an end-to-end Data Engineering and Business Intelligence project built for a tourist transportation platform. 
The project demonstrates the complete analytics lifecycle, starting from raw data cleaning and exploratory data analysis in Python, moving through feature engineering and data modeling, and ending with an interactive Power BI dashboard designed for business decision-making.

The goal of this project is to transform raw operational ride data into a clean, scalable, and analytics-ready **Star Schema** model that supports advanced KPI tracking, fleet monitoring, revenue analysis, and driver performance evaluation.

---

## 🎯 Business Objectives

The main objective of this analytics solution is to help transportation managers and business stakeholders make better operational and strategic decisions.

Key business questions addressed by this project include:

* How much revenue is generated over time?
* Which hours, days, or seasons show the highest ride demand?
* Which drivers perform best based on ride activity and ratings?
* How efficiently is the fleet being used?
* Which routes or customer segments generate the most value?
* How can the business optimize availability, pricing, and resource allocation?

---

## 📊 Key Performance Indicators

The Power BI dashboard focuses on monitoring the following KPIs:

* **Total Revenue**
* **Total Number of Rides**
* **Average Fare Amount**
* **Average Distance per Ride**
* **Peak Ride Hours**
* **Revenue by Time Period**
* **Driver Performance**
* **Fleet Utilization**
* **Customer Ratings and Feedback**
* **User Acquisition Trends**

---

## 🛠️ Tech Stack

| Category                | Tools                            |
| ----------------------- | -------------------------------- |
| Programming Language    | Python 3                         |
| Data Manipulation       | Pandas                           |
| Data Visualization      | Matplotlib, Seaborn              |
| Development Environment | Jupyter Notebook                 |
| Business Intelligence   | Power BI                         |
| Data Modeling           | Star Schema, Kimball Methodology |
| KPI Logic               | DAX                              |
| Data Format             | CSV                              |

---

## 🏗️ Project Architecture

The project follows a structured analytics pipeline:

```text
Raw Data
   ↓
Python Data Cleaning & EDA
   ↓
Feature Engineering
   ↓
Star Schema Modeling
   ↓
CSV Export
   ↓
Power BI Data Model
   ↓
DAX Measures
   ↓
Interactive Dashboard
```

---

## 🔄 Data Pipeline

### 1. Data Cleaning & Exploratory Data Analysis

The raw datasets were cleaned and prepared using Python.

Main cleaning steps included:

* Handling missing values
* Removing duplicate records
* Standardizing column names and formatting
* Cleaning ride logs, user profiles, vehicle details, driver data, and ratings
* Checking data consistency before BI modeling

Initial exploratory data analysis was performed using **Matplotlib** and **Seaborn** to understand distributions, patterns, and business trends.

---

### 2. Feature Engineering

Several new features were created to improve analytical performance and dashboard usability.

Key feature engineering steps:

* Extracted ride dates from `ride_start_time` and `ride_end_time`
* Extracted ride hours from datetime columns
* Extracted registration dates from `registration_date`
* Reduced datetime cardinality for better Power BI performance
* Prepared clean date fields for integration with a dedicated calendar table
* Prepared transactional metrics such as revenue and distance for KPI calculations

Example engineered fields:

```text
ride_start_date
ride_end_date
ride_hour
registration_date_clean
```

---

### 3. Star Schema Data Modeling

To optimize Power BI performance and simplify DAX calculations, the cleaned dataset was transformed into a Star Schema model.

The model separates transactional ride data from descriptive business entities.

#### Fact Table

### `fact_rides`

The central fact table containing ride-level transactional data.

Main fields include:

* `ride_id`
* `user_id`
* `driver_id`
* `vehicle_id`
* `rating_id`
* `ride_start_date`
* `ride_end_date`
* `ride_hour`
* `fare_amount`
* `distance_km`

#### Dimension Tables

### `dim_users`

Contains customer information and user-related attributes.

### `dim_drivers`

Contains driver details, availability, and performance-related attributes.

### `dim_vehicles`

Contains fleet information such as vehicle make, model, year, and specifications.

### `dim_ratings`

Contains ride feedback, rating scores, and customer satisfaction data.

---

## 🧠 Data Model Design

The Power BI model uses active **1-to-Many relationships** between dimension tables and the central fact table.

```text
dim_users      ────┐
dim_drivers    ────┤
dim_vehicles   ────┼── fact_rides
dim_ratings    ────┘
Calendrier     ────┘
```

This structure improves:

* Dashboard performance
* Data consistency
* DAX measure simplicity
* Scalability for future analytics
* Clear separation between facts and dimensions

---

## 📅 Calendar Table

A dynamic calendar table named `Calendrier` was created directly in Power BI using DAX.

The calendar covers the full operational period from **2022 to 2024** and enables time intelligence calculations such as:

* Revenue by year
* Revenue by month
* Revenue by quarter
* Ride trends over time
* Seasonal demand analysis

Example DAX structure:

```DAX
Calendrier =
CALENDAR(
    DATE(2022, 1, 1),
    DATE(2024, 12, 31)
)
```

---

## 📐 DAX Measures

A dedicated `_Measures` table was created in Power BI to centralize all KPI calculations.

Example measures:

```DAX
Total Revenue =
SUM(fact_rides[fare_amount])
```

```DAX
Total Rides =
COUNTROWS(fact_rides)
```

```DAX
Average Fare =
AVERAGE(fact_rides[fare_amount])
```

```DAX
Average Distance =
AVERAGE(fact_rides[distance_km])
```

These measures power the dashboard visuals and provide a clean structure for future KPI expansion.

---

## 📊 Power BI Dashboard

The Power BI dashboard provides a business-friendly overview of transportation operations.

Main dashboard sections include:

* Revenue overview
* Ride volume analysis
* Peak hour analysis
* Driver performance tracking
* Fleet utilization insights
* Customer rating analysis
* Time-based trend monitoring

The dashboard allows stakeholders to quickly identify business patterns, operational bottlenecks, and growth opportunities.

---

## 📂 Repository Structure

```text
├── data/
│   ├── raw/
│   │   └── Original uncleaned datasets
│   │
│   └── PowerBI_Export/
│       ├── fact_rides.csv
│       ├── dim_users.csv
│       ├── dim_drivers.csv
│       ├── dim_vehicles.csv
│       └── dim_ratings.csv
│
├── notebooks/
│   └── GoRide_EDA_Cleaning.ipynb
│
├── dashboards/
│   └── Navit_Analytics.pbix
│
└── README.md
```

---

## 🚀 How to Use This Project

### 1. Clone the Repository

```bash
git clone https://github.com/medincodex/navit-transfers-analytics.git
```

### 2. Open the Notebook

Open the Jupyter Notebook located in:

```text
notebooks/GoRide_EDA_Cleaning.ipynb
```

Run the notebook to review the data cleaning, EDA, and feature engineering process.

### 3. Load the Power BI Files

Open the Power BI dashboard file:

```text
dashboards/Navit_Analytics.pbix
```

### 4. Review the Data Model

Inside Power BI:

* Check the relationships between fact and dimension tables
* Review the `Calendrier` table
* Review the `_Measures` table
* Explore dashboard visuals and KPIs

---

## ✅ Project Outcomes

This project successfully delivers:

* A cleaned and structured transportation dataset
* A scalable Star Schema model
* Optimized CSV files for Power BI
* A dedicated calendar table for time intelligence
* Centralized DAX measures
* An interactive dashboard for business insights
* A complete analytics workflow from raw data to BI reporting

---

## 📌 Skills Demonstrated

This project highlights practical skills in:

* Data cleaning with Python
* Exploratory Data Analysis
* Feature engineering
* Data modeling
* Star Schema design
* Power BI dashboarding
* DAX measure creation
* Business KPI analysis
* Data storytelling
* End-to-end analytics project development

---

## 🧩 Future Improvements

Potential future enhancements include:

* Adding route-level profitability analysis
* Creating advanced driver ranking metrics
* Adding geospatial analysis for pickup and drop-off locations
* Building automated data refresh workflows
* Adding predictive analytics for demand forecasting
* Deploying the dashboard to Power BI Service
* Adding row-level security for different business users

---

## 👤 Author med marra

**Project:** Navit Transfers Analytics
**Type:** Data Engineering & Business Intelligence Project
**Tools:** Python, Pandas, Power BI, DAX, Star Schema

---

## ⭐ Conclusion

Navit Transfers demonstrates how raw transportation data can be transformed into a reliable business intelligence system.
By combining Python-based data preparation, Star Schema modeling, and Power BI dashboarding, this project provides actionable insights for revenue monitoring, fleet optimization, driver performance tracking, and operational decision-making.

