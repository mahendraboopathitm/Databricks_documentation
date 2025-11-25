# Databricks_documentation

## 1. Databricks

Databricks is a cloud-based unified data analytics platform designed for big data processing, analytics, data engineering, and machine learning. It provides a collaborative environment built on Apache Spark.

---

## 1.1 Workspace UI

The Databricks Workspace UI is the web interface where users interact with all Databricks features. It provides access to notebooks, jobs, data, clusters, ML components, and more.

Key areas of the UI:

* **Sidebar** – Navigation for workspace components (Workspace, Data, Compute, Jobs, etc.)
* **Main Canvas** – Displays opened notebooks, files, and cluster dashboards.
* **Toolbar** – Options like run commands, cell execution, settings, cluster selection.

---

## 1.2 Overview of UI Components

Important UI components include:

| Component          | Description                                           |
| ------------------ | ----------------------------------------------------- |
| Workspace          | Stores notebooks, folders, dashboards, and repos.     |
| Data               | View, upload, and explore datasets and tables.        |
| Compute (Clusters) | Manage Spark clusters used to run jobs and notebooks. |
| Repos              | Connect workspaces with Git version control.          |
| Jobs               | Schedule automated workflows and pipelines.           |
| Marketplace        | Access various data and package providers.            |
| Settings           | User profile, API tokens, and configuration.          |

---

## 1.3 Workspaces

A **Workspace** organizes all user objects, including:

* Notebooks
* Libraries
* Repos
* ML models
* Dashboards
* Folder structures

Workspaces allow role-based access control for users and teams.

---

## 1.4 Notebooks

A **Databricks Notebook** is an interactive environment used to:

* Write and run code (Python, SQL, Scala, R)
* Visualize data
* Document workflows using Markdown
* Execute commands on a selected Spark cluster

Notebooks support cell-based execution.

---

## 1.5 Libraries

**Libraries** are software packages installed to enhance your workspace or cluster.

Common library types:

* Python packages (.whl or PyPI)
* JAR files (Scala/Java)
* CRAN R packages

Libraries may be installed:

* At the cluster level
* Notebook/session level

---

## 1.6 Data

The **Data** section lets users:

* View datasets and schemas
* Upload CSV, JSON, Parquet, and other files
* Access tables and databases in the metastore
* Ingest data into the Lakehouse

Data may be stored in:

* DBFS (Databricks File System)
* External cloud storage (S3, ADLS, GCS)
* Hive tables

---

## 1.7 Clusters

A Databricks cluster is a Spark-based compute engine where notebook code executes.

Cluster features:

* Distributed data processing
* Support for auto-scaling
* Managed Spark environment
* Integration with Databricks runtime versions

---

# 2. Workspace Navigation

---

## 2.1 Creating and Managing Notebooks

1. Click **Workspace → Create → Notebook**
2. Give the notebook a name
3. Choose default language (Python/SQL/Scala/R)
4. Attach a cluster to start running code

Management actions:

* Rename, delete, move, import/export
* Run interactively or schedule in Jobs

---

## 2.2 Uploading and Managing Data

Ways to upload data:

* **Drag & Drop** via the Data UI
* Using **DBFS CLI**
* Using **Databricks File browser**
* Using Spark code:

```
df = spark.read.csv("/FileStore/tables/data.csv")
```

Data can then be transformed, queried, or registered as a table.

---

## 2.3 Managing Clusters

Users can:

* Create new clusters
* Start/stop clusters
* Monitor usage and logs
* Apply policies and limits

Cluster actions available from the **Compute** section.

---

## 2.4 Accessing Libraries

Installed libraries can be:

* Viewed in the **Libraries** tab within a cluster UI
* Installed via upload
* Pulled from repositories (Maven, PyPI, CRAN)

---

## 2.5 Collaboration and Sharing

Databricks provides real-time collaboration:

* Multiple users can work in the same notebook
* Role-based access control (view, edit, run)
* Activity history and notebook permissions

---

## 2.6 Sharing Notebooks

Steps:

1. Open a Notebook
2. Click **Share**
3. Add user emails or assign permissions:

   * Can View
   * Can Run
   * Can Edit
   * Can Manage

---

## 2.7 Collaborative Editing

