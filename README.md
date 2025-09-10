# AI-Augmented Data Pipeline — GCP

> **Project:** AI-Augmented Data Pipeline on GCP  
> **Tech stack:** Kafka, Python, Apache Airflow (Composer), Dataflow, Dataproc/Databricks (Spark/PySpark), dbt, Delta Lake/Iceberg on GCS, BigQuery, BigQuery ML / Vertex AI, Looker Studio, Terraform, Docker

---

## 📌 Project Summary
A production-style, end-to-end data pipeline that ingests **batch + streaming** data (Kafka + GCS), performs large-scale transformations with **Spark** and **dbt**, stores curated tables in a **Delta/Iceberg lakehouse on GCS**, and serves analytics in **BigQuery**. AI components (BigQuery ML / Vertex AI) provide **anomaly detection** and **forecasting**, while orchestration and infra are automated using **Airflow**, **Terraform**, and **Docker**. Visualizations are delivered through **Looker Studio**.

---

## 🏗 Architecture (high level)

> Add `assets/architecture.png` for a visual diagram (recommended). See **assets/** instructions below.

---

## ✅ What this README includes
- Setup & prerequisites  
- Folder structure  
- Deployment steps (Terraform + Docker + Airflow DAGs)  
- How to run locally and on GCP  
- dbt & Spark job examples  
- BigQuery ML usage example  
- Logging examples (with sample logs)  
- HTML animation + image placeholders you can paste into your repo

---

## ⚙️ Prerequisites
- GCP project with billing enabled  
- Service account with roles: BigQuery Admin, Storage Admin, Dataflow Admin, Composer Admin, Pub/Sub Admin  
- Python 3.8+ local environment  
- Kafka cluster (self-managed or Confluent Cloud)  
- Terraform  
- Docker  
- dbt (dbt-core + adapter for BigQuery)

---

## 📁 Recommended Repo Structure

---

## 🔧 Quick Deploy Steps
1. Clone repo  
2. Add your GCP credentials and set `GOOGLE_APPLICATION_CREDENTIALS`  
3. `cd infra/ && terraform init && terraform apply` (review changes)  
4. Build and push Docker images (`docker build -t gcr.io/<project>/processor:latest . && docker push ...`)  
5. Deploy Airflow DAGs to Composer environment (copy `dags/`)  
6. Start Kafka producers (or use sample producers in `services/`)  
7. Trigger Airflow DAGs manually for first run

---

## 💡 dbt & Delta Lake notes
- Use dbt to manage SQL models that run on BigQuery after the Spark stage writes curated tables to GCS/Delta and metadata is loaded into BigQuery.  
- Example `dbt` commands:

```bash
cd dbt
dbt deps
dbt seed
dbt run --models staging.*
dbt test --models +staging.*




