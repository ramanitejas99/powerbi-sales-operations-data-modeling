
## 📸 Project Screenshots

### 1. Data Model
![Data Model](Screenshots/01_Star_Schema_Data_Model.png)

A star schema built for sales and operations analysis.

| Layer | Tables |
|---|---|
| **Fact tables (6)** | `fact_sales`, `fact_order_process`, `fact_inventory`, `fact_compaign_spend`, `fact_promotion_coverage`, `fact_sales_target` |
| **Dimension tables (6)** | `dim_customer`, `dim_product`, `dim_date`, `dim_geo`, `dim_compaign`, `dim_order_flags` |
| **Support tables (2)** | `security` (region → user email mapping for RLS), `_measure` (DAX measures) |

**Highlights**
- One-to-many relationships from dimensions to facts using surrogate and business keys
- Role-playing date relationships: order, invoice and delivery dates linked to `dim_date`
- Shared dimensions let multiple fact tables be analysed together (sales, inventory, campaigns, targets)
- Dedicated measures table keeps all KPIs in one place

---

### 2. Power Query Pipeline
![Power Query](Screenshots/02_Power_Query_Pipeline_Layers.png)

34 queries organized into four layers:

| Folder | Queries | Purpose |
|---|---|---|
| `01_store` | 22 | Raw source tables (staging) |
| `02_dimension` | 5 | Cleaned dimension tables |
| `03_fact` | 6 | Fact tables ready for modeling |
| `04_support` | 1 | Security table for RLS |

**Transformations used:** Append (ORDERS_2025 + ORDERS_2026), Merge (joining tables on business keys), Pivot / Unpivot, data type standardization, column renaming, handling missing values and duplicates.

---

### 3. Raw Source Tables
![Source Tables](Screenshots/03_Raw_Source_Tables_Overview.png)

22 raw source tables covering:
- **Customers and geography:** CUST_MASTER, Address, cities, regions, customer_contacts, user_details
- **Products:** products, subcategories
- **Orders:** ORDERS_2025, ORDERS_2026, orders, order_line_items, Channels
- **Finance:** INVOICES, invoice_lines, payments, exchange_rates
- **Operations:** shipments, inventory
- **Marketing and targets:** campaign_skus, CAMPAIGN_LOG, sales_targets

---

### 4. DAX Measures
![DAX Measures](Screenshots/04_DAX_Measures_Table.png)

A dedicated `_measure` table with reusable measures:

| Measure | Description |
|---|---|
| `total_sales` | Total sales value |
| `total_orders` | Number of orders |
| `total_customer` | Number of customers |
| `total_active_customer` | Customers with activity |
| `average_order_to_pay` | Average days from order to payment |

---

### 5. Data Validation
![Validation](Screenshots/05_Model_Validation_Dashboard.png)

A validation page built to check the model before creating final dashboards.

- **KPI cards:** Total Sales (527K), Total Orders (80), Avg Order to Pay (33), Total Active Customers (47)
- **Region slicer:** Asia Pacific, Europe, Latin America, Middle East, North America (to test filter propagation and RLS)
- **Matrix by Year / Quarter / Month:** Total Sales, Target Revenue and Total Units, compared against the source data

**Checks performed:** row counts, duplicate and missing keys, fact-table grain, relationship cardinality, filter propagation, and source vs. model totals.