Multiple users can:

* See real-time cursor movements
* Chat through comments
* Work simultaneously like Google Docs

---

## 2.8 Version History

Databricks automatically stores versions of notebooks:

* Undo changes using **Revision History**
* Compare old and new versions
* Restore previous versions anytime

---

# 3. Cluster Creation

---

## 3.1 Cluster Configuration

Key configuration settings:

* Databricks Runtime version
* Python version
* Auto-termination time
* Worker node and driver specs
* Cluster size (min/max nodes)

---

## 3.2 Cluster Type

| Type                         | Use Case                                               |
| ---------------------------- | ------------------------------------------------------ |
| **Standard Cluster**         | Multi-purpose, general Spark computation               |
| **High Concurrency Cluster** | Shared among multiple users, optimized for concurrency |

---

## 3.3 Worker Node Types

Workers determine compute power. Options vary by cloud provider:

### Examples:

* Memory Optimized
* Compute Optimized
* GPU Accelerated

Node specs affect:

* Speed of operations
* Cost
* Performance on large datasets

---

## 3.4 Auto Scaling Options

Auto scaling allows Databricks to adjust cluster size automatically based on workload.

Benefits:

* Reduced cost during low usage
* Increased speed during load spikes
* Fully managed scaling logic

Configuration:

* Set **Min Workers**
* Set **Max Workers**
* Databricks adds or removes nodes automatically

---

# 📘 Databricks dbutils & DBFS – Complete Documentation
## 1. dbutils Command
### 1.1 Overview of dbutils

dbutils is a utility library in Databricks that provides helper functions to interact with:

File system

Notebooks

Widgets

Libraries

Secrets

### Why we use it?

To automate tasks and perform system-level operations inside notebooks.

### Where we use it?

Interaction with DBFS

Triggering other notebooks

Creating widgets

Installing libraries

Runtime utilities

## 1.2 Accessing dbutils in Notebooks

In a Databricks notebook:

dbutils
```
from pyspark.dbutils import DBUtils
dbutils = DBUtils(spark)
```
## 1.3 Common dbutils Commands
```
File System	dbutils.fs.ls("/")
Notebook	dbutils.notebook.run(...)
Widgets	dbutils.widgets.text(...)
Libraries	dbutils.library.install(...)
Secrets	dbutils.secrets.get(...)
```
## 1.4 dbutils.fs (File System Operations)
Definition
Used to interact with files and directories in DBFS.
### Why use?
To read, write, delete, move files.
Example:
### List files in a directory
```
dbutils.fs.ls("/")
```
### Create directory
```
dbutils.fs.mkdirs("/mnt/data")
```
### Remove directory/file
```
dbutils.fs.rm("/mnt/data", True)
```
## 1.5 dbutils.notebook (Notebook Operations)
Definition
Used to call and manage other notebooks.
### Why use?

Creating pipelines

Notebook chaining

Reusing logic

### Example:
```result = dbutils.notebook.run("/Shared/child_notebook", 60, {"table": "users"})
print(result)
```
## 1.6 dbutils.library (Library Operations)
Definition
Used to install and manage external libraries at runtime.
Why use?

To dynamically add libraries needed in a notebook.

### Example:
```
dbutils.library.installPyPI("pandas")
dbutils.library.restartPython()
```
## 1.7 dbutils.widgets (Widget Operations)
Definition
Used to add input widgets in a notebook UI.

Why use?

Parameterization

Interactive dashboards

### Example:
```
dbutils.widgets.text("input_val", "default_value", "Enter something")
dbutils.widgets.get("input_val")
```
# 2. Example Usages
### 2.1 Uploading and Downloading Files
# Upload using DBFS CLI or UI
```
dbutils.fs.put("/mnt/data/example.txt", "hello world")
```
# Read file
```
dbutils.fs.head("/mnt/data/example.txt")
```
## 2.2 Running External Notebooks
```
result = dbutils.notebook.run("/Shared/process_data", 300, {"date": "2025-01-01"})
print(result)
```
## 2.3 Installing and Managing Libraries
```
dbutils.library.installPyPI("numpy")
dbutils.library.restartPython()
```
## 2.4 Interacting with Widgets
```
dbutils.widgets.dropdown("state", "CA", ["CA", "TX", "NY"], "Select State")
state = dbutils.widgets.get("state")
print(state)
```
# 3. Read & Write in DBFS
## 3.1 Introduction to DBFS (Databricks File System)

