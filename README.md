# Deploy an MLflow Server on Hugging Face

This project provides a base setup to deploy an **MLflow tracking server** on **Hugging Face Spaces**, using a **Docker** environment.
The MLflow server connects to an **S3 bucket** for artifact storage and a **PostgreSQL** database for experiment metadata.

---

## 1. Prepare your local workspace

Create a working directory and clone this repository locally:

```bash
# Create a working directory
mkdir mlflow-server-huggingface
cd mlflow-server-huggingface

# Clone the base repository
git clone https://github.com/LyXoR51/mlflow-hf-server.git
```

---

## 2. Create a new Hugging Face Space

1. Go to [Hugging Face Spaces](https://huggingface.co/spaces).
2. Create a new Space — for example: `mlflow-server`.
3. Select **Docker** as the runtime.
4. Choose **Apache 2.0** as the license.

Then clone your new Space locally:

```bash
git clone https://huggingface.co/spaces/<HF-username>/mlflow-server
```

---

## 3. Copy the deployment files

Copy the Docker configuration files into your local Hugging Face Space folder:

```bash
cp mlflow-hf-server/Dockerfile mlflow-server/
cp mlflow-hf-server/requirements.txt mlflow-server/
```

---

## 4. Set your Hugging Face remote and push changes

Configure the Hugging Face remote using your user token, then commit and push the updated files:

```bash
cd mlflow-server

# Replace with your actual username and token
git remote set-url origin https://<HF-username>:<HF-token>@huggingface.co/spaces/<HF-username>/mlflow-server

git add .
git commit -m "Initial deployment setup"
git push origin main
```

---

## 5. Configure environment variables

In your Hugging Face Space, go to **Settings → Variables and secrets**.
Add the following **SECRETS** (adapt the values to your environment):

| Variable                      | Example Value                                                                                                            | Description                         |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------- |
| `AWS_ACCESS_KEY_ID`           | `AKIAIOSFODNN7EXAMPLE`                                                                                                   | AWS access key for your S3 bucket   |
| `AWS_SECRET_ACCESS_KEY`       | `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`                                                                               | AWS secret key for S3               |
| `ARTIFACT_STORE_URI`          | `s3://my-mlflow-bucket/artifacts/`                                                                                       | S3 path for storing model artifacts |
| `BACKEND_STORE_URI`           | `postgresql://mlflow_user:securepassword@ep-long-mode-aba1bf22-pooler.eu-west-2.aws.neon.tech/mlflow_db?sslmode=require` | PostgreSQL connection string        |
| `PORT`                        | `7860`                                                                                                                   | Default port for the MLflow server  |
| `MLFLOW_ALLOWED_HOSTS`        | `<HF-username>-mlflow-server.hf.space,localhost,127.0.0.1`                                                               | Allowed hosts                       |
| `MLFLOW_CORS_ALLOWED_ORIGINS` | `https://<HF-username>-mlflow-server.hf.space,localhost,127.0.0.1`                                                       | CORS configuration                  |

---

## 6. Access your MLflow server

Once deployed, your MLflow instance will be available at:

```
https://<HF-username>-mlflow-server.hf.space
```

To connect from a local machine or another service, set your tracking URI:

```bash
export MLFLOW_TRACKING_URI=https://<HF-username>-mlflow-server.hf.space
```
