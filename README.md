# ✈️ SFO Airport Lakehouse  
### Passenger & Landings Analytics

A **lakehouse-style data engineering project** that transforms public San Francisco International Airport (SFO) passenger and aircraft landing data into a **reusable, analytics-ready cloud data warehouse** using **Google BigQuery, Python, and CouchDB**.

---

## 📌 Project Overview

San Francisco International Airport publishes monthly statistics on passengers and landings, but these datasets are often analyzed through ad-hoc spreadsheets, making KPIs hard to reproduce and compare over time.

This project converts two public SFO datasets into a **modern lakehouse architecture**, enabling:
- Consistent KPI definitions  
- Historical trend analysis  
- Scalable analytics for airport planning decisions  

---

## 🎯 Objectives

- Integrate passenger and landing datasets at a **monthly grain**
- Design a reusable **star schema** with conformed dimensions
- Implement a **three-layer lakehouse architecture**
- Build analytics-ready **gold data marts**
- Define and standardize a key KPI: **Passengers per Landing**
- Demonstrate **SQL + NoSQL integration** using CouchDB

---

## 📂 Datasets Used

- **Air Traffic Passenger Statistics** (DataSF)
- **Air Traffic Landings Statistics** (DataSF)
- Time Range: **1999 – Present**
- Granularity: **Monthly**

---

## 🏗️ Architecture Overview

The project follows a **lakehouse-style design** within Google BigQuery:
Raw Layer → Core Layer → Marts Layer
(sfo_raw) (sfo_core) (sfo_marts)

---

### Layer Responsibilities
- **Raw:** Source-aligned tables loaded directly from CSV and CouchDB  
- **Core:** Cleaned star schema with facts and conformed dimensions  
- **Marts:** Business-ready tables with embedded KPIs and rules  

---

## 🧱 Data Modeling

### Conformed Dimensions
- Date
- Airline (Operating & Published)
- Geography
- Terminal & Boarding Area
- Activity Type (Enplaned, Deplaned, Transit)
- Aircraft
- Price Category

### Fact Tables
- `fact_passenger_monthly`
- `fact_landings_monthly`

All facts share conformed dimensions to ensure consistent analytics.

---

## 📊 Analytics Marts

Four **gold marts** are built on top of the core schema:

1. **Airline & Region Mix**  
   Passenger distribution by airline and geographic region

2. **Terminal Load**  
   Passenger volume by terminal and boarding area

3. **Passengers per Landing (Main KPI)**  
   Measures demand relative to aircraft operations

4. **Fleet Mix**  
   Trends in wide-body vs narrow-body aircraft usage

---

## 🔑 Key KPI: Passengers per Landing

A centralized KPI combining passenger demand and landing activity:
Passengers per Landing = Total Passengers (excluding transit) ÷ Total Landings

---


### Observed Insights
- Stable values before 2020  
- Sharp collapse during COVID  
- Gradual but incomplete recovery post-2021  

Defining this KPI once in a mart ensures **consistent interpretation across analyses**.

---

## 🧠 NoSQL Integration (CouchDB)

To demonstrate hybrid data architectures:

- Passenger records are exported as **JSON documents** to CouchDB
- Map/Reduce views aggregate:
  - Passengers by airline
  - Passengers by region
- Aggregated results are reloaded into BigQuery
- Validates **round-trip integrity** between SQL and NoSQL systems

This shows how document stores can **complement**, not replace, analytical warehouses.

---

## 🛠️ Tools & Technologies

- **Cloud Data Warehouse:** Google BigQuery
- **ETL & Analytics:** Python, Pandas, Google Colab
- **SQL Modeling:** BigQuery SQL
- **NoSQL Database:** CouchDB (Docker-based)
- **Visualization:** Matplotlib
- **Diagrams:** Mermaid
- **Version Control:** GitHub

---

## 📈 Key Findings

- SFO operates as a **United Airlines hub**
- Terminal **3-F** and **International-G** handle the highest passenger volumes
- Passenger-per-landing KPI clearly reflects COVID disruption
- Narrow-body aircraft dominate domestic traffic patterns

---

## 📁 Repository Structure

sfo-airport-lakehouse-analytics/
│
├── data/
│   ├── raw/
│   │   ├── Air_Traffic_Passenger_Statistics.csv
│   │   └── Air_Traffic_Landings_Statistics.csv
│   │
│   └── README.md
│
├── notebooks/
│   ├── etl_csv_to_bigquery.ipynb
│   ├── analytics_airline_mix.ipynb
│   ├── analytics_terminal_load.ipynb
│   ├── analytics_passengers_per_landing.ipynb
│   └── analytics_fleet_mix.ipynb
│
├── sql/
│   ├── core_dimensions/
│   │   ├── dim_date.sql
│   │   ├── dim_airline.sql
│   │   ├── dim_geo.sql
│   │   ├── dim_terminal.sql
│   │   ├── dim_aircraft.sql
│   │   └── dim_activity.sql
│   │
│   ├── core_facts/
│   │   ├── fact_passenger_monthly.sql
│   │   └── fact_landings_monthly.sql
│   │
│   └── marts/
│       ├── mart_airline_mix.sql
│       ├── mart_terminal_load.sql
│       ├── mart_passengers_per_landing.sql
│       └── mart_fleet_mix.sql
│
├── nosql/
│   ├── couchdb_setup.md
│   ├── passengers_to_couchdb.py
│   └── couchdb_views.json
│
├── diagrams/
│   ├── star_schema.png
│   └── pipeline_architecture.png
│
├── report/
│   └── Airport_Operations_Lakehouse_SFO.pdf
│
├── README.md
├── .gitignore
└── LICENSE


---

## 📄 Project Report

📎 **Full academic report:**  
`report/Airport_Operations_Lakehouse_SFO.pdf`

---


## ⭐ Why This Project Matters

This project demonstrates:
- Real-world **data warehouse & lakehouse design**
- End-to-end **ETL and analytics engineering**
- KPI standardization for decision-making
- Practical **SQL + NoSQL integration**

It reflects skills expected in **Data Engineer, Analytics Engineer, and BI Engineer** roles.

---

