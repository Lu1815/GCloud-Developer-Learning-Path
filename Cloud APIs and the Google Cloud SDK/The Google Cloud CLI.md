# The Google Cloud CLI

## Introduction
The Google Cloud Command Line Interface (CLI), or gcloud CLI, provides a set of tools to manage Google Cloud services directly from the command line or automated scripts. These tools offer the functionality of Cloud APIs in a user-friendly command-line format, automating credential handling and combining multiple API calls for common tasks.

## Key Features of gcloud CLI
1. **Comprehensive Management**:
   - Manage virtual machines, deploy applications, and perform most tasks allowed by Cloud APIs.
   - Includes various command-line tools, such as gcloud for general tasks, gsutil for Cloud Storage, and bq for BigQuery.

2. **Automation and Scripting**:
   - Automates the process of sending credentials in API calls.
   - Combines multiple Cloud API calls to complete single, common tasks.

## Common Command-Line Tools
1. **gcloud**:
   - **General Management**: Use gcloud to perform a wide range of tasks on Google Cloud, including creating and managing resources for many services.
   - **Example Command**: `gcloud compute instances list` - Lists the Compute Engine virtual machine instances for your project.
   - **Managing CLI Components**: Use `gcloud components list` to describe each CLI component and its status (not installed, update available, or installed). Install or update components using `gcloud components install [component]` and `gcloud components update`.

2. **gsutil**:
   - **Cloud Storage Management**: Manage Cloud Storage buckets and objects.
   - **Commands**: Create, list, delete, and manage access control lists for buckets and objects. Perform operations like copying, moving, listing, and deleting objects.
   - **Preferred Tool**: `gcloud storage` is now the preferred tool for managing Cloud Storage, offering better performance and a command structure similar to other gcloud commands.
   - **Example Commands**:
     - `gcloud storage buckets create` - Creates a new bucket.
     - `gcloud storage objects cp [source] [destination]` - Copies a file from your local machine into a Cloud Storage bucket.

3. **bq**:
   - **BigQuery Management**: A command-line tool for managing BigQuery, Google Cloud's serverless, highly scalable, and cost-effective data warehouse.
   - **Primary Purpose**: Running queries, managing datasets, tables, and other BigQuery entities.
   - **Example Command**: A query searching for all occurrences of a word in a sample public dataset containing the complete word index of Shakespeare's works.

## Detailed Commands and Examples
1. **Listing Compute Engine Instances**:
   ```sh
   gcloud compute instances list
   ```

2. **Managing CLI Components**:
   - List Components:
     ```sh
     gcloud components list
     ```
   - Install a Component:
     ```sh
     gcloud components install kubectl
     ```
   - Update CLI:
     ```sh
     gcloud components update
     ```

3. **Managing Cloud Storage**:
   - Create a Bucket:
     ```sh
     gcloud storage buckets create [bucket-name]
     ```
   - Copy a File to a Bucket:
     ```sh
     gcloud storage cp [local-file-path] gs://[bucket-name]
     ```

4. **Running BigQuery Queries**:
   - Example Query:
     ```sh
     bq query --use_legacy_sql=false 'SELECT word, word_count FROM `bigquery-public-data.samples.shakespeare` WHERE word = "love" ORDER BY word_count DESC'
     ```

## Conclusion
The Google Cloud CLI is a powerful set of tools for managing Google Cloud services efficiently from the command line. By using the gcloud, gsutil, and bq tools, you can automate tasks, manage resources, and run queries seamlessly, enhancing your ability to work with Google Cloud services effectively.