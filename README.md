# MLflow Server Configurations

This repository provides multiple **MLflow tracking server configurations** for different deployment environments.
Each setup is designed to simplify the process of running, testing, or deploying an **MLflow** instance with minimal configuration effort.

---

## Overview

MLflow is an open-source platform for managing the end-to-end machine learning lifecycle.
This repository serves as a **collection of environment-specific configurations** to deploy or run MLflow servers in various contexts — locally, on cloud platforms, or via hosted services such as Hugging Face Spaces.

Each configuration lives in its own folder and includes:

* Deployment and configuration files (`Dockerfile`, `docker-compose.yml`, `.yaml`, or other setup scripts)
* A `requirements.txt` file when needed
* A dedicated `README.md` describing the setup and environment variables

---

## Repository Structure

```
mlflow-server/
│
├── mlflow_server_hf/
│   ├── Dockerfile
│   ├── requirements.txt
│   └── README.md          # Deploy MLflow on Hugging Face Spaces
│
├── mlflow_server_local/
│   ├── docker-compose.yml
│   ├── .env
│   └── README.md          # Deploy MLflow locally
│
├── test_tracking_URI/
│   ├── register_model.py
│   ├── test_model.py
│   └── README.md          # Test connections to remote MLflow URIs
│
└── README.md              # (You are here)
```

---

## Available Configurations

### 1. **mlflow_server_hf**

Deploy an MLflow tracking server on **Hugging Face Spaces**.
Connects to a **PostgreSQL database** and an **S3 bucket** for backend and artifact storage.
Ideal for lightweight cloud deployments or hosted demos.

### 2. **mlflow_server_local**

Run an MLflow server **locally** using Docker Compose.
Includes local storage and database integration.
Perfect for development, prototyping, and offline testing.

### 3. **test_tracking_URI**

A minimal setup to **test connections** to a remote MLflow tracking URI.
Useful for validating authentication, SSL, and client-server communication.

---

## Requirements

* **Docker** (or Docker Desktop)
* **Python 3.9+**
* (Optional) AWS S3 and PostgreSQL credentials for remote or hosted setups

---

## Getting Started

1. Clone this repository:

   ```bash
   git clone https://github.com/LyXoR51/mlflow_server.git
   cd mlflow-server
   ```

2. Select the configuration you want to use:

   * `mlflow_server_hf/` → for Hugging Face Space deployments
   * `mlflow_server_local/` → for local or containerized runs
   * `test_tracking_URI/` → for remote connection testing

3. Follow the step-by-step instructions in the configuration’s own `README.md`.
