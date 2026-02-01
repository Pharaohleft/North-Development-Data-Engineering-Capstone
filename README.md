

# SQL Database for New Development Real Estate Market Analysis  
**Brickell & Downtown Miami for NORTH DEVELOPMENT, MIAMI**

---

##  Overview

This project builds a centralized **SQL database and analytics layer** to analyze the **new residential development market** in **Brickell and Downtown Miami**.

The system consolidates fragmented CSV data into a **structured relational model** and enables:

- Pricing analysis  
- Inventory tracking  
- Sales velocity insights  

The database supports **historical pricing**, **unit availability tracking**, and **sales detection logic** based on real-world market behavior, enabling reliable internal decision-making.

---

##  Business Objective

Real estate development data is often delivered in **disconnected spreadsheets**, making it difficult to:

- Track unit-level price changes over time  
- Monitor inventory availability accurately  
- Identify sales velocity and demand trends  
- Support pricing strategy decisions  

This project solves those challenges by:

- **Centralizing** all market data into SQL  
- **Automating** reporting logic with reusable queries  
- **Creating** consistent, auditable metrics for pricing and sales analysis  

---

##  Data Sources

The database ingests multiple standardized CSV inputs:

### 1️ Project-Level CSV
- Project name  
- Total units  
- Percent sold  
- Market location (Brickell / Downtown Miami)

### 2️ Project-Specific Unit CSVs (one per project)
- Unit number  
- Availability status  
- Price  
- Price per square foot  
- Release date  

### 3️ Unit Line Mapping CSV
- Maps each unit to a building line  
- Example: `Apt 1510 → Line 10`

All CSVs are standardized and loaded into **relational tables** for scalable analysis.

---

##  Database Design

The database follows a **normalized relational structure** designed for historical analysis and scalability.

### Core Tables

#### `projects`
- `project_id` (PK)  
- `project_name`  
- `location`  
- `total_units`  

#### `units`
- `unit_id` (PK)  
- `project_id` (FK)  
- `unit_number`  
- `line_number`  
- `exposure`  
- `floor`  
- `square_feet`  

#### `unit_pricing_history`
- `pricing_id` (PK)  
- `unit_id` (FK)  
- `price`  
- `price_per_sqft`  
- `release_date`  
- `snapshot_date`  

#### `unit_availability`
- `unit_id` (FK)  
- `is_available`  
- `last_seen_on_release_list`  
- `snapshot_date`  

---

##  Key SQL Queries & Logic

### 1️ Latest Available Units
Returns the **most recent available units** per project, including:

- Project name  
- Unit number  
- Unit ID (concatenated project name + unit number)  
- Unit description  
- Exposure  
- Floor / building location  
- Latest price  
- Price per square foot  

**Use case:** Real-time inventory review and pricing comparisons.

---

### 2️ Historical Pricing Analysis
Tracks **price changes over time** at the unit level:

- Retrieves the last recorded price a unit was released for  
- Enables historical pricing trend analysis  
- Supports price optimization decisions  

---

### 3️ Sales Tracking Logic
A unit is classified as **sold** if:

- It has been **off the release list for at least four consecutive weeks**

This logic mirrors **real-world sales behavior** instead of relying on manual status updates.

**Outputs:**
- Units sold per timeframe  
- Sales velocity by project  
- Market absorption trends  

---

### 4️ Available Inventory Forecast
Predicts future available inventory by:

- Accounting for sold units using sales-detection logic  
- Dynamically adjusting inventory as new snapshots are ingested  

**Use case:** Supply forecasting and pricing strategy planning.

---

##  Business Impact

This system enables:

- Automated internal pricing reports  
- Clear visibility into inventory levels and demand  
- Accurate sales velocity tracking  
- Data-driven pricing and release strategy decisions  

The project replaces **manual spreadsheet analysis** with a **scalable SQL analytics foundation**.

---

##  Tech Stack

- **SQL** (PostgreSQL / MySQL compatible)  
- **CSV ingestion pipelines**  
- **Relational database modeling**  
- **Analytical SQL** (CTEs, window functions, joins)  

---

##  Future Enhancements

- BI dashboard integration (Power BI / Tableau)  
- Automated weekly data ingestion  
- Market-level trend forecasting  
- Price elasticity and demand modeling  
- API layer for live reporting  

---

