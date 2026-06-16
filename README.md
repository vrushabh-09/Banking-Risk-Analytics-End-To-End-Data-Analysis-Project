# 🏦 Banking Risk Analytics — End-to-End Data Analytics Project

> A complete portfolio project covering data cleaning, exploratory data analysis (EDA), SQL database management, and interactive Power BI dashboarding — all on a real-world banking dataset.

---

## 📌 Project Overview

This project builds a **banking risk analytics pipeline** from raw data to executive-ready dashboards. The goal is to develop a foundational understanding of **risk analytics in banking and financial services** — specifically, how data can be used to minimize the financial risk of lending to customers.

Banks and financial institutions lend to a wide range of customers across income brackets. A subset of those customers default on their loans, resulting in direct financial loss. This project analyzes customer profiles to identify patterns and insights that support better lending decisions.

---

## 🎯 Business Problem

> *Develop a basic understanding of risk analytics in banking and financial services, and understand how data is used to minimize the risk of losing money while lending to customers.*

- High-income customers may be eligible for loans of ₹10–50 lakhs
- Medium-income customers may qualify for ₹2–5 lakhs
- Low-income customers may be eligible for ₹50k–₹2 lakhs
- Across all segments, a portion of customers **default** — and it is the data analyst's job to study this risk

---

## 📊 Dashboard Walkthrough

<details open>
<summary>🏠 Home Dashboard</summary>

<img width="100%" src="https://github.com/user-attachments/assets/79e38ee8-5bf7-40d9-9412-d04778220d60" />

</details>

<details>
<summary>📈 Loan Analysis</summary>

<img width="100%" src="https://github.com/user-attachments/assets/84c4af0f-41a1-4711-80e2-1fbf83900797" />

</details>

<details>
<summary>💰 Deposit Analysis</summary>

<img width="100%" src="https://github.com/user-attachments/assets/3b305c4b-e573-45f7-b433-e33fb3ac8e63" />

</details>

<details>
<summary>📋 Summary Dashboard</summary>

<img width="100%" src="https://github.com/user-attachments/assets/28c98f24-5415-4b52-9b2b-5efc8308d6b1" />

</details>

---

## 🗂️ Dataset

The dataset contains **3,000 customer records** across **25 columns**, including:

| Column | Description |
|---|---|
| `Age` | Customer age (range: 17–85) |
| `Gender ID` | 1 = Male, 2 = Female |
| `Nationality` | European, Asian, American, Australian, African |
| `Occupation` | Customer's occupation type |
| `Banking Relationship ID (BR ID)` | 1 = Retail, 2 = Institutional, 3 = Private Bank, 4 = Commercial Bank |
| `Investment Advisor ID (IIA ID)` | Assigned investment advisor |
| `Fee Structure` | Fee tier applied to the customer |
| `Estimated Income` | Approximate annual income |
| `Superannuation Savings` | Retirement savings balance |
| `Credit Cards (Amount)` | Number of credit cards held |
| `Credit Card Balance` | Outstanding credit card balance |
| `Bank Loans` | Total loan amount |
| `Bank Deposits` | Total deposit amount |
| `Checking Accounts` | Checking account balance |
| `Saving Accounts` | Savings account balance |
| `Foreign Currency Account` | Foreign currency holdings |
| `Business Lending` | Business loan amount |
| `Properties Owned` | Number of properties owned |
| `Risk Weighting` | Risk score assigned to the customer |

> **Note:** The dataset is provided as an Excel file, converted to CSV for analysis.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **Python** | Data cleaning, preparation, and EDA |
| **Pandas** | Data manipulation and transformation |
| **Matplotlib / Seaborn** | Data visualization |
| **MySQL** | Storing and querying the cleaned dataset |
| **MySQL Connector / PyMySQL** | Python–MySQL integration |
| **Power BI** | Interactive dashboard creation |
| **Canva** *(optional)* | Dashboard background design |
| **ChatGPT** *(optional)* | Insight generation assistance |

---

## 📁 Project Structure

```
banking-risk-analytics/
│
├── projec report
│
├── data
│
├── notebooks
│
├── powerbi/
│   └── banking_dashboard.pbix     # Power BI dashboard file 
│
└── README.md
```

---

## 🔄 Project Pipeline

```
Raw Excel Data
     │
     ▼
Convert to CSV
     │
     ▼
Load into MySQL (banking_case DB → customer table)
     │
     ▼
Connect Python (Jupyter) ↔ MySQL via connector
     │
     ▼
Data Cleaning & Preparation (Python / Pandas)
     │
     ▼
Exploratory Data Analysis (EDA)
 ├── Univariate Analysis
 ├── Bivariate Analysis
 ├── Numerical Distribution (Histograms)
 └── Correlation Heatmap
     │
     ▼
Connect MySQL → Power BI (as data source)
     │
     ▼
Dashboard (4–5 pages)
 ├── Home Page
 ├── Loan Analysis
 ├── Deposit Analysis
 ├── Summary
 └── Ask a Question (Q&A)
```

---

## 🧹 Data Cleaning & Preparation

Steps performed in Python:

- Load CSV with `pd.read_csv()`
- Check shape: **3,000 rows × 25 columns**
- Verify null values — dataset is complete (no missing values)
- Generate descriptive statistics via `df.describe()`
- **Feature Engineering:** Convert `Estimated Income` (continuous) into categorical `Income Band` using `pd.cut()`
  - `Low`: ₹0 – ₹1,00,000
  - `Mid`: ₹1,00,000 – ₹3,00,000
  - `High`: ₹3,00,000+
- Identify and separate **numerical** vs **categorical** columns for appropriate analysis

---

## 📊 Exploratory Data Analysis (EDA)