DBFS is a distributed file system on top of cloud storage like AWS S3, Azure Blob, or GCP.

Why use?

Central data storage for notebooks, jobs, and pipelines.

## 3.2 Overview of DBFS

Path types in DBFS:
Type	Example
```
DBFS root	/dbfs/...
DBFS path inside notebook	"dbfs:/mnt/data"
Mounted storage	dbfs:/mnt/my_mount/data.csv
```
### List files:
```
dbutils.fs.ls("/")
```
## 3.3 Mount Points

Example mount:
```
dbutils.fs.mount(
  source = "wasbs://container@storageaccount.blob.core.windows.net",
  mount_point = "/mnt/data",
  extra_configs = {"fs.azure.account.key": "<key>"}
)
```
## 3.4 Reading Data from DBFS

### List files:
```
dbutils.fs.ls("/mnt/data")

```
Read a text file:
```
spark.read.text("dbfs:/mnt/data/myfile.txt").show()
```
## 3.5 Reading CSV/Parquet Files
### CSV Example:
```
df = spark.read.option("header", True).csv("dbfs:/mnt/data/users.csv")
df.show()
```
### Parquet Example:
```
df = spark.read.parquet("dbfs:/mnt/data/sales.parquet")
```

### 3.6 Reading Other File Formats
Format	Example
```
JSON	spark.read.json(...)
Avro	spark.read.format("avro").load(...)
ORC	spark.read.orc(...)
```
### 3.7 Writing Data to DBFS
```
df.write.mode("overwrite").csv("dbfs:/mnt/output/users")
```
### 3.8 Writing CSV/Parquet Files
### Write CSV:
```
df.write.mode("overwrite").option("header", True).csv("dbfs:/mnt/output/users_csv")
```
### Write Parquet:
```
df.write.mode("overwrite").parquet("dbfs:/mnt/output/users_parquet")
```
## 3.9 Commands for Writing CSV & Parquet
### Operation	CSV	Parquet
|Write	|.csv(...)	|.parquet(...)|
|--------|-----------|-------------|
|Append	|.mode("append")|	.mode("append")|
Overwrite	|.mode("overwrite")	|.mode("overwrite")|
  
## 3.10 Writing Other File Formats
### JSON:
```
df.write.json("dbfs:/mnt/output/users_json")
```

### 3.11 Commands Summary
|Format  |           Read	        |         Write|
|--------|------------------------|---------------|
CSV	      |    spark.read.csv()	   |    df.write.csv()|
Parquet	  |  spark.read.parquet()	  |   df.write.parquet()|
JSON	   | spark.read.json()	    |   df.write.json()|

# Medallion Architecture & Delta Lake – Complete Documentation

This document provides a detailed explanation of Medallion Architecture, Delta Lake concepts, and advanced features used in modern data engineering pipelines (especially in Databricks).

---

# 1. Medallion Architecture

## 1.1 Introduction to Medallion

Medallion Architecture is a data design pattern used in data lakes to organize data into multiple structured layers:

* **Bronze Layer** – Raw data (unprocessed)
* **Silver Layer** – Cleaned, validated, and enriched data
* **Gold Layer** – Business-level aggregated data used for reporting

### Why Medallion Architecture?

* Better data quality at every stage
* Easier debugging and traceability
* Clear separation between raw and business-ready data

### Flow

```
Source Systems → Bronze → Silver → Gold → BI/Analytics
```

### Example Scenario

Assume you are receiving daily sales CSV files:

* **Bronze:** Load raw CSV files into Delta tables.
* **Silver:** Remove duplicates, handle missing values, standardize formats.
* **Gold:** Aggregate total sales per region/group for reporting or dashboards.

---

## 1.2 Use Cases and Applications

### Use Cases

* Enterprise Data Lake modernization
* ML feature data preparation
* Incremental pipelines
* Slowly Changing Dimensions
* Stream + Batch processing

### Real Applications

