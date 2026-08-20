# Banking Fraud & AML Analytics Platform

## Project Overview

Banks process large volumes of transactions that must be monitored for fraud, suspicious activity, customer risk, and potential AML concerns.

This project builds an end-to-end **Banking Fraud & AML Transaction Monitoring Analytics Platform** using **Python, PostgreSQL, SQL, and Metabase**.

The project uses synthetic customer, account, and transaction data to simulate a banking environment containing fraud indicators, AML flags, customer risk levels, transaction risk scores, PEP and sanctions indicators, velocity and structuring flags, fraud losses, and investigation statuses.

The workflow covers:

**Data Generation → PostgreSQL → SQL Analysis → Fraud & AML Rules → Metabase Dashboard → Business Insights**

---

## Business Problem

Fraud and AML teams need to quickly identify suspicious activity and understand where financial risk is concentrated.

This project addresses questions such as:

- What is the overall fraud rate and financial loss?
- Which customers, channels, payment methods, and regions have higher fraud exposure?
- Are high-risk customers associated with greater fraud activity?
- Which transactions show unusual velocity or high-value behavior?
- How are fraud patterns changing over time?
- Which fraud types occur most frequently?
- Which AML rules generate the most alerts?
- Where do multiple risk rules overlap?

---

## Project Objectives

- Generate realistic synthetic banking data using Python.
- Build relational customer, account, and transaction datasets.
- Store and validate 1M transactions in PostgreSQL.
- Analyze fraud and AML patterns using SQL.
- Apply JOINs, CTEs, CASE statements, subqueries, window functions, aggregations, and views.
- Develop rule-based fraud and AML detection logic.
- Analyze fraud losses across business dimensions.
- Build an interactive Metabase dashboard.
- Translate transaction data into actionable fraud and AML insights.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Python 3.x | Synthetic data generation |
| Pandas | Data manipulation |
| NumPy | Data generation |
| Faker | Synthetic customer data |
| Jupyter Notebook | Dataset generation |
| PostgreSQL 18 | Data storage and analysis |
| pgAdmin 4 | Database administration |
| SQL | Fraud, AML, and risk analysis |
| Metabase | BI dashboard and visualization |
| GitHub | Version control and documentation |

---

## Project Workflow

```text
Python Synthetic Data Generation
              ↓
CSV Dataset Export
              ↓
PostgreSQL Database
              ↓
Data Validation
              ↓
SQL Fraud & AML Analysis
              ↓
Rule-Based Fraud & AML Detection
              ↓
Metabase Dashboard
              ↓
Business Insights
```

---

# Dataset Overview

The project uses three synthetic datasets:

| Dataset | Records | Purpose |
|---|---:|---|
| Customers | 10,000 | Customer, geographic, financial, and risk information |
| Accounts | 10,000 | Account information and status |
| Transactions | 1,000,000 | Transaction, fraud, AML, risk, and monitoring data |

The datasets were generated specifically for this project rather than downloaded from a public dataset. This allowed the project to include customer-level, account-level, fraud, AML, investigation, and monitoring attributes in one relational environment.

All data is synthetic and contains no real customer or banking information.

---

## Dataset Relationships

```text
Customers
   │
   │ Customer_ID
   ↓
Accounts
   │
   │ Customer_ID / Account_ID
   ↓
Transactions
```

The relationships allow customer, account, and transaction information to be combined using SQL JOINs.

---

# Customers Dataset

`customers.csv` contains synthetic demographic, financial, geographic, and risk information.

| Column | Description |
|---|---|
| Customer_ID | Unique customer identifier |
| First_Name | Synthetic first name |
| Last_Name | Synthetic last name |
| Age | Customer age |
| Gender | Customer gender |
| Occupation | Synthetic occupation |
| Province | Canadian province |
| City | Customer city |
| Income | Synthetic annual income |
| Credit_Score | Synthetic credit score |
| Risk_Level | Low, Medium, or High |
| PEP_Flag | Synthetic PEP indicator |
| Sanctions_Flag | Synthetic sanctions indicator |
| Customer_Segment | Retail, Business, Premium, or Student |
| Account_Open_Date | Synthetic account opening date |

Customer risk classifications are simplified for portfolio purposes and do not represent production banking risk methodologies.

---

# Accounts Dataset

`accounts.csv` connects customer profiles with banking activity.

