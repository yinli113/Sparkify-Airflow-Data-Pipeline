
# Sparkify Airflow Data Pipeline


## 🚀 Project Overview  
A production-style data-warehouse ETL/analytics pipeline built for the fictitious company **Sparkify**, implemented using **Apache Airflow** to orchestrate Spark jobs and monitor data quality. This project demonstrates the design and development of scalable, modular, reliable data workflows aligned to enterprise data-platform standards.

## 🧩 Objectives  
- Automate ingestion, transformation and loading of raw JSON music-streaming data into a data warehouse.  
- Orchestrate all pipeline tasks via Airflow DAGs with retry logic, scheduling, monitoring and back-fill capability.  
- Implement data-quality checks to ensure integrity, completeness and reliability of analytic data.  
- Use a star-schema warehouse model (fact + dimension tables) for downstream analytics.

## 🔧 Architecture & Tech Stack  
| Component | Purpose |
|-----------|---------|
| **Airflow** | DAG orchestration: schedule, monitor and retry workflow tasks. |
| **Spark / PySpark** | Distributed data processing: transform JSON logs and song metadata efficiently. |
| **Amazon S3** | Storage for raw source data and intermediate artifacts. |
| **Amazon Redshift** | Data warehouse platform for analytics-ready tables (fact/dimension). |
| **Custom Operators** | Reusable Airflow operators for staging, loading, transforming and data-quality tasks. |

## 📁 Key Components  
- `dags/` – Contains the main DAG definition, with task dependencies and parameters for scheduling, retries and back-fills.  
- `plugins/operators/` – Custom Airflow operators:  
  - **StageOperator**: load raw JSON from S3 into Redshift staging tables.  
  - **FactOperator / DimensionOperator**: load data into final schema tables – supports truncate/insert (dimensions) and append (fact) patterns.  
  - **DataQualityOperator**: run data-quality checks (e.g., non-null columns) and fail the job if conditions are not met.  
- `CREATE_TABLES.py` – SQL definitions for fact + dimension tables and staging structures in Redshift.

## ⏱ Running the Pipeline  
1. Set up your AWS credentials and IAM user with appropriate access.  
2. Launch a Redshift cluster (region: `us-west-2`).  
3. Configure Airflow connections:  
   - AWS default connection for S3/Redshift access.  
   - Redshift connection for queries and table loads.  
4. Place raw datasets in S3:  
   - `s3://udacity-dend/log_data` (user activity logs)  
   - `s3://udacity-dend/song_data` (song metadata)  
5. Trigger the DAG in Airflow:  
   - The pipeline will perform data staging → loading into final warehouse schema → run data-quality checks → make data available for analytics.

## ✅ Project Highlights  
- Built robust DAG logic: **no past run dependencies**, **3 retry attempts**, **5-minute retry delays**, and catch-up disabled.  
- Orchestrated complex workflows with clear dependencies and monitoring.  
- Ensured data quality by implementing automated checks (e.g., ensure no `NULL` values in key columns).  
- Designed a star-schema warehouse: `songplays` (fact) + `users`, `songs`, `artists`, `time` (dimensions).  
- Demonstrated engineering best-practices: modular code, parameterised configs, error handling, monitoring via Airflow UI.

## 📊 Why This Matters for Enterprise Data Platforms  
This project aligns strongly with real-world data-platform requirements:  
- Orchestration and scheduling using Airflow.  
- Scalable data processing using Spark/PySpark.  
- Cloud storage and compute (S3 + Redshift).  
- ETL architecture built for analytics with a star schema.  
- Monitoring, alerting and data-quality enforcement, integral to production-grade systems.

## 👥 Author  
**Yin Li** — Data Engineer with a strong focus on cloud-based pipelines, orchestration, and analytics engineering.

## 📚 Acknowledgements  
- Course-materials and templates from Udacity.  
- Inspiration from the Sparkify team and real-world data-platform use-cases.


```
