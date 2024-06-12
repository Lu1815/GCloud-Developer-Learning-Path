# Choosing an Authentication Method for Google Cloud APIs

## Overview
When developing applications that interact with Google Cloud APIs, selecting the appropriate authentication method is crucial. This guide helps you determine which method to use based on whether your application is running on Google Cloud, Google Kubernetes Engine (GKE), or outside Google Cloud.

## Decision Diagram
The decision process for choosing an authentication method involves several key questions:

### 1. Is Your Application Running on Google Cloud?
- **Yes**: Proceed to determine if the application is running on Google Kubernetes Engine (GKE).
- **No**: Proceed to decide if federation is possible.

### 2. Is Your Application Running on Google Kubernetes Engine (GKE)?
- **Yes**: Use **Workload Identity**.
  - **Workload Identity**: Allows workloads in GKE clusters to impersonate IAM service accounts to access Google Cloud APIs securely and manageably.
- **No**: Use the following methods based on your environment:
  - **Local Development**: Use `gcloud auth application-default login`.
  - **Production (Non-local)**: Attach a service account directly to the compute or serverless instance on Google Cloud.

### 3. Is Federation Possible for External Applications?
- **Yes**: Use **Workload Identity Federation**.
  - **Workload Identity Federation**: Allows workloads running in other clouds or on-premises to exchange an external provider token for a Google Cloud access token, enabling service account impersonation without a service account key.
- **No**: Use **Service Account Keys** as a last resort, ensuring the best security practices.

## Detailed Methods

### Local Development Environment
- **Command**: `gcloud auth application-default login`
  - **Description**: Generates a JSON file containing user-access credentials and places it in a well-known location for Application Default Credentials (ADC) to find.
  - **Usage**: Allows the application to make API calls with your user identity. The JSON file is secure, does not include your password, and is time-bound.

### Google Cloud Services (Non-GKE)
- **Attached Service Accounts**: Attach a service account to your Compute Engine VM, Cloud Run service, or Cloud Function.
  - **Best Practice**: Replace the default service account with a specific service account created for the application, granting only the necessary privileges.

### Google Kubernetes Engine (GKE)
- **Workload Identity**: Recommended for secure and manageable access to Google Cloud APIs.
  - **Process**:
    1. Enable Workload Identity on your GKE cluster.
    2. Allow the Kubernetes service account to impersonate the IAM service account.
    3. ADC manages the token exchange.

### External Applications (Federation Possible)
- **Workload Identity Federation**: Use for multi-cloud or on-premises workloads.
  - **Process**:
    1. Use an identity provider that supports OpenID Connect.
    2. Exchange the OpenID Connect ID token for a short-lived Google Cloud access token.
    3. Impersonate an IAM service account without requiring a service account key.

### External Applications (Federation Not Possible)
- **Service Account Keys**: Use as a last resort.
  - **Best Practices**:
    - Generate and manage keys securely.
    - Upload a public key instead of downloading a private key.
    - Avoid embedding keys in source code or binaries.
    - Follow the principle of least privilege by granting minimal permissions.

## Application Default Credentials (ADC)
ADC is used by Cloud Client Libraries to find application credentials and allows seamless transitions between environments.

### ADC Credential Search Order
1. **Environment Variable**: Checks for `GOOGLE_APPLICATION_CREDENTIALS`.
2. **gcloud CLI**: Checks a well-known location for user credentials set by the gcloud CLI.
3. **Attached Service Account**: Uses the service account attached to the service or function.
4. **Default Service Account**: Uses the default service account for services like Compute Engine, GKE, Cloud Run, or Cloud Functions.

## Example: Python Function with ADC
- **Code**: Automatically finds credentials to make authenticated API requests without specifying credentials explicitly.

```python
from google.cloud import storage

def upload_to_bucket(bucket_name, source_file_name, destination_blob_name):
    storage_client = storage.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(destination_blob_name)
    blob.upload_from_filename(source_file_name)
    print(f'File {source_file_name} uploaded to {destination_blob_name}.')
```

## Conclusion
Choosing the right authentication method for Google Cloud APIs depends on your application's environment. Use the decision diagram and best practices outlined in this guide to ensure secure and effective authentication for your applications.