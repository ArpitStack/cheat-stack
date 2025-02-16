# GCP CLI Cheatsheet

A practical guide covering essential GCP CLI commands for managing Google Cloud resources efficiently.

## Table of Contents

- [Authentication & Setup](#authentication--setup)
- [Project Management](#project-management)
- [Compute Engine (VMs)](#compute-engine-vms)
- [Cloud Storage](#cloud-storage)
- [IAM & Security](#iam--security)
- [Networking](#networking)
- [Kubernetes Engine (GKE)](#kubernetes-engine-gke)
- [Cloud SQL](#cloud-sql)
- [BigQuery](#bigquery)
- [Logging & Monitoring](#logging--monitoring)
- [Cloud Functions](#cloud-functions)
- [Billing & Cost Management](#billing--cost-management)

## Authentication & Setup

Authenticate and set up GCP CLI:

```bash
gcloud auth login
gcloud auth application-default login
```

Set default project:

```bash
gcloud config set project <PROJECT_ID>
```

List available projects:

```bash
gcloud projects list
```

## Project Management

Create a new project:

```bash
gcloud projects create <PROJECT_ID>
```

Delete a project:

```bash
gcloud projects delete <PROJECT_ID>
```

## Compute Engine (VMs)

List all VM instances:

```bash
gcloud compute instances list
```

Create a new VM instance:

```bash
gcloud compute instances create <INSTANCE_NAME> --zone=<ZONE>
```

Start/Stop/Delete an instance:

```bash
gcloud compute instances start <INSTANCE_NAME>
gcloud compute instances stop <INSTANCE_NAME>
gcloud compute instances delete <INSTANCE_NAME>
```

## Cloud Storage

List buckets:

```bash
gcloud storage buckets list
```

Create a new bucket:

```bash
gcloud storage buckets create <BUCKET_NAME> --location=<REGION>
```

Upload and download files:

```bash
gcloud storage cp <LOCAL_FILE> gs://<BUCKET_NAME>/
gcloud storage cp gs://<BUCKET_NAME>/<FILE_NAME> <LOCAL_DESTINATION>
```

Delete a bucket:

```bash
gcloud storage buckets delete <BUCKET_NAME>
```

## IAM & Security

List IAM policies:

```bash
gcloud projects get-iam-policy <PROJECT_ID>
```

Add IAM role to a user:

```bash
gcloud projects add-iam-policy-binding <PROJECT_ID> --member=user:<EMAIL> --role=<ROLE>
```

Remove IAM role from a user:

```bash
gcloud projects remove-iam-policy-binding <PROJECT_ID> --member=user:<EMAIL> --role=<ROLE>
```

## Networking

List all networks:

```bash
gcloud compute networks list
```

Create a new VPC network:

```bash
gcloud compute networks create <NETWORK_NAME> --subnet-mode=auto
```

List firewall rules:

```bash
gcloud compute firewall-rules list
```

Create a firewall rule:

```bash
gcloud compute firewall-rules create <RULE_NAME> --allow tcp:80
```

## Kubernetes Engine (GKE)

List all clusters:

```bash
gcloud container clusters list
```

Create a Kubernetes cluster:

```bash
gcloud container clusters create <CLUSTER_NAME> --num-nodes=3 --zone=<ZONE>
```

Get credentials for a cluster:

```bash
gcloud container clusters get-credentials <CLUSTER_NAME> --zone=<ZONE>
```

Delete a cluster:

```bash
gcloud container clusters delete <CLUSTER_NAME>
```

## Cloud SQL

List all Cloud SQL instances:

```bash
gcloud sql instances list
```

Create a new Cloud SQL instance:

```bash
gcloud sql instances create <INSTANCE_NAME> --database-version=MYSQL_8_0 --tier=db-f1-micro --region=<REGION>
```

Connect to Cloud SQL instance:

```bash
gcloud sql connect <INSTANCE_NAME> --user=root
```

Delete an instance:

```bash
gcloud sql instances delete <INSTANCE_NAME>
```

## BigQuery

List all datasets:

```bash
gcloud bigquery datasets list
```

Create a new dataset:

```bash
gcloud bigquery datasets create <DATASET_NAME>
```

Run a SQL query:

```bash
gcloud bigquery query "SELECT * FROM \`<PROJECT_ID>.<DATASET>.<TABLE>\` LIMIT 10;"
```

Delete a dataset:

```bash
gcloud bigquery datasets delete <DATASET_NAME>
```

## Logging & Monitoring

List all logs:

```bash
gcloud logging logs list
```

View log entries:

```bash
gcloud logging read "resource.type=gce_instance" --limit 10
```

List monitoring metrics:

```bash
gcloud monitoring metrics list
```

## Cloud Functions

List all cloud functions:

```bash
gcloud functions list
```

Deploy a Cloud Function:

```bash
gcloud functions deploy <FUNCTION_NAME> --runtime=nodejs20 --trigger-http --allow-unauthenticated
```

Invoke a function:

```bash
gcloud functions call <FUNCTION_NAME>
```

Delete a function:

```bash
gcloud functions delete <FUNCTION_NAME>
```

## Billing & Cost Management

List billing accounts:

```bash
gcloud beta billing accounts list
```

Set billing account for a project:

```bash
gcloud beta billing projects link <PROJECT_ID> --billing-account=<BILLING_ACCOUNT_ID>
```