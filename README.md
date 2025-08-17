# Databricks-like Local Environment (Open Source)

This project provides a local, dockerized environment that mimics Databricks using open-source tools:
- **Apache Spark** (core engine)
- **JupyterLab** (notebook interface)
- **MLflow** (experiment tracking)
- **Delta Lake** (ACID data lake)
- **MinIO** (S3-compatible storage)

## Prerequisites
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Setup

1. Clone this repository or copy the files to your machine.
2. Start all services:
   ```bash
   docker compose up -d
   ```

## Services

| Service      | URL                        | Notes                        |
|--------------|----------------------------|------------------------------|
| JupyterLab   | http://localhost:8888      | Token in `docker compose logs jupyter` |
| Spark Master | http://localhost:8080      | Spark UI                     |
| MLflow       | http://localhost:5000      | MLflow UI                    |
| MinIO        | http://localhost:9001      | S3 UI (user: minio, pass: minio123) |
| Zeppelin     | http://localhost:8081      | Apache Zeppelin notebook UI   |
| Polynote     | http://localhost:8192      | Polynote notebook UI         |

## Using Spark, Delta Lake, and MLflow in Jupyter

1. Open JupyterLab and create a new Python notebook.
2. Example Spark session:
   ```python
   from pyspark.sql import SparkSession

   spark = SparkSession.builder \
       .appName("LocalDatabricks") \
       .master("spark://spark:7077") \
       .config("spark.jars.packages", "io.delta:delta-core_2.12:2.4.0") \
       .getOrCreate()

   df = spark.createDataFrame([(1, "foo"), (2, "bar")], ["id", "value"])
   df.show()
   ```

3. Use MLflow and Delta Lake as you would in Databricks.

## Stopping Services

```bash
docker compose down
```

## Notes
- Data and notebooks are persisted in local folders (`jupyter/`, `mlruns/`, `minio/data/`).
- MinIO provides S3-compatible storage for Delta Lake and MLflow artifacts.
- This setup is for local development and learning only.

## Zeppelin & Polynote

- **Zeppelin:**
  - Access at [http://localhost:8081](http://localhost:8081)
  - Supports Spark, SQL, and more.
  - No authentication by default (for local use only).

- **Polynote:**
  - Access at [http://localhost:8192](http://localhost:8192)
  - Multi-language notebooks (Scala, Python, SQL, etc.)
  - Not actively maintained, but useful for experimentation.
  - Notebooks and config are in `polynote/` directory.
# databricks-like-local-env