* Generating sales dashboards
* Feeding ML models from enriched data
* Customer analytics and segmentation
* Finance misreporting audits

---

# 2. Delta Lake (Theory)

## 2.1 Introduction to Delta Lake

Delta Lake is a storage layer built on top of data lakes (like S3/ADLS/DBFS) that provides:

* ACID transactions
* Schema enforcement
* Time Travel
* Data reliability

It is widely used in Databricks for scalable data pipelines.

---

## 2.2 ACID Transactions

ACID stands for:

* **Atomicity** – All operations succeed or fail together
* **Consistency** – Data always remains valid
* **Isolation** – Concurrent writes never corrupt data
* **Durability** – Once written, data is permanent

### Example

```python
df.write.format("delta").mode("append").save("/mnt/sales")
```

Even if the job fails midway, your Delta table won't become corrupted due to ACID guarantees.

---

## 2.3 Time Travel

Time Travel allows querying older versions of a Delta table.

### Example

```sql
SELECT * FROM sales_table VERSION AS OF 4;
```

or using timestamp:

```sql
SELECT * FROM sales_table TIMESTAMP AS OF '2024-11-21';
```

This is useful for:

* Auditing
* Comparing old data
* Recovering deleted data

---

## 2.4 Delta Table

A Delta Table is stored like a normal directory but with a structured transaction log.

### Example

```python
spark.sql("""
CREATE TABLE sales_delta
USING DELTA
AS SELECT * FROM sales_raw
""")
```

---

## 2.5 Delta Log

Every Delta table maintains a `_delta_log` directory that stores:

* Metadata
* Schema history
* Commit logs
* File actions and snapshots

This enables ACID and Time Travel features.

---

## 2.6 Usage and Benefits

### Benefits

* Consistent and correct data
* Scalable for large datasets
* Supports both streaming and batch
* Auto indexing for faster read

### Typical Use in ETL

```python
bronze_df.write.format("delta").save("/mnt/bronze")
silver_df.write.format("delta").save("/mnt/silver")
gold_df.write.format("delta").save("/mnt/gold")
```

---

## 2.7 Schema Evolution

Delta supports evolving schema dynamically.

### Example

```python
df.write.option("mergeSchema", "true").format("delta").save("/mnt/sales")
```

If new columns arrive, the table updates without failure.

---

# 3. Advanced Topics

# 3.1 Lakeflow Connect

Lakeflow Connect helps in moving external data sources into Databricks pipelines.

## 3.1.1 Upload Files

You can manually upload files from:

* UI
* CLI
* Mounted storage sources

Example:

```bash
dbfs cp sales.csv dbfs:/mnt/raw/
```

---

## 3.1.2 Managed Connectors

These are connectors maintained by Databricks, such as:

* Salesforce
* Azure SQL
* Postgres
* AWS RDS

They provide reliability and secure integration.

---

## 3.1.3 Standard Connectors

Community or open-source connectors used for:

* File transfers
* API ingestion
* Traditional ETL movement

---

## 3.1.4 Data Formats Supported

* CSV
* JSON
* Parquet
* Avro
* ORC
* Delta

### Example Read

```python
df = spark.read.format("csv").option("header", "true").load("/mnt/raw/sales.csv")
```

---

## 3.1.5 Migrate to Delta Table

You can convert existing tables to Delta:

```python
spark.sql("CONVERT TO DELTA sales_parquet")
```

---

# 3.2 Delta Lake Advanced Features

## 3.2.1 Operations

### Common Delta Operations

#### Update

```sql
UPDATE sales SET amount = amount * 1.1 WHERE region = 'APAC';
```

#### Delete

```sql
DELETE FROM sales WHERE canceled = true;
```

#### Merge (SCD Type 2)

```sql
MERGE INTO target t
USING source s
ON t.id = s.id
WHEN MATCHED THEN UPDATE SET *
WHEN NOT MATCHED THEN INSERT *
```

---

## 3.2.2 Data Layout Optimization

### Liquid Clustering

Organizes data by key columns for faster read performance.

### Data Skipping

Delta automatically avoids reading files irrelevant to the query.

### Tune File Size

Optimize small files:

```sql
OPTIMIZE sales ZORDER BY (customer_id);
```

