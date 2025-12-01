# E-commerce Data Lake Implementation (Delta Lake)

## Project Goal

This project focuses on designing and implementing a scalable, fault-tolerant, and high-performance Data Lake architecture for e-commerce order data using Delta Lake on Databricks.
The solution showcases modern data engineering practices such as ACID guarantees, schema evolution, time-travel querying, and storage optimizations required for large-scale analytical workloads.

---

##  Technology Stack

* *Platform:* Databricks
* *Language:* PySpark (Python)
* *Storage Format:* Delta Lake

---

##  Input Data Description

The solution ingests daily order records with the following base schema:

| Column | Type | Description |
| :--- | :--- | :--- |
| order_id | string | Unique order identifier |
| order_timestamp | timestamp | Time the order was placed (UTC) |
| customer_id | string | Unique customer identifier |
| country | string | Country code (e.g., "US", "IN") |
| amount | double | Order total |
| currency | string | Currency code |
| status | string | Current order status |

**Note:** The project also demonstrates **Schema Evolution* by later integrating two new fields: payment_method and coupon_code.*

---



## Key Features:

1. **Data Partitioning:** The Delta table is partitioned by:
* country
* order_date (derived from order_timestamp)

This ensures efficient data retrieval through:
- Partition pruning
- Faster query execution
- Reduced I/O scans

2.  **ACID Transactions:** Ensures data integrity during concurrent operations.
3.  **Time Travel (Data Versioning):** Demonstrated by querying a previous version of the table after an UPDATE operation.
4.  **Schema Evolution:** New fields are seamlessly added to the existing Delta table schema using the mergeSchema option.
5.  **Row-Level Manipulation:** Demonstrated using Delta's built-in **UPDATE** and **DELETE** commands.
6.  **Optimization:** Utilization of **OPTIMIZE** and **ZORDER BY** (customer_id) to compact small files and enhance data skipping performance.
