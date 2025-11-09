# Test MLflow Tracking URI

This folder is used to **validate your MLflow Tracking Server connection** and ensure that model logging, registration, and loading work correctly across different environments.

It provides a simple end-to-end test based on the **official MLflow documentation**, including:

* `register_model.py`: trains and registers a model.
* `test_model.py`: loads and uses the registered model.

---

## 1. Configuration

Before running the scripts, open each Python file and verify the following variables at the top of the code.

### In `register_model.py`:

```python
#### TO COMPLETE #######
MLFLOW_TRACKING_URI = 'http://localhost:5000'
EXPERIMENT_NAME = 'test'
########################
```

### In `test_model.py`:

```python
#### TO COMPLETE #######
MLFLOW_TRACKING_URI = 'http://localhost:5000'
########################
```

* Replace the `MLFLOW_TRACKING_URI` with the address of your MLflow server:

  * Local run → `http://localhost:5000`
  * Hugging Face Space → `https://<HF-username>-mlflow-server.hf.space`
  * Any remote instance → your deployed endpoint URL
* Optionally, update the `EXPERIMENT_NAME` as needed.

---

## 2. Setup

Navigate to the folder containing these scripts:

```bash
cd test_tracking_URI
```

Then make sure that:

* The **`mlflow`** library is installed and accessible in your Python environment.
* The necessary **credentials** (S3, PostgreSQL, or other backend configuration) are properly set based on the deployment you’re testing.

You can verify MLflow installation with:

```bash
python -m pip show mlflow
```

---

## 3. Run the training and model registration

Run the first script to train and register a simple model:

```bash
python register_model.py
```

This script will:

* Create (or use) the experiment defined by `EXPERIMENT_NAME`.
* Train a basic model using the official MLflow example.
* Log parameters, metrics, and artifacts.
* Register the trained model under the name defined in the script.

---

## 4. Test model loading and inference

Once the model is registered, run the test script to load and use it:

```bash
python test_model.py
```

This script will:

* Connect to the same `MLFLOW_TRACKING_URI`.
* Retrieve the latest version of the registered model.
* Perform a simple inference to confirm everything works.

---

## 5. Validation

If both scripts complete successfully:

* Your tracking server is reachable.
* Credentials and storage configuration are correct.
* Model registration and loading are fully functional.

If any errors occur, check:

* The server logs or Hugging Face Space logs.
* Network or credential issues.
* The experiment and model names.
