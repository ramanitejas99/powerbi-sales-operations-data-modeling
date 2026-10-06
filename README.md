# Power BI Sales & Operations Data Model

End-to-end Power BI project covering data cleaning, Power Query transformations, star schema modeling, DAX, row-level security (RLS) and data validation, built from 22 raw source tables.

---

## 📌 Project Overview

The goal of this project is to turn a complex, multi-table business dataset into a reliable analytical model. The focus is on **building the right foundation first** (clean data, a strong data model, accurate measures and validation) before building dashboards.

**Business areas covered:** sales, customers, products, orders, invoices, payments, shipments, inventory, marketing campaigns, promotions, sales targets and geography.

## 🛠️ Tools & Skills

| Area | Details |
|---|---|
| **Tool** | Power BI Desktop |
| **Data preparation** | Power Query (M) |
| **Modeling** | Star schema, fact and dimension design, relationships |
| **Calculations** | DAX measures |
| **Security** | Row-level security (RLS) |
| **Quality** | Data validation and reconciliation |

---

## 🏗️ Data Model

A star schema with **6 fact tables** and shared dimensions.

| Layer | Tables |
|---|---|
| **Fact tables (6)** | `fact_sales`, `fact_order_process`, `fact_inventory`, `fact_campaign_spend`, `fact_promotion_coverage`, `fact_sales_target` |
| **Dimension tables (6)** | `dim_customer`, `dim_product`, `dim_date`, `dim_geo`, `dim_campaign`, `dim_order_flags` |
| **Support tables (2)** | `security` (region to user email mapping for RLS), `_measure` (DAX measures) |

**Design highlights**
- One-to-many relationships from dimensions to facts
- Defined grain for each fact table
- Shared dimensions allow sales, inventory, campaigns and targets to be analysed together
- Role-playing date relationships for order, invoice and delivery dates ✏️ *(keep only if you set these up)*
- Dedicated measures table keeps all KPIs in one place

---

## 🧹 Power Query Pipeline

34 queries organized into four layers:

| Folder | Queries | Purpose |
|---|---|---|
| `01_store` | 22 | Raw source tables (staging) |
| `02_dimension` | 5 | Cleaned dimension tables |
| `03_fact` | 6 | Fact tables ready for modeling |
| `04_support` | 1 | Security table for RLS |

**Transformations used**
- **Append:** combined yearly order data (`ORDERS_2025` + `ORDERS_2026`)
- **Merge:** enriched tables using business keys
- **Pivot / Unpivot:** reshaped data for analysis
- Standardized column names and data types
- Handled missing values and duplicate records
- Removed unnecessary columns

### Raw source tables (22)
- **Customers & geography:** CUST_MASTER, Address, cities, regions, customer_contacts, user_details
- **Products:** products, subcategories
- **Orders:** ORDERS_2025, ORDERS_2026, orders, order_line_items, Channels
- **Finance:** INVOICES, invoice_lines, payments, exchange_rates
- **Operations:** shipments, inventory
- **Marketing & targets:** campaign_skus, CAMPAIGN_LOG, sales_targets

---

## 🧮 DAX Measures

A dedicated `_measure` table with reusable measures:

| Measure | Description |
|---|---|
| `total_sales` | Total sales value |
| `total_orders` | Number of orders |
| `total_customer` | Number of customers |
| `total_active_customer` | Number of active customers |
| `average_order_to_pay` | Average days from order to payment |

✏️ *Edit the descriptions to match your DAX. You can also add a code block for one or two key measures.*

---

## 🔐 Row-Level Security

- A `security` table maps each **region** to a **user email**
- The table filters `dim_customer` by region, so users see only their own region's data
- ✏️ *Add how you tested it (Modeling → View as), if you did.*

---

## ✅ Data Validation

A validation report page was used to check the model before building final dashboards:

- **KPI cards:** Total Sales, Total Orders, Avg Order to Pay, Total Active Customers
- **Region slicer** to test filter propagation and RLS
- **Matrix by Year / Quarter / Month** showing Total Sales, Target Revenue and Total Units

**Checks performed**
- Source vs. transformed row counts
- Duplicate and missing keys
- Fact-table grain and dimension key uniqueness
- Relationship cardinality and filter direction
- Source vs. model totals (sales, orders, quantities)
- Filter propagation to report visuals

---

## 💡 Key Learnings

- A good-looking dashboard does not guarantee correct analysis
- Data quality and model design come before visuals
- Validating at every stage catches issues early

**Workflow:** Clean data → Correct transformation → Strong data model → Accurate DAX → Validated results → Dashboard

---

## 📂 Project Structure

```
powerbi-sales-operations-data-modeling/
├── README.md
└── Sales_Operation_Data_Model.pbix   
```