| Column | Description |
|---|---|
| Account_ID | Unique account identifier |
| Customer_ID | Associated customer |
| Account_Type | Savings, Chequing, or Credit Card |
| Balance | Synthetic account balance |
| Branch | Associated branch |
| Status | Account status |

---

# Transactions Dataset

`transactions.csv` contains approximately one million synthetic banking transactions and is the primary dataset for fraud and AML analysis.

### Transaction Information

| Column | Description |
|---|---|
| Transaction_ID | Unique transaction identifier |
| Customer_ID | Associated customer |
| Account_ID | Associated account |
| Transaction_Date | Transaction date |
| Transaction_Time | Transaction time |
| Transaction_Timestamp | Combined date and time |
| Transaction_Hour | Hour of transaction |
| Amount | Transaction value |
| Merchant | Synthetic merchant |
| Merchant_Category | Merchant category |
| Transaction_Type | Purchase, Withdrawal, Deposit, Transfer, or Bill Payment |
| Payment_Method | Credit Card, Debit Card, Wire Transfer, E-Transfer, or Mobile Banking |

### Geographic & Device Information

| Column | Description |
|---|---|
| Country | Transaction country |
| Province | Transaction province |
| City | Transaction city |
| Is_International | International transaction indicator |
| IPAddress | Synthetic IP address |
| Device_ID | Synthetic device identifier |
| Device_Type | Device category |
| Browser | Browser used |
| Operating_System | Operating system |
| Channel | ATM, Mobile, Online, Branch, or POS |

### Risk & Compliance Indicators

| Column | Description |
|---|---|
| Customer_Risk_Level | Customer risk classification |
| PEP_Flag | Synthetic PEP indicator |
| Sanctions_Flag | Synthetic sanctions indicator |
| Risk_Score | Synthetic transaction risk score |
| Alert_Level | Alert classification |
| Alert_Reason | Reason for alert |
| Velocity_Flag | Unusual transaction-frequency indicator |
| Structuring_Flag | Potential structuring indicator |

### Fraud Indicators

| Column | Description |
|---|---|
| Fraud_Alert | Synthetic fraud alert |
| Is_Fraud | Confirmed fraud classification |
| Fraud_Type | Fraud category |
| Fraud_Loss_Amount | Estimated fraud loss |
| Chargeback | Synthetic chargeback indicator |

Fraud types include Card Not Present, Identity Theft, Account Takeover, Phishing, Friendly Fraud, Synthetic Identity, and Merchant Fraud.

### AML & Investigation Indicators

| Column | Description |
|---|---|
| AML_Flag | Synthetic AML alert |
| Case_ID | Investigation case identifier |
| Investigation_Status | Open, Under Review, Escalated, Closed, or Not Required |

---

# PostgreSQL Database Setup

## Database

**Database:** `banking_aml`

**Tables:**

- `Customers`
- `Accounts`
- `Transactions`

### Data Validation

```sql
SELECT COUNT(*) AS "Total Transactions"
FROM Transactions;
```

![PostgreSQL Tables](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-19%20at%2022.46.12.png)

1,000,000 transaction records were imported into PostgreSQL.

### Transaction Summary

```sql
SELECT
    COUNT(*) AS "Total Transactions",
    SUM("Amount") AS "Total Transaction Amount",
    AVG("Amount") AS "Average Transaction Amount",
    MIN("Amount") AS "Minimum Transaction",
    MAX("Amount") AS "Maximum Transaction"
FROM Transactions;
```

