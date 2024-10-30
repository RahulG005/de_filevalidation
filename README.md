# Project Overview: 
The goal was to create a robust pipeline to validate incoming CSV files for schema conformity, including file name and date formats, and manage them efficiently.



# Project Architecture
![Project architecture](https://github.com/user-attachments/assets/119ab18c-118a-4ee7-8f9a-f8b33e084f97)


# Components Used:

Azure Data Factory (ADF): Orchestrates the workflow with linked services for Azure Data Lake Storage, Databricks, and Key Vault.

Databricks: Runs validation logic using parameters passed from ADF.

Azure Data Lake Storage: Acts as the landing zone for incoming files.

Key Vault: Secures sensitive information including SAS tokens and database credentials.

Azure SQL Database: Stores schema details for validation reference.

# How It Works:

**File Drop**: When a file is dropped in the landing folder, a storage event trigger in ADF captures the fileName and triggers the pipeline.

**ADF Pipeline**: Passes the fileName parameter to a Databricks notebook.

**Databricks Notebook**:

Accesses necessary credentials from Key Vault.

Mounts the storage account and connects to Azure SQL Database.

Retrieves schema details from the database to validate the file.

Checks for:

Presence of fileName in schema details.

Duplication in data.

Date column names and formats.

Moves the file to either the validated or rejected folder based on the checks.

# Outcome: 
An automated, secure, and efficient process for validating and managing incoming data files, ensuring data integrity and streamlining our workflow.
