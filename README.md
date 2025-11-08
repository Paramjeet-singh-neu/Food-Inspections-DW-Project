# 🍔 Food Inspections Data Warehouse Project

**Course:** DAMG7370 - Designing Data Arch & Business Intelligence  
**Institution:** Northeastern University  
**Team Members:** Nihil , Prathush ,Paramjeet Singh

---

## 📋 Project Overview

This project analyzes and visualizes food inspection data from Chicago and Dallas to improve public health transparency. We implement a complete data warehousing solution using the Medallion Architecture (Bronze → Silver → Gold layers) with dimensional modeling.

### Business Objectives
- Merge and standardize food inspection data from two cities with different schemas
- Create a dimensional data warehouse for efficient querying and analysis
- Build interactive dashboards for public health officials to identify trends and violations
- Implement data quality rules to ensure reliable insights

---

## 🏗️ Architecture

### Medallion Architecture Layers

**🥉 Bronze Layer (Raw Data)**
- Direct ingestion from source CSV files
- Minimal transformations
- Schema-on-read approach
- Preserves original data for auditing

**🥈 Silver Layer (Cleansed Data)**
- Data quality validation and cleansing
- Schema standardization across Chicago and Dallas datasets
- Data type conversions and formatting
- Duplicate removal
- Implements 8+ validation rules (per project requirements)

**🥇 Gold Layer (Dimensional Model)**
- Star schema with fact and dimension tables
- SCD Type 2 implementation for dim_business
- Optimized for analytical queries and reporting
- Ready for BI tool consumption

---

## 🛠️ Tech Stack

| Category | Tool | Purpose |
|----------|------|---------|
| **Data Profiling** | Alteryx Designer | Initial data exploration and quality assessment |
| **Data Processing** | Databricks | ETL pipeline (Bronze → Silver → Gold) |
| **Data Modeling** | ER Studio / Navicat | Dimensional model design |
| **Visualization** | Power BI / Tableau | Interactive dashboards |
| **Version Control** | Git + GitHub | Collaboration and code management |

---

## 📊 Data Sources

