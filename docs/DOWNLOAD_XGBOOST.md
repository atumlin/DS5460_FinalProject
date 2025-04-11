# Running XGBoost with PySpark on Google Cloud Dataproc

This guide walks you through setting up a Google Cloud Dataproc cluster with support for XGBoost4J-Spark to run `SparkXGBRegressor`.

---

## Requirements

- Google Cloud account with billing enabled
- Access to Google Cloud Shell
- `gcloud` CLI already authenticated
- A GCS bucket (e.g., `gs://bucket-name`)
- Region and zone (e.g., `us-east5`, `us-east5-a`)

---

## Step 1: Create an Init Script

This script installs the required XGBoost JARs on all nodes.

### 1. Open Cloud Shell and create the script:

```bash
nano xgboost-init.sh
```
#### 2. Paste the following:
```bash
#!/bin/bash

# Install Python xgboost
sudo /opt/conda/default/bin/pip install xgboost==1.7.6
```

### 3. Save and exit:
- `Ctrl + O` to write the file, then press enter 
- `Ctrl + X` to exit the editor 

## Step 2: Upload the Script to GCS 
```bash 
gsutil cp xgboost-init.sh gs://bucket-name/scripts/xgboost-init.sh
```

## Step 3: Create the Dataproc Cluster
Something like this but don't forget to insert your own desired information.
```bash 
gcloud dataproc clusters create xgb-cluster \
  --region=us-east5 \
  --zone=us-east5-a \
  --image-version=2.1-debian11 \
  --enable-component-gateway \
  --optional-components=JUPYTER \
  --initialization-actions=gs://bucket-name/scripts/xgboost-init.sh \
  --bucket=dbucket-name \
  --master-machine-type=e2-standard-2 \
  --worker-machine-type=e2-standard-2 \
  --num-workers=2
```
## Step 4. Access Jupyter via Dataproc Cluster 

## Step 5. Import and Use SparkXGBRegressor 
Run in your notebook,
```bash
from xgboost.spark import SparkXGBRegressor
```