![Transaction Summary](https://raw.githubusercontent.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/main/Screenshot%202026-07-19%20at%2023.24.56.png)

The dataset contains 1M transactions with total transaction value exceeding $4B and an average transaction amount of approximately $4,002.

---

# SQL Fraud Analysis

## Fraud Rate

```sql
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
```

![Fraud Rate Analysis](https://raw.githubusercontent.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/main/Screenshot%202026-07-19%20at%2023.26.33.png)

**Result:** 25,334 of 1,000,000 transactions were classified as fraudulent, producing a **2.53% fraud rate**.

---

## Fraud Type Distribution

```sql
SELECT
    "Fraud_Type",
    COUNT(*) AS "Fraud Count",
    ROUND(SUM("Amount"),2) AS "Total Fraud Amount"
FROM Transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY "Fraud_Type"
ORDER BY "Fraud Count" DESC;
```

![Fraud Type Distribution](https://raw.githubusercontent.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/main/Screenshot%202026-07-20%20at%2000.17.41.png)

This identifies the most common fraud categories and their associated transaction value.

---

## Fraud by Customer Risk Level

```sql
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
```

![Fraud by Customer Risk Level](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-20%20at%2000.19.37.png)

Compares fraud volume and financial exposure across High, Medium, and Low risk customers.

---

## Top 10 Customers by Fraud Amount

```sql
SELECT
    c."Customer_ID",
    c."First_Name",
    c."Last_Name",
    c."Risk_Level",
    COUNT(t."Transaction_ID") AS "Fraud Transactions",
    ROUND(SUM(t."Amount"),2) AS "Total Fraud Amount"
FROM Customers c
JOIN Transactions t
    ON c."Customer_ID" = t."Customer_ID"
WHERE t."Is_Fraud"='Yes'
GROUP BY
    c."Customer_ID",
    c."First_Name",
    c."Last_Name",
    c."Risk_Level"
ORDER BY "Total Fraud Amount" DESC
LIMIT 10;
```

![Top 10 Customers by Fraud Amount](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-20%20at%2000.24.49.png)

Identifies customers associated with the highest total fraudulent transaction amounts, supporting investigation prioritization.

---

## Fraud by Province

```sql
SELECT
    "Province",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"),2) AS "Total Fraud Amount"
FROM Transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY "Province"
ORDER BY "Total Fraud Amount" DESC;
```

![Fraud by Province](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-20%20at%2000.28.15.png)

Identifies geographic concentrations of fraudulent activity and financial loss.

---

## Fraud by Payment Method

```sql
SELECT
    "Payment_Method",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"), 2) AS "Total Fraud Amount"
FROM Transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY "Payment_Method"
ORDER BY "Total Fraud Amount" DESC;
```

![Fraud by Payment Method](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-20%20at%2000.32.26.png)

Shows which payment methods have the greatest fraud volume and financial impact.

---

## Fraud by Merchant Category

```sql
SELECT
    "Merchant_Category",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"), 2) AS "Total Fraud Amount"
FROM Transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY "Merchant_Category"
ORDER BY "Total Fraud Amount" DESC;
```

![Fraud by Merchant Category](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-20%20at%2000.35.46.png)

Highlights merchant categories associated with higher fraud losses.

---

## Monthly Fraud Trend

```sql
SELECT
    DATE_TRUNC('month', "Transaction_Date") AS "Month",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"), 2) AS "Total Fraud Amount"
FROM Transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY DATE_TRUNC('month', "Transaction_Date")
ORDER BY "Month";
```

![Monthly Fraud Trend](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-20%20at%2000.38.04.png)

Tracks fraud volume and financial impact over time.

---

## Time-of-Day Fraud Analysis

```sql
SELECT
    EXTRACT(HOUR FROM "Transaction_Timestamp") AS "Hour of Day",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"), 2) AS "Total Fraud Amount"
FROM transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY EXTRACT(HOUR FROM "Transaction_Timestamp")
ORDER BY "Hour of Day";
```

![Time-of-Day Fraud Analysis](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-25%20at%2018.47.54.png)

The dataset shows higher fraudulent activity during late-night and early-morning periods, providing a basis for time-based monitoring rules.

---

## Fraud by Day of Week

```sql
SELECT
    TRIM(TO_CHAR("Transaction_Date", 'Day')) AS "Day of Week",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"), 2) AS "Total Fraud Amount"
FROM transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY
    TRIM(TO_CHAR("Transaction_Date", 'Day')),
    EXTRACT(DOW FROM "Transaction_Date")
ORDER BY EXTRACT(DOW FROM "Transaction_Date");
```

![Fraud by Day of Week](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-25%20at%2020.11.16.png)

Analyzes recurring weekly fraud patterns.

---

## Fraud by Device Type

```sql
SELECT
    "Device_Type",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"), 2) AS "Total Fraud Amount",
    ROUND(AVG("Amount"), 2) AS "Average Fraud Amount"
FROM transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY "Device_Type"
ORDER BY "Fraud Transactions" DESC;
```

![Fraud by Device Type](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-25%20at%2020.14.56.png)

Compares fraud volume and financial impact across device types.

---

## Fraud by Channel

```sql
SELECT
    "Channel",
    COUNT(*) AS "Fraud Transactions",
    ROUND(SUM("Amount"), 2) AS "Total Fraud Amount",
    ROUND(AVG("Amount"), 2) AS "Average Fraud Amount"
FROM transactions
WHERE "Is_Fraud" = 'Yes'
GROUP BY "Channel"
ORDER BY "Fraud Transactions" DESC;
```

![Fraud by Channel](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-07-25%20at%2021.22.37.png)

Identifies banking channels with higher fraud activity and loss.

---

# Fraud & AML Rule Engine

The project extends descriptive analysis with rule-based transaction monitoring.

The rules are stored as independent indicators so they can be evaluated separately and combined later into broader risk assessments.

## High Value Transaction Rule

A `Rule_High_Value` column was added to the `transactions` table.

```sql
UPDATE transactions
SET "Rule_High_Value" =
CASE
    WHEN "Amount" >= 7000 THEN 'Yes'
    ELSE 'No'
END;
```

Transactions of **$7,000 or more** are flagged as high value.

### Validation

```sql
SELECT
    "Rule_High_Value",
    COUNT(*) AS Total
FROM transactions
GROUP BY "Rule_High_Value";
```

![High Value Rule Validation](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-07%20at%2018.07.01.png)

The rule flagged **125,046 transactions (12.50%)**.

---

## High Velocity Transaction Rule

`Rule_High_Velocity` identifies customers with unusually frequent transaction activity.

A rolling 24-hour window is used. A transaction is flagged when the customer has **5 or more transactions within the previous 24 hours**.

The rule is designed to identify unusual transaction frequency and does not independently classify a transaction as fraudulent.

### Validation

- Flagged transactions: **2,266**
- Non-flagged transactions: **997,734**
- Flag rate: **0.23%**

This makes the velocity rule more selective than the high-value rule.

---

## Transaction Frequency by Type

```sql
SELECT
    "Customer_ID",
    "Transaction_Type",
    COUNT(*) AS transaction_count
FROM transactions
GROUP BY
    "Customer_ID",
    "Transaction_Type"
ORDER BY
    "Customer_ID",
    "Transaction_Type";
```

![Transaction Frequency Analysis](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-07%20at%2023.44.53.png)

This establishes a behavioral baseline by customer and transaction type.

---

## Transaction Amount by Type

```sql
SELECT
    "Transaction_Type",
    COUNT(*) AS transaction_count,
    ROUND(AVG("Amount"), 2) AS average_amount,
    ROUND(MAX("Amount"), 2) AS maximum_amount
FROM transactions
GROUP BY "Transaction_Type"
ORDER BY maximum_amount DESC;
```

The transaction types show similar average values, approximately $4,000, with maximum values close to $8,000. Therefore, the high-value rule is retained as a general amount-based rule rather than creating separate thresholds by transaction type.

---

## AML Rule Validation

```sql
SELECT
    COUNT(*) FILTER (WHERE "Rule_High_Value" = 'Yes') AS high_value_yes,
    COUNT(*) FILTER (WHERE "Rule_High_Value" = 'No') AS high_value_no,
    COUNT(*) FILTER (WHERE "Rule_High_Velocity" = 'Yes') AS high_velocity_yes,
    COUNT(*) FILTER (WHERE "Rule_High_Velocity" = 'No') AS high_velocity_no
FROM transactions;
```

![AML Rule Validation](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-08%20at%2000.21.14.png)

The validation confirms the coverage of both rules:

- **High Value:** 125,046 flagged transactions, 12.50%
- **High Velocity:** 2,266 flagged transactions, 0.23%

---

## AML Rule Overlap Analysis

```sql
SELECT
    CASE
        WHEN "Rule_High_Value" = 'Yes'
         AND "Rule_High_Velocity" = 'Yes'
            THEN 'Both Rules'
        WHEN "Rule_High_Value" = 'Yes'
            THEN 'High Value Only'
        WHEN "Rule_High_Velocity" = 'Yes'
            THEN 'High Velocity Only'
        ELSE 'No Rule Triggered'
    END AS rule_result,
    COUNT(*) AS transaction_count
FROM transactions
GROUP BY rule_result
ORDER BY transaction_count DESC;
```

![AML Rule Overlap](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-08%20at%2000.56.16.png)

Transactions are classified into:

- **High Value Only**
- **High Velocity Only**
- **Both Rules**
- **No Rule Triggered**

The overlap analysis shows whether the rules identify similar transactions or provide complementary coverage.

---

# Metabase Dashboard

Metabase connects to the PostgreSQL `banking_aml` database and provides the interactive BI layer.

```text
CSV Data → PostgreSQL → Metabase → Fraud & AML Dashboard
```

The dashboard uses the `Transactions`, `Customers`, and `Accounts` tables. Metabase's query builder was used for filtering, grouping, aggregations, and calculated metrics.

## Dashboard Visuals

| Visual | Creation | Purpose |
|---|---|---|
| **Total Transactions** | Count of transactions | Overall transaction volume |
| **Fraudulent Transactions** | Count where `Is_Fraud = Yes` | Confirmed fraud volume |
| **Fraudulent Transaction Amount** | Sum of `Amount` for fraud | Fraud-related transaction value |
| **High-Risk Transactions** | Count of high-risk transactions | High-risk activity volume |
| **High-Risk Transaction Value** | Sum of `Amount` for high-risk transactions | Financial exposure |
| **Fraud Rate** | `CountIf(Is Fraud = "Yes") / Count() × 100` | Percentage of transactions that are fraudulent |
| **AML Flagged Transactions** | Count where `AML_Flag = Yes` | AML monitoring activity |
| **Total Fraud Loss** | Sum of `Fraud_Loss_Amount` for fraud | Financial impact |
| **High-Risk Transactions by Country** | Count grouped by country | Geographic risk concentration |
| **Account Status Distribution** | Count grouped by status | Active vs. dormant accounts |
| **Fraud Loss by Channel** | Fraud loss grouped by channel | Channel-level financial impact |
| **Transaction Volume by Risk Level** | Count grouped by customer risk | Risk-level comparison |
| **Fraudulent Transactions by Channel** | Fraud count grouped by channel | Channel fraud volume |
| **Transaction Distribution by Risk Level** | Risk-level count shown as percentage | Risk composition |
| **Fraud by Customer Segment** | Fraud count grouped by segment | Segment comparison |
| **Fraud Trend Over Time** | Weekly fraud count | Fraud trend monitoring |
| **Top Fraud Types** | Fraud count grouped and sorted by type | Most common fraud patterns |

### Visualization Types

- **Number cards** → headline KPIs
- **Bar charts** → category comparisons and rankings
- **Donut charts** → proportional distributions
- **Map** → geographic risk
- **Line/area chart** → fraud trends

![Metabase Dashboard](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-20%20at%2015.33.20.png)

![Metabase Dashboard](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-20%20at%2015.33.44.png)

![Metabase Dashboard](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-20%20at%2015.33.54.png)

![Metabase Dashboard](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-20%20at%2015.34.23.png)

![Metabase Dashboard](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-20%20at%2015.34.37.png)

![Metabase Dashboard](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-20%20at%2015.34.52.png)

![Metabase Dashboard](https://github.com/kaur-b76/Banking-Fraud-AML-Analytics-Platform/blob/main/Screenshot%202026-08-20%20at%2015.34.59.png)

The dashboard brings together transaction volume, fraud exposure, financial loss, customer risk, AML activity, geographic risk, channels, segments, fraud trends, and fraud types in one monitoring view.

---

# Key Project Outcomes

The project demonstrates an end-to-end analytics workflow covering:

- Synthetic banking data generation
- Relational data modeling
- PostgreSQL database management
- Data validation
- SQL fraud and AML analysis
- Customer and transaction risk analysis
- Rule-based transaction monitoring
- Fraud trend and loss analysis
- AML rule validation and overlap analysis
- Interactive Metabase dashboard development

The result is a portfolio-scale simulation of how transaction data can move from raw records to **fraud detection rules, risk analysis, and management-level monitoring**.

---

# Data Disclaimer

All datasets are synthetic and were generated using Python.

The project does not contain:

- Real customer information
- Real banking transactions
- Real account information
- Real investigation cases
- Real PEP information
- Real sanctions screening results

Fraud, AML, PEP, sanctions, structuring, velocity, risk scores, and investigation indicators are simulated for educational and portfolio purposes.

The rules and scoring methods are simplified examples and should not be interpreted as production banking controls, regulatory requirements, or real financial institution methodologies.
