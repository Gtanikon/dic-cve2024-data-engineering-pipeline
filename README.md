
# 🛡️ CVE 2024 Data Engineering Pipeline (Databricks + Delta Lake)

This repository contains a complete data engineering pipeline for ingesting, validating, transforming, and analyzing the **2024 CVE (Common Vulnerabilities and Exposures)** dataset using **Databricks**, **Apache Spark**, and **Delta Lake**.  
The project follows the modern **Bronze → Silver → Analysis** lakehouse architecture and demonstrates end-to-end processing of large-scale cybersecurity data.

---

## 📘 Project Overview

The goal of this project is to build a production-style ETL pipeline capable of processing **38,753 CVE records from 2024**, normalizing nested JSON structures, and generating meaningful security insights.  
The pipeline is fully automated inside a Databricks notebook and includes:

✔ Large-scale JSON ingestion  
✔ Schema normalization and validation  
✔ Delta Lake Bronze and Silver layers  
✔ SQL-based exploratory analysis  
✔ Vendor and severity intelligence  

This project aligns with the requirements for the **Data Intensive Computing (DIC)** assignment.

---

## 🏗️ Architecture

```

GitHub CVE V5 JSON
↓
Bronze Layer (Raw Normalized Delta)
↓
Silver Layer (Relational Model)
↓
Exploratory Data Analysis (SQL)
↓
Cybersecurity Insights

```

---

## 🥇 Bronze Layer – Raw → Validated Delta Table

### ✔ Data Source
All CVE 2024 files are downloaded from the official  
**CVEProject/cvelistV5** GitHub repository.

### ✔ Processing Steps
- Extract the CVE ZIP archive  
- Traverse all **CVE-2024-*.json** files  
- Normalize nested `containers` fields to JSON strings  
- Add ingestion metadata  
- Convert into a Spark DataFrame  
- Save as a **managed Delta table**:

```

bronze_db.cve_bronze_2024

```

### ✔ Assignment-required logical view
```

cve_bronze.records

```

### ✔ Quality Checks
- Row count ≈ **38,753**
- CVE IDs are **non-null**
- CVE IDs are **100% unique**
- Table metadata and Delta history validated

---

## 🥈 Silver Layer – Normalized Analytical Tables

Two relational tables are created by parsing the Bronze JSON:

### **1. silver_db.cve_core_2024**
One row per CVE with:
- `cve_id`
- `date_reserved_ts`
- `date_published_ts`
- `date_updated_ts`
- `state`
- `description_en`
- `cvss_base_score`, `cvss_base_severity`, `cvss_vector`
- Ingestion metadata

**Rows:** 38,753

---

### **2. silver_db.cve_affected_2024**
Exploded table capturing affected software:

- `vendor`
- `product`
- `version`
- `version_status`
- `cve_id`

**Rows:** 179,498

---

## 📊 Exploratory Data Analysis (SQL)

### **1. Temporal Trends**
- Monthly CVE publication counts  
- Seasonality based on month names  
- **Reserved → Published latency** using `DATEDIFF`  

### **2. Severity Distribution**
- CVSS-based severity buckets  
- Monthly severity trends  
- Count of CVEs with unknown scores  

### **3. Vendor Intelligence**
- Top 25 vendors by vulnerability volume  
- Top-10 concentration share (≈ 40.22%)  
- Vendor × severity risk matrix  

---

## 🚀 How to Run the Pipeline

### **Prerequisites**
- Databricks Workspace  
- Runtime 14.x or later  
- Internet access for downloading the CVE dataset  

### **Steps**
1. Upload the notebook:
```

DIC_Assignment (6).ipynb

```
2. Attach an active Databricks cluster  
3. Run all cells sequentially  
4. Bronze and Silver tables will be created automatically  
5. SQL EDA results will be displayed in the notebook  

---

## 📁 Suggested Repository Structure

```

├── notebook/
│   └── DIC_Assignment.ipynb
├── screenshots/
│   ├── bronze_preview.png
│   ├── silver_core_preview.png
│   ├── eda_monthly_counts.png
│   └── vendor_distribution.png
└── README.md

```

---

## 🎯 Purpose of This Project

This project demonstrates real-world data engineering skills including:

- Processing large nested JSON datasets  
- Designing lakehouse pipelines with Bronze/Silver layers  
- Building reproducible ETL in Databricks  
- Applying schema normalization and validation  
- Generating domain-specific cybersecurity insights at scale  

It serves as both an academic assignment and a strong portfolio project for **Data Engineering**, **Big Data**, and **Security Analytics** roles.

---

## 👤 Author

**Gowtham Sai Krishna Tanikonda**  
MS in Data Science, University at Buffalo  


```

---


