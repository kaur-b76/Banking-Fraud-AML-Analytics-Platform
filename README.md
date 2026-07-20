# Banking-Fraud-AML-Analytics-Platform

# Banking Fraud & AML Transaction Monitoring Analytics Platform

## Project Overview

Banks and financial institutions process large volumes of transactions every day. Identifying potentially fraudulent activity, monitoring suspicious transactions, prioritizing high-risk alerts, and supporting Anti-Money Laundering (AML) investigations are important responsibilities for fraud, risk, compliance, and financial crime teams.

The objective of this project is to develop an end-to-end **Banking Fraud and AML Transaction Monitoring Analytics Platform** using Python, SQL Server, and Power BI.

The project simulates a banking transaction monitoring environment using synthetic customer, account, and transaction data. The generated datasets include fraud indicators, AML alerts, customer risk levels, transaction risk scores, Politically Exposed Person (PEP) indicators, sanctions indicators, transaction velocity flags, potential structuring patterns, fraud losses, and investigation statuses.

The project demonstrates how banking transaction data can be generated, stored, validated, analyzed, and visualized to support data-driven fraud and AML monitoring.

---

## Business Problem

Financial institutions need to analyze large volumes of transaction data to identify suspicious activities and potential financial crime risks.

Fraud and AML teams need to answer questions such as:

- What is the overall fraud rate?
- How much money has been lost due to fraudulent transactions?
- Which transaction types and payment methods have the highest fraud exposure?
- Which customers generate the highest number of suspicious transactions?
- Which countries and geographic locations generate the most AML alerts?
- Are high-risk customers associated with greater fraud losses?
- Which transactions demonstrate unusual transaction velocity?
- Which customers demonstrate potential structuring activity?
- How many fraud and AML investigation cases are currently open, under review, escalated, or closed?
- Which high-risk transactions should investigators prioritize?

The purpose of this project is to build an analytics solution that helps answer these questions using SQL-based analysis and interactive Power BI dashboards.

---

## Project Objectives

The primary objectives of this project are to:

- Generate realistic synthetic banking data using Python.
- Simulate customer, account, transaction, fraud, and AML-related attributes.
- Store and manage large transaction datasets using SQL Server.
- Perform data validation and data quality checks.
- Analyze fraud and AML patterns using SQL.
- Apply SQL concepts including JOINs, CTEs, CASE statements, subqueries, window functions, aggregations, and views.
- Identify high-risk customers and suspicious transaction patterns.
- Analyze fraud losses across multiple business dimensions.
- Monitor AML alerts and investigation cases.
- Develop interactive Power BI dashboards for fraud, AML, customer risk, and investigation monitoring.
- Translate complex transaction data into actionable business insights.

---

# Technology Stack

| Technology       | Purpose                              | Version        |
| ---------------- | ------------------------------------ | -------------- |
| Python           | Synthetic banking dataset generation | 3.x            |
| Pandas           | Data manipulation                    | Latest         |
| NumPy            | Synthetic data generation            | Latest         |
| Faker            | Customer data generation             | Latest         |
| Jupyter Notebook | Dataset generation                   | Latest         |
| PostgreSQL       | Relational database                  | **18**         |
| pgAdmin 4        | PostgreSQL administration            | **Latest**     |
| SQL              | Fraud & AML analysis                 | PostgreSQL SQL |
| Power BI         | Dashboard development                | Desktop        |
| GitHub           | Version control & documentation      | Latest         |


# Project Workflow

The project follows an end-to-end analytics workflow:

Python Synthetic Data Generation

↓

CSV Dataset Export

↓

SQL Server Database

↓

Data Validation and Quality Checks

↓

SQL Fraud & AML Analysis

↓

SQL Views and Analytical Queries

↓

Power BI Data Model

↓

Interactive Fraud & AML Dashboards

↓

Business Insights and Recommendations

---

# Dataset Overview

The project uses three primary synthetic datasets:

1. Customers Dataset
2. Accounts Dataset
3. Transactions Dataset

The datasets were generated using Python rather than downloaded from an existing public dataset.

This approach was selected to create a customized banking analytics environment containing specific fraud, AML, risk, and investigation attributes required for the project.

The generated data is entirely synthetic and does not contain real customer, financial, or personally identifiable information.

---

# Why Synthetic Data Was Created

Public fraud datasets are useful for machine learning and statistical analysis; however, many publicly available datasets have limitations for end-to-end banking analytics projects.

For example, public datasets may:

- Contain anonymized column names.
- Lack customer-level information.
- Lack account information.
- Exclude AML-related attributes.
- Exclude PEP and sanctions indicators.
- Exclude transaction risk scores.
- Exclude investigation workflows.
- Exclude fraud loss information.
- Lack transaction monitoring indicators.

