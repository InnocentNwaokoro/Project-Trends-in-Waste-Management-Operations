# Project-Trends-in-Waste-Management-Operations

## Table of Contents

- [Project Overview](#project-Overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-Cleaning/Preparation)
- [Exploratory Data Analysis](#exploratory-Data-Analysis)
- [Data Analysis](#data-Analysis)
- [Results/Findings](#results/Findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [Refrences](#refrences)

### Project Overview

This data analysis project aims to explore and analyze operational trends in waste management facilities, focusing on service usage, wait times, costs, and site-specific performance. The goal is to derive actionable insights for optimizing operations and improving service efficiency.

### Data Sources

The dataset, originally sourced from the "environmental_sanitation_unit.csv" file, includes detailed information about waste management operations across multiple facilities.

### Tools

- Excel - Data Cleaning
- SQL Server - Data Analysis
- PowerBI - Creaing a Reports


### Data Cleaning/Preparation

In the initial data preparation phase, i performed the following tasks:
1. Data loading and inspection.
2. Handling Missing Values.
3. Removing Duplicates.
4. Outlier detection and removal of outliers
5. Data Aggregation
6. Validating Data Consistency


### Exploratory Data Analysis

EDA involved exploring the Trends in Waste Management Operations

- What are the monthly and yearly trends in the number of visits across waste management facilities?
- Which services are most frequently utilized, and how does service usage vary across facilities?
- How do wait times and visit durations vary by service type?
- Which facilities have the highest operational demand, and how does this impact wait times and total service times?

### Data Analysis

~~~sql
CREATE TABLE master_table_dashboard (
    site_name VARCHAR(100),
    decommission_date DATE,
    cost DECIMAL(10, 2),
    service_used_label VARCHAR(100),
    visit_date DATE,
    visit_time TIME,
    wait_length DECIMAL(8, 2),
    visit_length DECIMAL(8, 2),
    visit_id INT,
    service_id INT
);
-- Data into the master table from the existing tables
INSERT INTO master_table_dashboard (
    site_name,
    decommission_date,
    cost,
    service_used_label,
    visit_date,
    visit_time,
    wait_length,
    visit_length,
    visit_id,
    service_id
)
SELECT 
    l.site_name,
    l.decommission_date,
    s.cost,
    su.service_used_label,
    v.visit_date,
    v.visit_time,
    v.wait_length,
    v.visit_length,
    v.visit_id,
    s.service_id
FROM services s
JOIN visits v ON s.visit_id = v.visit_id
JOIN Location_table l ON v.site_id = l.site_id
JOIN service_used su ON s.service_used_id = su.service_used_id;

SELECT *
from master_table_dashboard;
~~~

### Results/Findings
The analysis results are summarised as follows:
1. The analysis revealed consistent growth in visits to waste management facilities, with seasonal peaks likely driven by periodic cleaning or disposal needs.
2. Recyclables and hazardous waste services were the most frequently utilized, reflecting their importance in waste management operations.
3. Hazardous waste handling exhibited longer wait and visit durations, likely due to the complexity and resources required for processing.
4. High-demand facilities experienced longer service times, highlighting potential bottlenecks during peak periods and the need for operational improvements.


### Recommendations

Based on my analysis, i recommend the following actions:
- Allocate additional resources and staff to high-demand facilities during peak periods to reduce bottlenecks.
- Streamline hazardous waste handling through advanced equipment or specialized training to minimize delays.
- Expand capacity or redistribute traffic to underutilized facilities to balance demand.
- Use data-driven insights to predict peak periods and optimize resource allocation effectively.

### Limitations

In my analysis faced limitations due to missing data, lack of user demographics or geographic details, unclear outliers, and the dataset's static nature, which restricted real-time trend evaluation.

### Refrences

1. SQL for Environmental Health and Safety.
2. [Oracle Community](https://community.oracle.com/customerconnect/discussion/604994/sql-for-environmental-health-and-safety)
