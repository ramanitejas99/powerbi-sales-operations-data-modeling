## 📸 Project Screenshots

### Data Model
Star schema with 6 fact tables, shared dimensions, role-playing date relationships and a security table.

![Data Model](Screenshots/README.md/01_Star_Schema_Data_Model.png)

### Power Query Pipeline
34 queries organized into Source, Dimension, Fact and Support layers.

![Power Query](Screenshots/02_Power_Query_Pipeline_Layers.png)

### Raw Source Tables
22 raw source tables covering customers, orders, invoices, payments, shipments, inventory and campaigns.

![Source Tables](Screenshots/03_Raw_Source_Tables_Overview.png)

### DAX Measures
Dedicated measures table with reusable KPIs: total sales, total orders, total customers, total active customers and average order-to-pay.

![DAX Measures](Screenshots/04_DAX_Measures_Table.png)

### Data Validation
Validation page checking KPIs, regional filtering and monthly totals against the source.

![Validation](Screenshots/05_Model_Validation_Dashboard.png)