### Partitioning

```python
df.write.partitionBy("country").format("delta").save("/mnt/sales")
```

---

## 3.2.3 Schema Enforcement & Evolution

* Blocks invalid writes
* Automatically tracks schema drift
* Merge new fields when enabled

---

## 3.2.4 Table Features

### Change Data Feed (CDF)

Track changed rows:

```sql
ALTER TABLE sales ENABLE CHANGE DATA FEED;
```

### Table Constraints

Example constraint:

```sql
ALTER TABLE sales ADD CONSTRAINT valid_amount CHECK (amount > 0);
```

### Generated Columns

```sql
ALTER TABLE events ADD COLUMN day STRING GENERATED ALWAYS AS (date_format(event_time,'yyyy-MM-dd'));
```

### Row Tracking

Helps track row identity over time.

### Type Widening

Allows changing data types progressively
(e.g., `int` → `bigint` without errors)

---

# 4. Catalog Explorer

## 4.1 Introduction

Catalog Explorer is a Databricks UI-based tool that allows users to:

- Browse databases, schemas, and tables in Unity Catalog  
- View table details, permissions, columns, statistics, lineage, and audit logs  
- Manage access control  
- Perform data exploration without writing SQL  

It provides a centralized view of all metadata stored in Unity Catalog.

---

## 4.2 Why Use Catalog Explorer?

### Benefits

- Unified place to explore all data assets  
- Easy governance and permission management  
- Audit trail and lineage for compliance  
- Helps prevent unauthorized access  
- Enables productivity for analysts, developers, and admins  

---

## 4.3 What You Can View in Catalog Explorer

### 1. Catalogs  
- Logical grouping of data assets  
- Example: `main`, `production`, `development`

### 2. Schemas  
- Subsection inside a catalog  
- Similar to databases in traditional systems  
- Contains tables, views, functions, etc.

### 3. Tables & Views  
For each table, you can see:

- Table schema  
- Storage format (Delta, Parquet, CSV, etc.)  
- Location  
- Owner details  
- Created/Modified timestamps  
- Record statistics  
- Table constraints  
- Change Data Feed status  

---

## 4.4 Exploring a Table – Example

When selecting a table (e.g., `sales_gold`), you may see:

### **Table Details**
```
Format: Delta
Rows: 36,42,580
Location: /mnt/gold/sales
Owner: data_admin
Created: 2024-10-01
```

### **Columns View**
| Column Name | Data Type | Nullable | Comment |
|-------------|------------|----------|---------|
| sale_id     | BIGINT     | NO       | Primary key |
| region      | STRING     | YES      | Sales region |
| amount      | DOUBLE     | YES      | Sales amount |

---

## 4.5 Access Management

From Catalog Explorer, you can view and assign permissions:

### Example Permission Roles

- `SELECT`
- `INSERT`
- `UPDATE`
- `DELETE`
- `OWNERSHIP`
- `USAGE`

### Example GRANT Statement

```sql
GRANT SELECT ON TABLE sales_gold TO `analyst_team`;
```

---

## 4.6 Data Lineage View

Catalog Explorer can show full data flow:

```
Raw File → Bronze Table → Silver Table → Gold Table → BI Dashboard
```

This helps in:

- Impact analysis  
- Debugging pipelines  
- Understanding transformations  

---

## 4.7 SQL and Sample Queries

Catalog Explorer also allows opening a notebook or SQL editor directly.

### Example

```sql
SELECT region, SUM(amount) AS total_sales
FROM sales_gold
GROUP BY region;
```

---

## 4.8 Audit Logs and Changes

You can audit:

- Who accessed table
- What updates were made
- When schema changed
- Version history

### Example Time Travel Check

```sql
DESCRIBE HISTORY sales_gold;
```

---

## 4.9 Common Use Cases

- Data discovery  
- Table lookup during development  
- Compliance and governance reporting  
- Debugging ETL failures  
- Tracking schema evolution  

---

## 4.10 Summary

Catalog Explorer provides:

- A centralized UI for exploring and managing all data assets  
- Governance and permission control  
- Powerful metadata insights  
- Support for lineage, auditing, and schema visibility  

It is an essential tool in Unity Catalog-based data engineering environments.

