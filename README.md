### IAM-Risk-Analytics-Dashboard
IAM Risk &amp; Access Analytics Dashboard

IAM Risk & Access Analytics Dashboard

### Overview

This project simulates a real-world Identity & Access Management (IAM) environment by analysing user access data to identify security risks and support data-driven decision-making.

The goal is to provide visibility into access control, risk exposure, and IAM operational metrics through an interactive dashboard.

### Business Problem

Organisations often lack visibility into:

Who has access to what systems
Which accounts pose security risks
How access patterns impact compliance

This creates risks such as:

- Over-privileged users
- Dormant/inactive accounts
- Unmonitored access behaviour

### Solution

Built an interactive dashboard to monitor IAM metrics and highlight risk areas, enabling stakeholders to take corrective action.

### Key Features
📊 Access Risk Dashboard (Low / Medium / High)
🔐 Privileged Account Monitoring
⏳ Inactive User Detection
📈 Access Activity Trends
🎯 KPI Tracking for IAM performance

### Tech Stack

SQL (data modelling & transformation)
Python (data cleaning & simulation)
Power BI / Tableau (visualisation)

### Data Model

Simulated IAM dataset including:

1. Users
2. Roles
3. Permissions
4. Login Activity
5. Risk Scores

### Key Insights

Identified high percentage of inactive accounts → potential security vulnerability
Detected concentration of privileged access in specific roles
Highlighted unusual access patterns indicating possible risk

### Business Impact

Improves visibility into access control risks
Supports compliance and audit readiness
Enables proactive risk mitigation

### How to Run

Load dataset into SQL / Snowflake
Run transformation scripts
Connect Power BI / Tableau to dataset
Open dashboard file

### Author Note (IMPORTANT)

This project was built to demonstrate how data analytics can support IAM and cybersecurity decision-making, bridging the gap between data and security operations.


1. DATASET DESIGN (REALISTIC IAM MODEL)

--- You will create 5 core tables:

1. users
user_id (INT)
username (VARCHAR)
department (VARCHAR)
job_role (VARCHAR)
status (VARCHAR)  -- Active / Inactive
created_date (DATE)
last_login_date (DATE)

2. roles
role_id (INT)
role_name (VARCHAR)
risk_level (VARCHAR)  -- Low / Medium / High

3. user_roles
user_id (INT)
role_id (INT)
assigned_date (DATE)

4. access_logs
log_id (INT)
user_id (INT)
login_time (TIMESTAMP)
ip_address (VARCHAR)
access_type (VARCHAR) -- Login / File Access / Admin Action

5. permissions
permission_id (INT)
role_id (INT)
resource (VARCHAR)
access_level (VARCHAR) -- Read / Write / Admin
