### IAM-Risk-Analytics-Dashboard

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

🧠 2. SAMPLE SQL TABLE CREATION
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    username VARCHAR(50),
    department VARCHAR(50),
    job_role VARCHAR(50),
    status VARCHAR(20),
    created_date DATE,
    last_login_date DATE
);

CREATE TABLE roles (
    role_id INT PRIMARY KEY,
    role_name VARCHAR(50),
    risk_level VARCHAR(20)
);

CREATE TABLE user_roles (
    user_id INT,
    role_id INT,
    assigned_date DATE
);

CREATE TABLE access_logs (
    log_id INT PRIMARY KEY,
    user_id INT,
    login_time TIMESTAMP,
    ip_address VARCHAR(50),
    access_type VARCHAR(50)
);

CREATE TABLE permissions (
    permission_id INT PRIMARY KEY,
    role_id INT,
    resource VARCHAR(50),
    access_level VARCHAR(20)
);

📊 3. KEY IAM METRICS (SQL QUERIES)
🔹 Inactive Users
SELECT COUNT(*) AS inactive_users
FROM users
WHERE last_login_date < CURRENT_DATE - INTERVAL '90 days';

🔹 High-Risk Users
SELECT u.username, r.risk_level
FROM users u
JOIN user_roles ur ON u.user_id = ur.user_id
JOIN roles r ON ur.role_id = r.role_id
WHERE r.risk_level = 'High';

🔹 Privileged Access (Admin)
SELECT COUNT(DISTINCT user_id) AS admin_users
FROM permissions p
JOIN user_roles ur ON p.role_id = ur.role_id
WHERE p.access_level = 'Admin';

🔹 Login Activity Trend
SELECT DATE(login_time) AS login_date, COUNT(*) AS logins
FROM access_logs
GROUP BY DATE(login_time)
ORDER BY login_date;

🔹 Users with Multiple Roles (Risk Indicator)
SELECT user_id, COUNT(role_id) AS role_count
FROM user_roles
GROUP BY user_id
HAVING COUNT(role_id) > 1;

📈 4. DASHBOARD DESIGN (POWER BI / TABLEAU)

## Visuals to Include

## KPI Cards:

Total Users
Inactive Users
High-Risk Users

## Bar Chart:
Users by Risk Level

## Line Chart:
Login Trends

## Table:
Users with multiple roles
