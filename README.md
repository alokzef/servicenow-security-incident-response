# Automated Security Incident Response (SIRT) Triage

A custom ServiceNow application designed to automate the detection, prioritization, and routing of critical security incidents. This project minimizes incident response lifecycle times by eliminating manual sorting and establishing immediate communication channels for high-risk infrastructure threats.

## 🚀 Key Features
* **Dynamic Incident Triage:** Automatically intercepts incoming security alerts and assesses priority based on custom impact and urgency matrix rules.
* **Flow Designer Automation:** Utilizes backend workflows to dynamically evaluate records and manage assignment groups.
* **Notification Engine:** Built-in outbound communication configurations to instantly alert remediation teams regarding high-severity breaches.
* **Source Control Integration:** Fully linked with GitHub via ServiceNow Studio to enable standard CI/CD tracking and backup.

---

## 📂 Application Structure

This repository contains the metadata and configuration files exported directly from ServiceNow Studio. The key application files are organized into the following logical layers:

* **`1c2ba4b7937143108988fc20ed03d6b5/` (Application Scope Folder):** The primary data directory hosting all custom records built for this application scope.
    * **Data Schema:** Houses the definitions, fields, layout views, and access controls (ACLs) for the custom `Security Incident Ticket` table.
    * **User Interface:** Contains form layouts, list views, and module configurations optimized for security analysts.
* **`Automation / Flows`:** Holds the metadata configuration for the **`Triage Security Incident`** flow created in Flow Designer. This engine acts as the core listener that triggers processing on incident creation.
* **`sn_source_control.properties`:** System tracking configurations used by the ServiceNow Git engine to handle continuous integration mappings.

---

## 🛠️ Setup & Installation Guide

To import this application into a ServiceNow Personal Developer Instance (PDI) or an enterprise sandbox, follow these setup steps:

### Prerequisites
1. A ServiceNow Personal Developer Instance (PDI) running a compatible family release (e.g., Washington or Xanadu).
2. A GitHub account with a Personal Access Token (Classic) generated containing the `repo` scope permission.

### Step 1: Create a Basic Authentication Credential in ServiceNow
Because ServiceNow requires secure platform handshakes to pull files from GitHub, you must register your token inside the platform instance:
1. Log into your main ServiceNow platform interface.
2. In the Filter Navigator, type `discovery_credentials.list` and hit **Enter**.
3. Click **New** and select **Basic Auth Credentials**.
4. Configure the record with the following settings:
    * **Name:** `GitHub - <your-username>`
    * **User name:** Your GitHub account username.
    * **Password:** Paste your GitHub **Personal Access Token (`ghp_...`)**.
5. Click **Submit**.

### Step 2: Import the Application via ServiceNow Studio
1. In your ServiceNow instance, open the Filter Navigator, type **`Studio`**, and click on it to launch the development environment.
2. In the application selection modal window, click the **Import from Source Control** button.
3. Provide the following integration parameters:
    * **URL:** `https://github.com/alokzef/servicenow-security-incident-response.git`
    * **Credential:** Select the `GitHub - <your-username>` profile you created in Step 1.
    * **Branch:** Leave empty or set to the default branch to pull the core application structure.
4. Click **Import**. ServiceNow will pull down the metadata, compile the components, and instantly activate the application tables and flows inside your instance.

### Step 3: Activating the Core Components
* **Forms & Fields:** Navigate to `Security Incident Ticket` in your application menu to view or modify the data entry forms.
* **Workflow Automation:** Open **Flow Designer**, locate the `Triage Security Incident` flow, and ensure it is toggled to **Active** so it intercepts real-time incoming records.
*
