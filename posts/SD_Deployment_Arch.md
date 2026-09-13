---
aliases:
- /markdown/2026/09/13/DeploymentArchitecture
categories:
- SD
date: '2026-09-13'
description: Deployment Architecture
image: /images/SD/DeploymentArchitecture.png
layout: post
title: GCP Deployment Architecture
toc: true

---
We'll be discussing about deployment architecture using GCP for both realtime serving and batch serving

## Realtime Deployment Architecture

![Realtime Serving Architecture](/blog/images/SD/realtime_deploy.png)

### Step by Step RT Pipeline Description:

Step 1: Code Push & Jenkins Trigger
    * Trigger : A developer pushes changes (DAG definitions, pyspark scripts or SQL logic) to the Git repository (GitHub, Gitlab, Bitbucket).

    * Jenkins Pipeline Invocation : A webhook notifies the jenkins master server, which executes the defined Jenkinsfile pipeline.

Step 2: Continuous Integration & Pre-Flight Testing (Jenkins)
    * Authentication: Jenkins authenticates with Google Cloud Platform using a dedicated GCP Service Account key stoored in the Jenkins Credetials Manager.

    * Code Checkout: Jenkins pulls the latest code revision and extracts the short Git commit SHA for version tracking.

    * Automated Testing: Jenkins creates a isolated virtual environment to execute unit tests, validate API contract definitions, and verify that model loading dependencies compile without erros.

Step 3: Container Build & Storage (Cloud Build & Artifact Registry)
    * Delegation to Cloud Build: Jenkins calls the Google Cloud SDKL to offload containerzation tasks directly to GCP Cloud Build.

    * Image Packaging: Cloud Build creates a production-ready Docker container image containing: The FastAPI web framework, GCP serving libraries, the compiled prediction model artifact, and a health check endpoint.  

    * Tagging & Pushing: The container image is tagged with the unique Git commit SHA and pushed to GCP Artifact Registry for centralized registry management. 

Step 4: Model Artifact Resolution (Cloud Storage): 

    * Large ML model files (e.g. binaries , weights, serizlized model files) are maintained separately from the container code in a high-durability GCS bucket.

    * When the cintainer initilzes, it downloads the artifacts from the GCS bucket based on the version specified in the request. This ensures that the model artifacts are versioned and can be rolled back independently of the code. 

Step 5: Serverless Deployment & Traffic Routing (Cloud Run)
    * Revision Rollout : Cloud Build issues a deployment command to Cloud Run, creating a new, immutable revision of the serverless microservice using the newly pushed Artifact Registry image.

    * Zero-Downtime Traffic Shift: Cloud Run verifies cointainer startup health checks before automatically shifting 100% of live traffic from the old revision to the new revision.

    * Auto-Scaling Configuration: Cloud Run automatically scales instances up or down based on CPU utilization or request count. The concurrency setting defines the maximum number of requests a single container instance can handle simultaneously.

Step 6: Pipeline health Check & Verificaiton 
    * Once deployment finishes, jenkins retrieves the public/authenticated Cloud Run HTTPS endpoint URL.
    * Jenkins executes an automated health probe(/health) against the live Cloud Run endpoint to confirm the service is operational.
    * Upon receiving a successful response, jenkins marks the pipeline execution as complete and cleans up the build workspace.


## Batch Deployment Architecture

![Batch Serving Architecture](/blog/images/SD/batch_deploy.png)

### Step by Step Batch Pipeline Description

Step 1: Code Push & Jenkins Trigger
    * Trigger : A developer pushes changes (DAG definitions, pyspark scripts or SQL logic) to the Git repository (GitHub, Gitlab, Bitbucket).

    * Jenkins Pipeline Invocation : A webhook notifies the jenkins master server, which executes the defined Jenkinsfile pipeline on an agent node.

Step 2: Continuous Integration & Pre-Flight Testing (Jenkins Agent)
    * DAG Syntax & Cycle Verification : Jenkins creates an isolated Python virtual environment to parse the Apache Airflow DAGs locally. It verifies there are no import errors, missing task dependencies, or circular loops before pushing to GCP.

    * Unit Testing: Jenkins runs pytest to execute unit test on feature manipulation functions, SQL templates, and custom Airflow operators.

Step 3:GCP Authentication
    * Authentication : Jenkins authenticates to Google Cloud Platform using either:
        1. A secured GCP Service Account JSON key stored within the Jenkins Credentials Manager.
        2. Workload Identify Federation via the Jenkins OIDC plugin for keyless authentication.
    * Project Context: Jenkins configures the gcloud CLI session for the designated target GCP Project and Region

Step 4: Deployment & DAG Synchronization
    * DAG Sync: Jenkins copies the validated Python DAG files from the agent node's workspace to the Google Cloud Composer Environment's DAGs folder (usually a GCS bucket like gs://<composer-env-name>-data/dags).
    
    * Build Staging Containers (If Applicable): If custom Python packages or ML dependencies are required beyond the base Composer image, Jenkins triggers a Docker build on the agent node. It pushes the newly built container image to Google Container Registry (GCR) or Artifact Registry for the project. 

Step 5: Scheduled Batch Serving Execution (Cloud Composer & Vertex AI)
    * DAG Execution: On its scheduled interval (or via event triggers), cloud composer runs the deployed Airflow DAG.

    * Feature Extraction: Airflow triggers a BigQuery job (or Dataproc cluster) to extract and prepare raw input features, placing them into a staging area (BigQuery temporary table or GCS .jsonl/.parquet bucket)

    * Vertex AI Batch Job: Airflow invokes the Vertex AI Batch Prediction API. Vertex AI automatically provisions an ephemeral compute cluster, loads the specified model artifact from the vertex AI Model Registry, processes the staged data in parallel, and writes prediction results directly to Bigquery.

    * Cluster Deprovisioning: Upon completion, Vertex AI automatically tears down the compute cluster to eliminate idle infrastructure costs.

Step 6: Post-Processing & Notification
    * Data Quality Validation: A BigQuery SQL operator runs automated data quality checks on the prediction output (e.g., ensuring score distributions are within expected ranges, checking for missing values).

    * Notification: If the data quality checks pass, the DAG triggers a notification (via Cloud Pub/Sub, Slack, or Email) to the Data Engineering or Analytics team, signaling that the batch predictions are ready for consumption.