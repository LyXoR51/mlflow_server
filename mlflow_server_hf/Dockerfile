FROM ghcr.io/mlflow/mlflow

RUN pip install --no-cache-dir \
    boto3 \
    psycopg2-binary

CMD mlflow server \
    --host 0.0.0.0 \
    --port ${PORT} \
    --backend-store-uri "${BACKEND_STORE_URI}" \
    --default-artifact-root "${ARTIFACT_STORE_URI}" \
    --allowed-hosts "${MLFLOW_ALLOWED_HOSTS}" \
    --cors-allowed-origins "${MLFLOW_CORS_ALLOWED_ORIGINS}"