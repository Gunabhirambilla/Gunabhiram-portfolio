---
layout: default
title: Gunabhiram Billa – Data Engineering & Analytics Portfolio
---

# Gunabhiram Billa

**Data Engineer | Analytics Engineer | Snowflake | Healthcare Data | New York City**  
[LinkedIn](https://www.linkedin.com/in/gunabhiram/) • [GitHub](https://github.com/gunabhiram) • [Email](mailto:gunabhiram.billa@gmail.com)

---

<nav>
  <a href="#about">About</a> ·
  <a href="#skills">Skills</a> ·
  <a href="#projects">Projects</a> ·
  <a href="#articles">Articles</a> ·
  <a href="#contact">Contact</a>
</nav>

---

## 👋 About Me {#about}

I design and build **scalable data systems, automated reporting pipelines, and operational analytics frameworks** that support revenue, efficiency, and decision-making.

My work sits at the intersection of:

- **Data Engineering** – Snowflake data warehousing, SQL modeling, incremental pipelines  
- **Analytics Engineering** – Semantic layers, KPI frameworks, governed reporting systems  
- **Operational Analytics** – Funnel analysis, provider productivity, billing accuracy  
- **Business Impact** – ROI modeling, cost optimization, cross-system reconciliation  

I collaborate across Product, Engineering, Finance, Sales, and Customer Success to turn fragmented operational data into reliable, decision-ready systems.

---

## 🧠 Core Skills {#skills}

### Languages & Tools
- **SQL** – Advanced joins, CTE pipelines, window functions, performance tuning  
- **Python** – Automation, reporting workflows, data wrangling  
- **Excel & Word Automation** – Dynamic charts, templated reporting, PDF generation  
- **Git & GitHub** – Version control and collaboration  

### Platforms & Databases
- **Snowflake** – Warehouse design, transformation logic, semantic modeling  
- **AWS (Exposure)** – S3, API log analysis  
- **Tableau & Amazon QuickSight** – Dashboarding and embedded analytics  
- **CRM & Finance Systems** – Zoho CRM/Desk, QuickBooks integration  

### Strengths
- End-to-end pipeline thinking  
- Dimensional modeling discipline  
- Operational KPI framework design  
- Cross-functional systems integration  
- Data governance and reconciliation workflows  

---

## ⭐ Featured Projects {#projects}

Below are selected projects demonstrating end-to-end data system design — from modeling and automation to measurable business impact.

---

### 1. Automated KPI Reporting Pipeline (Snowflake → Python → Word/PDF)

**Tech Stack**: Snowflake, SQL, Python, Excel, Word, PDF  

- Built a fully automated reporting system extracting KPIs via parameterized SQL  
- Populated Excel templates and dynamic charts programmatically  
- Injected metrics and visuals into structured Word reports  
- Exported finalized documents as PDF for leadership distribution  
- Designed for scheduling and reuse across multiple customers  

**Impact**: ~80% reduction in manual reporting time and consistent, standardized weekly insights.

---

### 2. Customer ROI Metrics Engine (Product-Level ROI)

**Tech Stack**: Snowflake, SQL, Excel  

- Designed a standardized ROI framework across products  
- Modeled intake completion, scheduling adoption, reminder effectiveness, and engagement metrics  
- Quantified time savings, product adoption, and revenue impact potential  

**Impact**: Enabled structured renewal and upsell discussions backed by measurable product value.

---

### 3. SMS Reminder Optimization & Phone Number Rationalization

**Tech Stack**: SQL, Excel  

- Audited message content and SMS segment usage  
- Standardized templates with a ~150-character optimization threshold  
- Identified and disabled 300+ inactive or unnecessary phone numbers  

**Impact**: Reduced monthly SMS costs and improved messaging consistency.

---

### 4. Provider Count & Billing Reconciliation System

**Tech Stack**: SQL, Excel, QuickBooks  

- Built a reconciliation workflow aligning operational provider counts with CRM contracts and billing records  
- Implemented classification logic and FTE thresholds for billing alignment  
- Standardized reconciliation checkpoints across systems  

**Impact**: Improved billing accuracy and reduced risk of underbilling or misclassification.

---

### 5. EMR API Usage & Cost Analysis

**Tech Stack**: SQL, API Logs  

- Analyzed six months of API usage across multiple systems  
- Identified high-volume endpoints and redundant call patterns  
- Proposed optimization opportunities for improved cost efficiency  

**Impact**: Supported engineering decision-making and API cost governance.

---

### 6. Multi-Tenant Data Warehouse Modeling (Fact & Dimension Architecture)

**Tech Stack**: Snowflake, SQL  

- Designed scalable fact and dimension models supporting multi-customer analytics  
- Implemented time-aware joins (SCD Type 1 / Type 2 patterns) for historical attribution  
- Structured layered transformations (staging → intermediate → mart)  
- Enforced tenant-aware modeling discipline for secure benchmarking  

**Impact**: Improved query performance, reduced redundancy, and strengthened governance.

---

### 7. Idempotent Incremental ETL Framework

**Tech Stack**: Snowflake, SQL, Python  

- Designed incremental loads with deterministic watermark tracking  
- Implemented merge-based upsert logic for safe reruns  
- Built validation checks for duplicates and late-arriving data  
- Structured control tables to track pipeline state and recovery checkpoints  

**Impact**: Increased reliability of daily pipelines and reduced recovery time.

---

### 8. Cross-System Data Quality & Reconciliation Framework

**Tech Stack**: Snowflake, SQL  

- Built automated validation logic across CRM, billing, and operational systems  
- Implemented deterministic mismatch detection rules  
- Generated daily reconciliation snapshots to monitor system drift  
- Created structured exception reporting views  

**Impact**: Improved trust in financial and operational reporting.

---

### 9. Snowflake Warehouse Cost & Query Optimization Initiative

**Tech Stack**: Snowflake, SQL  

- Analyzed warehouse metering and query history to identify cost inefficiencies  
- Segmented compute by workload type (ETL, BI, ad hoc)  
- Optimized filtering and aggregation strategies to reduce full scans  
- Implemented right-sizing and auto-suspend policies  

**Impact**: Improved compute efficiency and long-term cost predictability.

---

### 10. UrgentIQ Visit Status Pipeline & Event Analytics Framework

**Tech Stack**: Python, SQL, Snowflake, API Integration  

- Designed and built an event-driven pipeline to process UrgentIQ API visit status data  
- Normalized visit status timelines (Status 1 → N) with gap-filling logic for missing transitions  
- Standardized timestamps (UTC → EST) to ensure consistent analytics  
- Developed transition duration analysis (e.g., Status 1→2, 2→3) to identify operational delays  
- Implemented a reusable incremental ingestion framework with deduplication and configurable schema mapping  

**Impact**: Eliminated manual lifecycle analysis, enabled scalable ingestion of API event data, and improved visibility into visit flow and operational bottlenecks  

---

## ✍️ Articles & Technical Writing {#articles}

I publish technical writing exploring data modeling, architecture decisions, automation strategies, and governance patterns.

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}

Topics include:

- Multi-tenant warehouse design  
- Incremental vs CDC trade-offs  
- Idempotent pipeline design  
- Behavioral fact & dimension modeling  
- Cross-system reconciliation frameworks  
- Snowflake cost optimization  
- Automation with Snowflake + Python  

---

## 🎯 Location & Career Direction

- **Location**: New York City (open to hybrid and remote roles)  
- **Current Focus**:
  - Production-grade Snowflake + Python pipelines  
  - Data quality and reconciliation systems  
  - Scalable analytics engineering patterns  
- **Career Direction**:
  - Senior Data Engineer / Analytics Engineer  
  - Platform-oriented data system ownership  
  - Cross-functional data infrastructure leadership  

---

## 📁 Contact {#contact}

- **LinkedIn**: [linkedin.com/in/gunabhiram](https://www.linkedin.com/in/gunabhiram)  
- **GitHub**: [github.com/gunabhiram](https://github.com/gunabhiram)  
- **Email**: [gunabhiram.billa@gmail.com](mailto:gunabhiram.billa@gmail.com)

---

*Building data systems that drive operational clarity — not just dashboards.*