To address these limitations, synthetic banking datasets were generated specifically for this project.

The synthetic datasets allow the project to simulate relationships between:

- Customers
- Bank accounts
- Transactions
- Customer risk
- Fraud alerts
- AML alerts
- Transaction monitoring indicators
- Investigation cases

This provides a more complete environment for practicing SQL analysis, data modeling, and Power BI dashboard development.

---

# Dataset Size

| Dataset | Approximate Records | Description |
|---|---:|---|
| Customers | 10,000 | Synthetic banking customer profiles |
| Accounts | 10,000 | Customer bank account information |
| Transactions | 1,000,000 | Synthetic banking transaction records |

The large transaction dataset was generated to simulate a higher-volume banking analytics environment and provide sufficient data for SQL querying, aggregation, trend analysis, and dashboard development.

---

# Dataset Relationships

The datasets follow a relational structure.

Customers

Customer_ID

↓

Accounts

Customer_ID / Account_ID

↓

Transactions

Customer_ID / Account_ID

The primary relationships are:

- One customer is associated with an account.
- Each account belongs to a customer.
- Customers and accounts can be associated with multiple transactions.

These relationships allow customer information, account information, and transaction activity to be combined using SQL JOIN operations and Power BI relationships.

---

# 1. Customers Dataset

## Description

The `customers.csv` dataset contains synthetic demographic, financial, geographic, and customer risk information.

The purpose of this dataset is to support customer segmentation, customer risk analysis, KYC-related analysis, and fraud and AML investigations.

## Customer Dataset Columns

| Column | Description |
|---|---|
| Customer_ID | Unique identifier assigned to each customer |
| First_Name | Synthetic customer first name |
| Last_Name | Synthetic customer last name |
| Age | Customer age |
| Gender | Customer gender |
| Occupation | Synthetic customer occupation |
| Province | Canadian province associated with the customer |
| City | Customer city |
| Income | Estimated synthetic annual customer income |
| Credit_Score | Synthetic customer credit score |
| Risk_Level | Customer risk classification: Low, Medium, or High |
| PEP_Flag | Indicates whether the customer is synthetically classified as a Politically Exposed Person |
| Sanctions_Flag | Indicates a synthetic potential sanctions screening indicator |
| Customer_Segment | Customer classification such as Retail, Business, Premium, or Student |
| Account_Open_Date | Synthetic date when the customer relationship was established |

---

## Customer Risk Classification

Customers were assigned risk classifications based primarily on synthetic credit score ranges.

Example classifications include:

- Low Risk
- Medium Risk
- High Risk

Additional customer attributes, including PEP and sanctions indicators, were generated to support AML and financial crime analysis.

These classifications are simplified for portfolio and educational purposes and do not represent the complete customer risk assessment methodologies used by actual financial institutions.

---

# 2. Accounts Dataset

## Description

The `accounts.csv` dataset contains synthetic banking account information associated with customers.

The dataset provides the connection between customer profiles and banking transaction activity.

## Accounts Dataset Columns

| Column | Description |
|---|---|
| Account_ID | Unique identifier assigned to each bank account |
| Customer_ID | Customer associated with the account |
| Account_Type | Type of banking account |
| Balance | Synthetic account balance |
| Branch | Banking branch associated with the account |
| Status | Current synthetic account status |

---

## Account Types

The generated dataset contains account types such as:

- Savings
- Chequing
- Credit Card

Account information can be combined with customer and transaction data to analyze transaction activity across different account types and customer risk categories.

---

# 3. Transactions Dataset

## Description

The `transactions.csv` dataset is the primary dataset used for fraud and AML analysis.

It contains approximately one million synthetic banking transactions.

Each transaction contains information about:

- Customer
- Account
- Transaction amount
- Transaction date and time
- Merchant
- Payment method
- Geographic location
- Device information
- Transaction channel
- Customer risk
- Fraud indicators
- AML indicators
- Transaction monitoring alerts
- Investigation status
- Fraud losses

This dataset is designed to support SQL analysis and Power BI dashboard development.

---

# Transactions Dataset Columns

## Transaction Identification

| Column | Description |
|---|---|
| Transaction_ID | Unique identifier assigned to each transaction |
| Customer_ID | Customer associated with the transaction |
| Account_ID | Account associated with the transaction |

---

## Transaction Date and Time

| Column | Description |
|---|---|
| Transaction_Date | Date when the transaction occurred |
| Transaction_Time | Time when the transaction occurred |
| Transaction_Timestamp | Combined transaction date and time |
| Transaction_Hour | Hour during which the transaction occurred |

Transaction date and time information supports:

