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


