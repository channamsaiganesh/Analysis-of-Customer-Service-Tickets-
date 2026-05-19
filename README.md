# 📊 Customer Service Tickets Analysis Dashboard

A comprehensive Power BI project that analyzes customer service and network incident tickets to uncover operational trends, SLA compliance, root causes, and team performance. This dashboard transforms raw ticketing data into actionable insights to support better decision-making and improve customer service reliability.

---

## 📌 Project Overview

This project focuses on analyzing customer service and telecom incident tickets using Power BI.

### 🎯 Objectives

- Track ticket volume trends over time
- Monitor Service Level Agreement (SLA) adherence
- Identify frequently occurring issues and root causes
- Evaluate team performance and resolution efficiency
- Improve customer experience and service reliability

---

## 📂 Dataset Overview

The dataset was compiled from three monthly Excel files exported from the Telecom Incident Ticketing System.

### 📁 Source Files

- `Oct24.xlsx`
- `Nov24.xlsx`
- `Dec24.xlsx`

### 📊 Dataset Summary

| Metric | Value |
|------:|:------|
| Total Tickets | 3,051 |
| Time Period | October 2024 – December 2024 |
| Data Format | One row per ticket |
| Source System | Telecom Incident Ticketing System |

### 🏷️ Key Columns

- Ticket Number
- Created Date
- Closed Date
- Ticket Status
- Severity / Priority
- SLA Status
- Root Cause
- Assigned Team

---

# 🧹 Data Cleaning Process (Power Query)

All data cleaning and transformation were performed using the Power Query Editor in Power BI.

## 1️⃣ Data Loading and Header Preparation

- Imported all three monthly files
- Promoted first row to headers

## 2️⃣ Schema Standardization

The three files had different structures:

| File | Columns |
|------|--------:|
| Oct24 | 34 |
| Nov24 | 25 |
| Dec24 | 30 |

### Common Columns Retained

- 27 standardized columns were identified across all files.

### Removed Columns

- Provider
- Fault Area Detail
- WBU-Customer Type
- Closed By Group
- Network

### Reasons for Removal

- Inconsistent across files
- High percentage of null values
- Low analytical value

## 3️⃣ Month Identifier and Data Appending

- Added a `Month` column to each dataset
- Appended all files into one consolidated table

## 4️⃣ Data Type Corrections

| Column Type | Conversion |
|-----------|-----------|
| Created Date, Cleared Date, Closed Date | Date/Time |
| Numeric Fields | Whole Number / Decimal |
| Text Fields | Text |

---

## 5️⃣ Handling Missing Values

Meaningful null values were preserved:

- Closed Date → Open tickets
- Root Cause → Unresolved issues
- Customer Name → Internal/System tickets

> No blanket replacement of null values was performed to avoid introducing bias.

---

## 6️⃣ Duplicate Check

- Used `Ticket Number` as the unique identifier.
- No duplicates were found.

---

## 7️⃣ Filtering Test and Draft Records

Removed:

- Test tickets
- Internal or draft records

---

## 8️⃣ Derived Columns

### 📅 Month

Used for monthly trend analysis.

### ⏱️ Resolution Hours

Converted from `HH:MM:SS` text format into decimal hours.

#### Example
02:30:00 → 2.5 Hours
#### Benefits

- Average Resolution Time
- SLA Performance
- Team Efficiency Metrics

---

## 9️⃣ Text Standardization

### Abstract Column

Reduced 90+ variations into 10 standardized categories.

| Original Values | Standardized Category |
|----------------|----------------------|
| connectivity issue | Connectivity - Incident |
| incident connectivity | Connectivity - Incident |
| cm | CM |
| STC MDT | CM |

### Root Cause Column

| Original Value | Standardized Value |
|---------------|-------------------|
| Link Down | Equipment |
| Power Issue | Power |
| Link Congestion | Congestion |

---

## 🔟 Final Validation

Verified using Power Query Column Quality and Distribution tools:

- High completeness
- Valid date relationships
- Logical consistency

---

# 🗂️ Data Model

A single fact table named `Append1` was used.

## Model Characteristics

- Centralized ticket data
- Date fields used for time analysis
- DAX measures used instead of calculated columns

## Benefits

- Better performance
- Reduced redundancy
- Simplified maintenance

---

# 📈 Key KPIs and DAX Measures

## 📌 Core KPIs

### Total Tickets
``DAX
Total Tickets = COUNTROWS(Append1)

### Closed Tickets

``DAX
Closed Tickets =
CALCULATE(
    [Total Tickets],
    Append1[Status] = "Closed"
)

## Open Tickets

Open Tickets = [Total Tickets] - [Closed Tickets]

## ⚡ Performance KPI

### Average Resolution Time

``DAX
Avg Resolution Time =
AVERAGE(Append1[Resolution Hours])

# 🔍 Key Insights

## 🚨 SLA Breaches

Certain severity levels consistently exceeded SLA limits.

## 📈 Ticket Volume Trends

Ticket counts peaked during specific months, indicating workload fluctuations.

## 🎯 Root Cause Concentration

A small number of root causes accounted for the majority of incidents.

## 👥 Team Performance Variation

Some teams resolved tickets significantly faster than others.

---

# 🛠️ Tools & Technologies Used

- Power BI
- Power Query
- DAX (Data Analysis Expressions)
- Microsoft Excel

---

# 📊 Dashboard Features

- KPI Cards
- Monthly Trend Analysis
- SLA Compliance Visualization
- Root Cause Breakdown
- Team Performance Comparison
- Interactive Filters and Slicers

---

# 🎓 Skills Demonstrated

- Data Cleaning and Transformation
- Data Modeling
- DAX Measure Development
- KPI Design
- Dashboard Development
- SLA and Operational Analysis
- Text Standardization
- Business Intelligence Reporting

---

# ✅ Conclusion

This project demonstrates how structured data preparation and visualization can turn operational ticket data into meaningful business insights.

By combining:

- Power Query for cleaning and transformation
- DAX for KPI calculations
- Power BI for interactive dashboards

The analysis provides:

- Clear visibility into ticket handling efficiency
- SLA compliance monitoring
- Root cause identification
- Team performance benchmarking
- Operational improvement opportunities
