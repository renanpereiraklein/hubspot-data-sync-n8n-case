# HubSpot Contact Sync & Association Engine (n8n)

This repository showcases a professional production-grade workflow developed in **n8n**. It automates the extraction of contact data from an external API, performs advanced data transformation, and synchronizes the results with **HubSpot CRM**, including complex object associations and multi-layered error handling.

This project demonstrates expertise in ETL (Extract, Transform, Load), API integration, and automation reliability.

---

## 📌 Project Overview

The workflow automates the following lifecycle:

* **Paginated Data Ingestion**: Consumes data from an external AWS Lambda endpoint with dynamic pagination logic.
* **Data Normalization**: Uses JavaScript expressions to sanitize strings and split full names into `firstName` and `lastName`.
* **HubSpot Integration**: Performs Upsert operations on Contacts and establishes default associations with Companies via the HubSpot CRM v4 API.
* **Batch Processing**: Implements a `Split In Batches` strategy to optimize performance and respect API rate limits.
* **Fault Tolerance**: Continues execution on individual item errors and routes failures to dedicated audit logs.

---

## 🏗️ Technical Architecture

The workflow follows a structured logic flow:

1.  **Context Discovery**: Retrieves the "Origin Company" and associated company IDs from HubSpot.
2.  **External Sync**: Fetches contact records using an HTTP Request node with an automated "Complete Expression" to handle pagination.
3.  **Transformation**: Maps incoming properties (Email, Address, City, State) into a standard format.
4.  **Processing Loop**: Processes contacts in batches of 5 to ensure stability.
5.  **Audit & Observability**: 
    * **Success**: Sends a styled HTML email report via Gmail upon completion.
    * **Failure**: Logs specific "Upsert Errors" and "Association Errors" into internal n8n DataTables for manual review.

---

## 🛠️ Tools & Technologies

* **n8n**: Core orchestration engine.
* **HubSpot CRM API (v2.2 & v4)**: Contact and Company management.
* **JavaScript (Node.js)**: Advanced string manipulation and logic.
* **AWS API Gateway/Lambda**: External data source.
* **Gmail API**: Automated notification system.

---

## ⚠️ Disclaimers & Setup

> [!IMPORTANT]
> **Security/Sanitization**: This JSON file has been sanitized. All API Tokens, Credential IDs, personal emails, and instance-specific IDs have been removed or replaced with `REDACTED` placeholders for security.

> [!WARNING]
> **Functionality**: After importing the JSON, you must re-link your own HubSpot and Gmail credentials. Internal `DataTable` nodes will need to be re-pointed to your specific tables to avoid execution errors.

---

### How to Use
1. Copy the content of `workflow_sanitized.json`.
2. In n8n, create a new workflow and paste (`Ctrl+V`).
3. Configure your credentials and update the `Origin Company` ID.