- Monthly trend analysis
- Daily transaction analysis
- Time-based fraud analysis
- Transaction velocity monitoring

---

## Transaction Information

| Column | Description |
|---|---|
| Amount | Monetary value of the transaction |
| Merchant | Synthetic merchant associated with the transaction |
| Merchant_Category | Business category associated with the merchant |
| Transaction_Type | Type of banking transaction |
| Payment_Method | Method used to complete the transaction |

Example transaction types include:

- Purchase
- Withdrawal
- Deposit
- Transfer
- Bill Payment

Example payment methods include:

- Credit Card
- Debit Card
- Wire Transfer
- E-Transfer
- Mobile Banking

---

## Geographic Information

| Column | Description |
|---|---|
| Country | Country where the synthetic transaction occurred |
| Province | Canadian province associated with the transaction |
| City | City associated with the transaction |
| Is_International | Indicates whether the transaction occurred outside Canada |

Geographic attributes support:

- Domestic versus international transaction analysis
- Fraud analysis by location
- AML alerts by country
- Geographic risk analysis

---

## Device and Technology Information

| Column | Description |
|---|---|
| IPAddress | Synthetic IP address associated with the transaction |
| Device_ID | Synthetic identifier for the device used |
| Device_Type | Type of device used to complete the transaction |
| Browser | Browser associated with the transaction |
| Operating_System | Operating system associated with the transaction |
| Channel | Banking channel used for the transaction |

Example banking channels include:

- ATM
- Mobile
- Online
- Branch
- POS

These attributes provide opportunities to analyze fraud patterns across devices and banking channels.

---

## Currency and International Activity

| Column | Description |
|---|---|
| Currency | Currency associated with the transaction |
| Is_International | Identifies domestic and international transactions |

International transaction information is used to support geographic fraud and AML analysis.

---

# Customer Risk & Compliance Indicators

| Column | Description |
|---|---|
| Customer_Risk_Level | Risk classification associated with the customer |
| PEP_Flag | Synthetic Politically Exposed Person indicator |
| Sanctions_Flag | Synthetic sanctions screening indicator |

These columns allow transactions to be analyzed in combination with customer-level compliance and risk indicators.

---

# Transaction Monitoring Indicators

| Column | Description |
|---|---|
| Velocity_Flag | Indicates potentially unusual transaction frequency |
| Structuring_Flag | Indicates potential transaction structuring activity |
| Risk_Score | Synthetic transaction risk score |
| Alert_Level | Transaction alert classification |
| Alert_Reason | Explanation of factors contributing to the transaction alert |

---

## Transaction Risk Score

A synthetic transaction risk scoring methodology was developed to classify transactions according to multiple risk indicators.

Example risk factors include:

- High transaction value
- International transaction activity
- Wire transfers
- Higher-risk customer classification
- PEP indicators
- Sanctions indicators
- Unusual transaction times
- Selected geographic indicators
- Transaction velocity
- Potential structuring activity

Transactions receive a synthetic risk score based on these indicators.

The risk score is then used to classify transactions into categories such as:

- Low
- Medium
- High
- Critical

The scoring methodology was developed for educational and portfolio purposes and does not represent a proprietary or production risk model used by an actual financial institution.

---

# Fraud Indicators

| Column | Description |
|---|---|
| Fraud_Alert | Indicates whether the transaction generated a synthetic fraud alert |
| Is_Fraud | Synthetic confirmed fraud classification |
| Fraud_Type | Category of fraudulent activity |
| Fraud_Loss_Amount | Estimated financial loss associated with confirmed fraudulent activity |
| Chargeback | Indicates whether the transaction resulted in a synthetic chargeback |

Example fraud types include:

- Card Not Present
- Identity Theft
- Account Takeover
- Phishing
- Friendly Fraud
- Synthetic Identity
- Merchant Fraud

---

# AML Indicators

| Column | Description |
|---|---|
| AML_Flag | Indicates whether the transaction generated a synthetic AML monitoring alert |
| PEP_Flag | Synthetic Politically Exposed Person indicator |
| Sanctions_Flag | Synthetic sanctions screening indicator |
| Structuring_Flag | Indicates potential transaction structuring activity |
| Velocity_Flag | Indicates potentially unusual transaction frequency |

These attributes support analysis of suspicious transaction activity and customer risk.

---

# Investigation Information

| Column | Description |
|---|---|
| Case_ID | Synthetic investigation case identifier |
| Investigation_Status | Current status of the synthetic investigation |
| Alert_Reason | Description of factors contributing to the alert |

Example investigation statuses include:

- Open
- Under Review
- Escalated
- Closed
- Not Required

Investigation information supports the development of operational dashboards for fraud and AML case monitoring.

---

# Important Data Disclaimer

