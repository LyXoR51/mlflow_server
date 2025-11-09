# Run an MLflow Server Locally with Docker Compose

This setup runs a complete **MLflow Tracking Server** environment on your local machine using **Docker Compose**.
It includes all required components to experiment with MLflow locally — a **PostgreSQL** database for metadata and a **MinIO** service acting as an S3-compatible artifact store.

* **MLflow** uses **PostgreSQL** as the *backend store* for experiment and run metadata.
* **MLflow** uses **MinIO** as the *artifact store* (via S3 APIs).
* **Docker Compose** wires all services on a shared network, allowing MLflow to communicate with PostgreSQL and MinIO using container names (e.g., `postgres`, `minio`).

---

## 1. Setup Environment Variables

Before starting the containers, configure your local environment file:

1. Go to the folder:

   ```bash
   cd mlflow_server_local
   ```

2. Open the `.env` file and adjust the credentials and ports as needed:

   ```bash
   # Example .env configuration

   # PostgreSQL
   POSTGRES_USER=mlflow
   POSTGRES_PASSWORD=mlflow
   POSTGRES_DB=mlflow

   # MinIO
   MINIO_ROOT_USER=minio
   MINIO_ROOT_PASSWORD=minio123
   MINIO_BUCKET_NAME=mlflow
   ...
   ```

Make sure the credentials are unique if you plan to expose any services beyond localhost.

---

## 2. Start the Stack

Once the `.env` file is configured, launch the full MLflow stack:

```bash
docker compose up -d
```

This command will start:

* **PostgreSQL** (database for MLflow metadata)
* **MinIO** (S3-compatible storage)
* **MLflow server** connected to both services

---

## 3. Access the Services

* **MLflow Tracking UI:**
  [http://localhost:5000](http://localhost:5000)
  (or the port defined in your `.env` file)

* **MinIO Console:**
  [http://localhost:9001](http://localhost:9001)
  Login using the `MINIO_ROOT_USER` and `MINIO_ROOT_PASSWORD` defined in your `.env` file.

---

## 4. Stop or Remove the Containers

To stop and remove the containers and network (without deleting data):

```bash
docker compose down
```

> **Note:**
> Data is preserved in Docker **volumes** for PostgreSQL and MinIO.
> To remove volumes as well (irreversible), run:
>
> ```bash
> docker compose down -v
> ```

---

## 5. Configure Your MLflow Client

Once the services are running, you can connect to the local MLflow server from Python or CLI:

```bash
export MLFLOW_TRACKING_URI=http://localhost:5000
```

---

## 6. Verify Artifact Storage

After running an experiment, open the **MinIO console** and check the bucket defined in `.env`
(e.g., `mlflow`). You should see logged artifacts such as models, metrics, and parameters.


