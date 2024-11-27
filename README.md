# Project-Trends-in-Waste-Management-Operations
---

## Table of Contents
---

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

---

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
![Line chart](https://github.com/user-attachments/assets/47a288a1-07d0-4c90-b62b-68a29477175f)

This chart illustrates the monthly trends in facility visits, showing a steady increase in visits from January 2022 to a peak in August 2022. Following this peak, visits gradually declined through early 2023, indicating a possible seasonal pattern or reduced demand over time. This trend suggests the need to analyze the factors influencing the rise and fall in visits to optimize resource allocation during peak and off-peak periods

- Which services are most frequently utilized, and how does service usage vary across facilities?
![Stack bar chart](https://github.com/user-attachments/assets/4fa1a281-8eb9-42f3-8c7d-8e08523f2fc8)

This chart highlights the most frequently utilized services across waste facilities based on cost. Tires and hazardous waste services dominate in terms of costs, with variations in usage across facilities. The Tosorontio Waste Facility and Matchedash Waste Facility show higher spending on these services, while other facilities like Oro Waste Facility and North Simcoe Waste Facility exhibit balanced spending across multiple services. This suggests differences in service demand and specialization among facilities.

- How do wait times and visit durations vary by service type?
![Cluster column chart](https://github.com/user-attachments/assets/791dc3a2-5841-4abd-8814-320af452b032)

This chart compares the average wait times and visit durations across different service types. Services such as "Brush," "Garbage," and "Tires" exhibit the highest average visit durations, while wait times remain relatively consistent across all services. This suggests that certain services require more time for completion, potentially due to processing complexity, while wait times are generally well-managed across facilities.

- Which facilities have the highest operational demand, and how does this impact wait times and total service times?
![Cluster bar chart](https://github.com/user-attachments/assets/8d9e2188-993a-42bd-9c19-d6e8221fc9ea)

This chart shows the facilities with the highest operational demand, measured by the count of visits, and the impact on average wait times. Mara Waste Facility has the highest demand with 1,204 visits and a slightly higher average wait time of 9.06 minutes. Tosorontio Waste Facility and Matchedash Waste Facility also experience significant traffic, with average wait times around 8.9 minutes. In contrast, facilities like Collingwood and North Simcoe have lower visit counts and slightly shorter wait times. This indicates that high-demand facilities may face operational bottlenecks, impacting wait times.

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

😄
💻
