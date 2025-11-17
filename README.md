
#  CVE 2024 Data Engineering Pipeline (Databricks + Delta Lake)

This repository contains a complete data engineering pipeline for ingesting, validating, transforming, and analyzing the **2024 CVE (Common Vulnerabilities and Exposures)** dataset using **Databricks**, **Apache Spark**, and **Delta Lake**.  
The project follows the modern **Bronze → Silver → Analysis** lakehouse architecture and demonstrates end-to-end processing of large-scale cybersecurity data.

---

##  Project Overview

The goal of this project is to build a production-style ETL pipeline capable of processing **38,753 CVE records from 2024**, normalizing nested JSON structures, and generating meaningful security insights.  
The pipeline is fully automated inside a Databricks notebook and includes:

 Large-scale JSON ingestion  
 Schema normalization and validation  
 Delta Lake Bronze and Silver layers  
 SQL-based exploratory analysis  
 Vendor and severity intelligence  

This project aligns with the requirements for the **Data Intensive Computing (DIC)** assignment.

---

##  Architecture

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

##  Bronze Layer – Raw → Validated Delta Table

###  Data Source
All CVE 2024 files are downloaded from the official  
**CVEProject/cvelistV5** GitHub repository.

###  Processing Steps
- Extract the CVE ZIP archive  
- Traverse all **CVE-2024-*.json** files  
- Normalize nested `containers` fields to JSON strings  
- Add ingestion metadata  
- Convert into a Spark DataFrame  
- Save as a **managed Delta table**:

```

bronze_db.cve_bronze_2024

```

###  Assignment-required logical view
```

cve_bronze.records

```

###  Quality Checks
- Row count ≈ **38,753**
- CVE IDs are **non-null**
- CVE IDs are **100% unique**
- Table metadata and Delta history validated

---
<img width="1122" height="542" alt="image" src="https://github.com/user-attachments/assets/e4c4f34e-310b-42d7-908e-1a5ddb2c00a3" />
<img width="1141" height="437" alt="image" src="https://github.com/user-attachments/assets/339fad79-39fb-48dd-8032-5504428da9c2" />



##  Silver Layer – Normalized Analytical Tables

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
<img width="1108" height="381" alt="image" src="https://github.com/user-attachments/assets/6aeafd6d-4c71-4f0a-a838-91c9c9f0ed86" />
<img width="1084" height="343" alt="image" src="https://github.com/user-attachments/assets/769f8459-008a-40d0-9fad-0fbf07023d41" />
<img width="1104" height="413" alt="image" src="https://github.com/user-attachments/assets/6843b818-1252-4610-954f-16e3f8ef97a7" />
<img width="1101" height="630" alt="image" src="https://github.com/user-attachments/assets/40de9e9d-3450-489c-9c8b-873a7a5fd1c7" />





## 📊 Exploratory Data Analysis (SQL)

### **1. Temporal Trends**
- Monthly CVE publication counts  
- Seasonality based on month names  
- **Reserved → Published latency** using `DATEDIFF`
  <img width="1077" height="729" alt="image" src="https://github.com/user-attachments/assets/1ccf9e4e-6c9c-48a6-a85b-fc6d49af3656" />
  <img width="1091" height="596" alt="image" src="https://github.com/user-attachments/assets/43c8d6f7-044e-4ba1-bf1b-072ddd3140f7" />
  


### **2. Severity Distribution**
- CVSS-based severity buckets  
- Monthly severity trends  
- Count of CVEs with unknown scores
  <img width="1103" height="731" alt="image" src="https://github.com/user-attachments/assets/eba5f163-398a-4bcf-b839-45fc5b3a86b1" />
  <img width="1111" height="492" alt="image" src="https://github.com/user-attachments/assets/12ab8420-3c6e-491a-a8bb-6c477872fec9" />



### **3. Vendor Intelligence**
- Top 25 vendors by vulnerability volume  
- Top-10 concentration share (≈ 40.22%)  
- Vendor × severity risk matrix  
<img width="1122" height="659" alt="image" src="https://github.com/user-attachments/assets/d5ffb322-7fa4-4f6d-9813-ab671f108633" />
<img width="1123" height="674" alt="image" src="https://github.com/user-attachments/assets/4763d68f-b855-477f-b3db-5e17e393516b" />


---

##  How to Run the Pipeline

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

---

##  Purpose of This Project

This project demonstrates real-world data engineering skills including:

- Processing large nested JSON datasets  
- Designing lakehouse pipelines with Bronze/Silver layers  
- Building reproducible ETL in Databricks  
- Applying schema normalization and validation  
- Generating domain-specific cybersecurity insights at scale  

It serves as both an academic assignment and a strong portfolio project for **Data Engineering**, **Big Data**, and **Security Analytics** roles.

---

##  Author

**Gowtham Sai Krishna Tanikonda**  
MS in Data Science, University at Buffalo  


```

---