### Chicago Food Inspections
- **Source:** [City of Chicago Data Portal](https://data.cityofchicago.org/Health-Human-Services/Food-Inspections/4ijn-s7e5)
- **Update Frequency:** Daily
- **Time Period:** 2010-Present
- **Key Fields:** Inspection ID, DBA Name, License #, Facility Type, Risk, Results, Violations

### Dallas Food Inspections
- **Source:** [To be added]
- **Update Frequency:** [To be determined]
- **Time Period:** [To be determined]
- **Key Fields:** [To be documented after data profiling]

---

## 📂 Project Structure
```
Food-Inspections-DW-Project/
│
├── 00-Documentation/              # Project documentation
│   ├── Project-Requirements.pdf
│   ├── Data-Profiling-Report.docx
│   └── Source-to-Target-Mapping.xlsx
│
├── 01-Raw-Data/                   # Source data files
│   ├── Chicago/
│   └── Dallas/
│
├── 02-Data-Profiling/             # Data quality analysis
│   ├── Alteryx/                   # Alteryx workflows
│   └── Results/                   # Profiling outputs
│
├── 03-Dimensional-Model/          # Database design
│   ├── ER-Diagrams/               # Star schema diagrams
│   └── DDL-Scripts/               # Table creation scripts
│
├── 04-Databricks-Code/            # ETL pipeline code
│   ├── Bronze-Layer/              # Raw data ingestion
│   ├── Silver-Layer/              # Cleansing & validation
│   └── Gold-Layer/                # Dimensional model loading
│
├── 05-BI-Dashboards/              # Visualization files
│   ├── PowerBI/
│   └── Tableau/
│
└── 06-Screenshots/                # Evidence of deliverables
    ├── Bronze/
    ├── Silver/
    ├── Gold/
    └── Dashboard/
```

---

## 🎯 Deliverables

###  Part 1: Data Profiling (25 marks)
- [ ] Download and explore both datasets
- [ ] Profile data using Alteryx
- [ ] Document findings (structure, quality, characteristics)
- [ ] Identify common attributes for merging
- [ ] Create data profiling report

###  Part 2: Dimensional Model Design (25 marks)
- [ ] Design star schema with fact and dimension tables
- [ ] Create ER diagram
- [ ] Build source-to-target mapping document
- [ ] Write DDL scripts
- [ ] Deploy model structure in Databricks

###  Part 3: Data Loading (25 marks)
- [ ] Implement Bronze layer (raw data ingestion)
- [ ] Implement Silver layer with validation rules
- [ ] Implement Gold layer (dimensional model)
- [ ] Implement SCD Type 2 for dim_business
- [ ] Apply naming conventions (dim_, fact_)

###  Part 4: BI Dashboards (25 marks)
- [ ] Create interactive dashboards in Power BI or Tableau
- [ ] Include all required visuals (by result, type, risk, violations, etc.)
- [ ] Build inspection report view
- [ ] Ensure proper formatting and user experience

---

## 🔍 Data Quality Rules (Silver Layer)

The following validation rules are implemented:

1.  Restaurant Name cannot be null
2.  Inspection Date cannot be null
3.  Inspection Type cannot be null
4.  Zip codes cannot be null and must be in valid format (5 digits)
5.  Violation score in Dallas cannot exceed 100
6.  Chicago inspection results cannot be null
7.  Every inspection must have at least 1 unique violation
8.  Duplicate violations are loaded as distinct
9.  Dallas: If violation score ≥90, max 3 violations allowed
10. Inspection result cannot be "PASS" if violations contain "Urgent" or "Critical"

### Chicago Score Derivation

| Chicago Result | Derived Score |
|----------------|---------------|
| Pass | 90 |
| Pass w/ Conditions | 80 |
| Fail | 70 |
| No Entry | 0 |
| All other types | NULL |

---

## 🚀 Setup Instructions

### Prerequisites
- Python 3.8+
- Databricks account (Community Edition or Enterprise)
- Alteryx Designer
- ER Studio or Navicat
- Power BI Desktop or Tableau Desktop
- Git installed on your machine

### Getting Started

1. **Clone the repository:**
```bash
   git clone https://github.com/YourUsername/Food-Inspections-DW-Project.git
   cd Food-Inspections-DW-Project
```

2. **Download the data:**
   - Chicago: [Download link]
   - Dallas: [Download link]
   - Place files in `01-Raw-Data/` respective folders

3. **Follow the implementation guide:**
   - Start with data profiling (Part 1)
   - Design dimensional model (Part 2)
   - Implement ETL pipeline (Part 3)
   - Create dashboards (Part 4)

---

## 👥 Team Collaboration

### Git Workflow

**Before starting work:**
```bash
git pull origin main
```

**After making changes:**
```bash
git add .
git commit -m "Descriptive message about what you changed"
git push origin main
```

### Branching Strategy
- `main` - Stable, working code only
- `dev` - Active development branch
- `feature/your-name-task` - Individual feature branches

---

## 📚 Documentation

Detailed documentation can be found in the `00-Documentation/` folder:
- **Data Profiling Report**: Comprehensive analysis of data quality
- **Source-to-Target Mapping**: Field-level transformations
- **Technical Design Document**: Architecture decisions

---

## 📸 Screenshots

All deliverable screenshots are organized in `06-Screenshots/`:
- Bronze layer tables and data
- Silver layer validation results
- Gold layer dimensional model
- Dashboard visualizations

---

## 📊 Dimensional Model

### Fact Table
- `fact_inspection_violation` - Grain: One row per inspection-violation

### Dimension Tables
- `dim_date` - Time dimension
- `dim_business` - Restaurant details (SCD Type 2)
- `dim_location` - Geographic information
- `dim_violation` - Violation codes and descriptions
- `dim_inspection_type` - Types of inspections
- `dim_facility_type` - Types of facilities
- `dim_risk_category` - Risk classifications

---

## 🎓 Learning Outcomes

This project demonstrates:
- End-to-end data warehousing implementation
- Medallion Architecture best practices
- Dimensional modeling (Kimball methodology)
- Data quality management
- ETL pipeline development
- BI dashboard design
- Git collaboration workflows

---

---

**Last Updated:** [Current Date]
