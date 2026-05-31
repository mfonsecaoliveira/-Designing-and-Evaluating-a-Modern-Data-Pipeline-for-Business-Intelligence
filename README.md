# 🏗️ Designing and Evaluating a Modern Data Pipeline for Business Intelligence

> Academic project — **Business Intelligence & Data Warehousing**
> City College Dublin | Data Analytics Program | 2026

[![Grade](https://img.shields.io/badge/Grade-85%2F100-success?style=flat-square)](#-grade--feedback)
[![Type](https://img.shields.io/badge/Type-Architecture%20Design-blue?style=flat-square)](#)
[![Topic](https://img.shields.io/badge/Topic-Data%20Warehousing-orange?style=flat-square)](#)

---

## 📋 Overview

This project presents the **design and critical evaluation of a modern, end-to-end data pipeline** that transforms operational transactional data into business intelligence capability.

The scenario: a **medium-sized retail organization** running on a transactional MySQL system with no dedicated analytical infrastructure. The challenge: move the business from ad-hoc querying that strains the production database toward a structured, governed analytical ecosystem ready for advanced analytics and machine learning.

The solution is built on proven data warehousing principles (Kimball, Inmon) combined with the modern **Medallion architecture** (Bronze–Silver–Gold) popularized by Databricks.

---

## 🎯 What This Project Covers

- **OLTP vs OLAP** — fundamental distinctions in storage, schema design, and performance characteristics, and why analytical workloads shouldn't run on transactional systems
- **End-to-end pipeline design** — a six-layer architecture from source extraction to the BI consumption layer
- **Staging layers** — the role of raw vs clean staging, and how they enable validation checkpoints, debugging, and pipeline restart capability
- **Medallion architecture** — mapping Bronze/Silver/Gold layers onto the proposed pipeline
- **Data quality & governance** — a validation framework (duplicate detection, null checks, referential integrity, domain validation), metadata, and data lineage
- **Critical evaluation** — honest trade-offs: batch vs streaming, query performance vs schema flexibility, cost vs performance

---

## 🏛️ Architecture at a Glance

The proposed pipeline progressively refines data across six layers:

```
MySQL Database (OLTP Source)
        ↓
Batch Extraction (CSV Export, daily)
        ↓
Cloud Storage / S3 (Landing Zone — immutable storage)
        ↓
Raw Staging Layer (Bronze — unvalidated, preserves source fidelity)
        ↓
Clean Staging Layer (Silver — validated & cleaned)
        ↓
Data Warehouse (Gold — star schema, dimensional model)
        ↓
BI Layer (Dashboards & Reports — analytics ready)
```

### Medallion Layer Mapping

| Layer | Purpose | Data Quality | Pipeline Mapping |
|-------|---------|--------------|------------------|
| **Bronze** | Raw data ingestion | Unvalidated | Landing Zone + Raw Staging |
| **Silver** | Cleaned, validated | Quality checks applied | Clean Staging |
| **Gold** | Business-ready analytics | Curated, aggregated | Warehouse + BI Layer |

---

## 🛡️ Data Quality Framework

A core part of the design is a layered quality validation process:

| Quality Check | Implementation | Business Impact |
|---------------|----------------|-----------------|
| **Duplicate Detection** | Primary key uniqueness, fuzzy matching | Prevents revenue inflation & customer count errors |
| **Null Validation** | NOT NULL constraints on critical fields | Ensures aggregation accuracy |
| **Referential Integrity** | Foreign key validation, orphan detection | Maintains dimensional model integrity |
| **Domain Validation** | Range checks, enumeration, pattern matching | Catches data entry errors |

---

## ⭐ Star Schema Design (Gold Layer)

The data warehouse uses a dimensional star schema with **Type 2 Slowly Changing Dimensions** for historical tracking:

- **fact_sales** — order grain, with FKs to all dimensions plus quantity, unit_price, total_amount, discount_amount
- **dim_customer** — surrogate + natural keys, with SCD2 validity tracking (effective_date, expiry_date, is_current)
- **dim_product** — category & brand attributes, SCD2 tracked
- **dim_date** — calendar attributes (quarter, year, is_weekend, is_holiday)
- **dim_store** — geographic attributes (city, region, country)

---

## 🧠 Key Takeaways

This project demonstrates understanding of the **full data warehousing stack**, not just isolated tools:

- Why operational and analytical systems must be separated
- How staging layers reduce pipeline fragility and enable debugging
- How the Medallion pattern gives stakeholders an intuitive mental model of data maturation
- Why proactive data quality is an investment that prevents downstream costs
- The conscious trade-offs every architecture decision involves

---

## 📄 Full Report

The complete technical report is available in this repository:

📑 **[CA01_Marcelo_Fonseca_Warehouse.pdf](./CA01_Marcelo_Fonseca_Warehouse.pdf)**

It includes detailed diagrams (pipeline topology, Medallion architecture, data quality validation flow), a full glossary of terms, and an appendix with SQL extraction examples and the complete star schema design.

---

## 🎓 Grade & Feedback

**Grade: 85/100**

Professor's overall comments:

> *"This is a top-tier submission, combining academic rigor, technical depth, and real architectural thinking. One of the strongest submissions overall — near benchmark quality."*

**Strengths highlighted:**
- Excellent end-to-end architecture with diagrams
- Strong technical depth (CDC discussion, SCD Type 2, star schema design)
- Very strong data quality framework
- Excellent critical evaluation (batch vs streaming, schema trade-offs)
- Strong use of academic sources throughout

---

## 📚 Course Details

| | |
|---|---|
| **Course** | Business Intelligence & Data Warehousing |
| **Program** | Data Analytics |
| **Institution** | City College Dublin |
| **Year** | 2026 |

---

## 👤 Author

**Marcelo da Fonseca Oliveira**
Data Analytics @ City College Dublin 🇮🇪

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ofonsecamarcelo)

---

*This is an academic project submitted as coursework. The architecture described is a design exercise based on a hypothetical retail scenario.*