All datasets used in this project are entirely synthetic and were generated using Python.

The project does not contain:

- Real customer information
- Real banking transactions
- Real account information
- Real fraud investigation information
- Real PEP information
- Real sanctions screening results

The fraud, AML, PEP, sanctions, structuring, velocity, risk score, and investigation indicators were created solely for educational, analytical, and portfolio demonstration purposes.

The rules and risk-scoring methodologies used in this project are simplified simulations and should not be interpreted as actual financial institution monitoring systems, regulatory requirements, or production fraud detection methodologies.

---

# Expected Project Outcomes

By completing this project, the goal is to develop an analytics solution capable of:

- Monitoring fraud performance.
- Measuring fraud rates and financial losses.
- Identifying fraud trends.
- Analyzing high-risk customers.
- Monitoring AML alerts.
- Analyzing transaction monitoring indicators.
- Prioritizing high-risk cases.
- Tracking investigation statuses.
- Providing management-level fraud and AML reporting.
- Supporting data-driven decision-making through interactive dashboards.

---

# Phase 1: Synthetic Dataset Generation
- Generated 10,000 synthetic customers.
- Generated 10,000 bank accounts.
- Generated 1,000,000 banking transactions.
- Exported all datasets as CSV files.

# Phase 2: PostgreSQL Database Setup
# Software Used
- PostgreSQL 18
- pgAdmin 4

# Database Created - banking_aml
Tables Created
- Customers
- Accounts
- Transactions

# Data Imported
| Table        |   Records |
| ------------ | --------: |
| Customers    |    10,000 |
| Accounts     |    10,000 |
| Transactions | 1,000,000 |

# Data Validation
**Total Transactions**

SELECT COUNT(*) AS "Total Transactions" FROM Transactions;

![PostgreSQL Tables](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-19%20at%2022.46.12.png)

Imported 1,000,000 transaction records into PostgreSQL 18 without data loss. 

**Transaction Summary**

SELECT
    COUNT(*) AS "Total Transactions",
    SUM("Amount") AS "Total Transaction Amount",
    AVG("Amount") AS "Average Transaction Amount",
    MIN("Amount") AS "Minimum Transaction",
    MAX("Amount") AS "Maximum Transaction"
FROM Transactions;

![Transaction Summary](https://raw.githubusercontent.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/main/Screenshot%202026-07-19%20at%2023.24.56.png)

The transaction dataset contains 1,000,000 synthetic banking transactions with a total transaction value exceeding $4.0 billion. The average transaction amount is approximately $4,002, providing a realistic, high-volume dataset for fraud analytics and transaction monitoring.

**Fraud Rate Analysis**

SELECT
    "Is_Fraud",
    COUNT(*) AS "Total Transactions",
    ROUND(
        COUNT(*) * 100.0 /
        (SELECT COUNT(*) FROM Transactions),
        2
    ) AS "Fraud Percentage"
FROM Transactions
GROUP BY "Is_Fraud"
ORDER BY "Total Transactions" DESC;

![Fraud Rate Analysis](https://raw.githubusercontent.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/main/Screenshot%202026-07-19%20at%2023.26.33.png)

Out of 1,000,000 transactions, 25,334 were classified as fraudulent, resulting in a fraud rate of approximately 2.53%. This dataset provides a balanced environment for fraud detection and investigative analytics.

**Fraud Type Distribution**

SELECT
    "Fraud_Type",
    COUNT(*) AS "Fraud Count",
    ROUND(SUM("Amount"),2) AS "Total Fraud Amount"
FROM Transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY "Fraud_Type"
ORDER BY "Fraud Count" DESC;

![Fraud Type Distribution](https://raw.githubusercontent.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/main/Screenshot%202026-07-20%20at%2000.17.41.png)

Fraud incidents are distributed across multiple fraud categories including Friendly Fraud, Synthetic Identity, Card Not Present, Identity Theft, Account Takeover, Phishing, and Merchant Fraud. Understanding these patterns helps prioritize fraud prevention strategies.

**Fraud by Customer Risk Level**

SELECT
    c."Risk_Level",
    COUNT(t."Transaction_ID") AS "Fraud Transactions",
    ROUND(SUM(t."Amount"),2) AS "Fraud Amount"
FROM Customers c
JOIN Transactions t
ON c."Customer_ID" = t."Customer_ID"
WHERE t."Is_Fraud"='Yes'
GROUP BY c."Risk_Level"
ORDER BY "Fraud Amount" DESC;

This query analyzes fraudulent transactions by customer risk level. It joins the Customers and Transactions tables using the Customer_ID field, filters only fraudulent transactions, and groups the results by customer risk category. The output shows the total number of fraudulent transactions and the total fraud amount associated with each risk level.