### Libraries Used
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### 1. Univariate Analysis — Categorical Columns
Analyzed distribution of unique categories across:
- BR ID, Gender ID, IIA ID, Amount of Credit Cards, Nationality, Occupation, Fee Structure, Properties Owned, Risk Weighting, Income Band

**Key Finding:** ~66% of customers hold only **one credit card**. Private Bank (BR ID = 3) has the highest customer count.

### 2. Bivariate Analysis
Added `hue` parameter to compare categorical distributions against `Gender ID` and `Nationality`.

**Key Finding:** European customers hold disproportionately more credit cards compared to other nationalities.

### 3. Univariate Analysis — Numerical Columns
Plotted histograms for:
- Estimated Income, Superannuation Savings, Credit Card Balance, Bank Loans, Bank Deposits, Checking Accounts, Saving Accounts, Foreign Currency Account, Business Lending

**Key Finding:** All numerical columns exhibit **right-skewed distributions**, indicating the presence of high-value outliers.

### 4. Correlation Heatmap
```python
correlation_matrix = df[numerical_cols].corr()
sns.heatmap(correlation_matrix, annot=True, cmap='crest', fmt='.2f')
plt.title('Correlation Matrix')
plt.show()
```

**Key Insights:**
- **Strong positive correlation** between `Bank Deposits`, `Checking Accounts`, `Saving Accounts`, and `Foreign Currency Account` — customers who maintain high balances in one account type tend to hold substantial funds across others as well
- `Credit Card Balance` shows **low correlation** with `Estimated Income` and `Bank Loans`, suggesting credit usage patterns vary independently of income level

---

## 🗄️ MySQL Integration

### Setup
```sql
CREATE DATABASE banking_case;
USE banking_case;
-- Import CSV via MySQL Workbench Data Import Wizard → table: customer
SHOW TABLES;
```

### Python → MySQL Connection
```python
import mysql.connector  # or pymysql

conn = mysql.connector.connect(
    host='localhost',
    user='your_username',
    password='your_password',
    database='banking_case'
)

df = pd.read_sql("SELECT * FROM customer", conn)
```

> **Note:** Google Colab cannot connect to a local MySQL instance. Use Jupyter Notebook, VS Code, or Spyder for local database connectivity.

---

## 📈 Power BI Dashboard

### Dashboard Structure (4–5 Pages)

| Page | Content |
|---|---|
| **Home** | Logo, KPI cards (Total Clients, Total Loans, Total Deposits, Total Fees), slicers for Gender & Date, navigation buttons |
| **Loan Analysis** | Total Bank Loans, Business Lending, Credit Card totals; bar chart of Bank Loan by BR ID; pie chart of Bank Loan by Income Range; slicers for Gender, BR ID, Investment Advisor |
| **Deposit Analysis** | Total Deposits, Bank Deposits, Savings Accounts, Checking Accounts; charts mirrored from Loan Analysis page |
| **Summary** | All key KPI cards in one view; icons per metric; quick comparison across all numerical attributes |
| **Ask a Question** | Power BI native Q&A visual for free-form data exploration |

### Data Source Connection
In Power BI Desktop:
`Get Data → MySQL Database → Server: localhost → Database: banking_case`

### Best Practices Applied
- All DAX measures created in a **dedicated measures table** (not scattered across queries)
- Background images designed in **Canva** for a polished look
- Navigation buttons implemented with **page action bookmarks**
- Color theme aligned with brand identity

---

## 💡 Key Insights

1. **Strongest positive correlations** occur among `Bank Deposits`, `Checking Accounts`, `Saving Accounts`, and `Foreign Currency Account` — indicating that customers who maintain high balances in one account type often hold substantial funds across other account types as well.

2. **Credit card usage** is relatively low — ~66% of customers hold only one credit card, and credit balance shows weak correlation with income, suggesting usage is behavior-driven rather than income-driven.

3. **Private Bank** (BR ID = 3) has the largest customer segment, followed by Retail, Institutional, and Commercial.

4. **Gender distribution** is near-equal (1,512 Male / 1,488 Female), limiting gender as a standalone differentiating factor across most metrics.

5. **All financial numerical variables** (loans, deposits, balances) exhibit right-skewed distributions, indicating a small number of very high-value customers drive aggregate totals.

6. **European customers** make up the largest nationality segment and show higher multi-card ownership rates.

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas matplotlib seaborn mysql-connector-python jupyter
```

### Steps
1. Clone this repository
2. Convert `banking_data.xlsx` to `banking_data.csv`
3. Import `banking_data.csv` into MySQL using the Data Import Wizard
4. Open `notebooks/banking_eda.ipynb` in Jupyter and run all cells
5. Open `powerbi/banking_dashboard.pbix` in Power BI Desktop
6. Update the MySQL connection credentials if needed

---

## 📚 Skills Demonstrated

- ✅ Python (Pandas, Matplotlib, Seaborn)
- ✅ Exploratory Data Analysis (Univariate, Bivariate, Correlation)
- ✅ Feature Engineering (Binning / Categorization)
- ✅ MySQL (Database creation, data import, SQL queries)
- ✅ Python–MySQL connectivity
- ✅ Power BI (Dashboard design, DAX measures, page navigation, slicers)
- ✅ Data storytelling and insight communication

---

## 🙌 Acknowledgements

Project by **Vrushabh Patil** 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/patilvrushabh/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/vrushabh-09)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:vrushabhpatil97711@gmail.com)

---

## 📬 Contact

Have questions or suggestions? Drop a comment or reach out via :
- **Email**: [vrushabhpatil97711@gmail.com](mailto:vrushabhpatil97711@gmail.com)
- **LinkedIn**: [Vrushabh Patil](https://www.linkedin.com/in/patilvrushabh/)
- **GitHub**: [vrushabh-09](https://github.com/vrushabh-09)
