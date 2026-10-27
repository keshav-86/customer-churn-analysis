## Customer Churn Analysis 📊 

An exploratory data analytics project using **Python, Pandas, SQLite, Matplotlib, and Seaborn** to analyze customer churn, subscription behavior, revenue metrics, and customer support indicators.

## 📌 Project Overview

Customer churn occurs when customers stop using a company's products or services. Analyzing churn helps businesses understand customer retention, identify potentially at-risk segments, and make informed decisions.

In this project, I used a SQLite database containing customer, subscription, and support information. I cleaned the data, engineered analytical features, combined the tables, calculated business KPIs, and visualized churn patterns using Python.

## 🎯 Project Objectives

- Calculate overall customer churn and retention rates.
- Compare churn rates across subscription plan types and states.
- Analyze average revenue per user (ARPU) and revenue associated with churned customers.
- Explore customer tenure and support-related indicators.
- Categorize customers into low, medium, and high churn-risk groups using churn scores.
- Visualize churn trends and relationships between selected variables.

## 🛠️ Tools & Technologies

- **Python** — analytical programming
- **Pandas** — data cleaning, transformation, grouping, and merging
- **NumPy** — feature engineering and conditional logic
- **SQLite & SQL** — database access and table inspection
- **Matplotlib** — churn trend and category-based charts
- **Seaborn** — correlation heatmap
- **Jupyter Notebook** — interactive analysis

## 📂 Database Structure

The SQLite database, `customer_churn.db`, contains three tables:

| Table | Purpose |
|---|---|
| `db_customer` | Customer details, country, state, gender, and date of birth |
| `db_subscription` | Subscription dates, plan and contract types, cancellation details, monthly charges, CLTV, and churn score |
| `db_support` | Complaint dates, escalations, customer satisfaction scores, and support comments |

The tables were loaded into Pandas DataFrames using Python's `sqlite3` module and `pd.read_sql_query()`.

## 🔄 Project Workflow

### 1. Database Exploration

- Connected to the SQLite database using `sqlite3`.
- Retrieved table names from SQLite's metadata.
- Inspected table schemas and column names.
- Loaded database tables into Pandas DataFrames.

### 2. Data Cleaning

**Customer data**
- Renamed `name` to `customer_name`.
- Removed the `interests` and `pincode` columns.
- Converted `dob` to a datetime data type.
- Standardized gender values such as `Men` and `Women` to `Male` and `Female`.
- Filled missing country values using the state-to-country mapping.

**Subscription data**
- Converted subscription start, renewal, and cancellation dates to datetime format.

**Support data**
- Removed unused columns.
- Converted complaint dates to datetime format.
- Created a complaint-count feature and retained the latest support record per customer.

### 3. Feature Engineering and Data Integration

- Created `churn_flag`: 1 when a cancellation date exists, otherwise 0.
- Merged customer, subscription, and support DataFrames using `customerid`.
- Calculated customer tenure in days.
- Created churn-risk categories from `churn_score`:
  - Low: score below 50
  - Medium: score from 50 to below 70
  - High: score of 70 or above
- Exported the merged dataset to `exported_data.csv`.

### 4. Exploratory Data Analysis (EDA)

Calculated the following business metrics:

- Overall churn rate and retention rate
- Churn rate by plan type
- Churn rate by state
- Customer counts and aggregated monthly charges by state and plan
- Average Revenue Per User (ARPU)
- Average customer tenure
- Monthly charges associated with churned customers, labelled revenue at risk
- Escalation rate
- Average complaint count per customer
- Correlation between escalations and churn

### 5. Data Visualization

Created visualizations using Matplotlib and Seaborn:

- Monthly churn trend
- Churn rate by plan type
- Churn rate by state
- Correlation heatmap for selected encoded variables
- Pivot table summarizing churn by plan type

The notebook also includes basic SQL table-creation and data-insertion practice using SQLite.

## 📈 Key Findings

The following results are from the notebook's saved analysis outputs.

| KPI | Result |
|---|---:|
| Customers in merged dataset | 21 |
| Customer churn rate | 28.57% |
| Customer retention rate | 71.43% |
| Average monthly charges per customer (ARPU) | 18.85 |
| Average customer tenure | 1,569 days |
| Monthly charges associated with churned customers | 73.94 |
| Escalation rate | 19.05% |
| Average complaint count per customer | 0.43 |
| Correlation between escalations and churn | 0.77 |

### Churn by Plan Type

| Plan Type | Churn Rate |
|---|---:|
| Basic | 60.00% |
| Standard | 22.22% |
| Premium | 14.29% |

**Observations**

- The Basic plan had the highest observed churn rate at 60%.
- The Premium plan had the lowest observed churn rate at 14.29%.
- The calculated escalation–churn correlation was positive at 0.77.
- These findings are exploratory and should be validated using a larger dataset before making business-wide decisions.

**Metric note:** The 73.94 figure represents the sum of monthly charges for churned customers in the current dataset. It is not a calculated lifetime revenue loss. The notebook labels it as revenue at risk; the actual financial impact depends on the business definition and time horizon.

## 💼 Potential Business Recommendations

Based on the observed patterns, the following actions could be investigated:

1. **Investigate Basic plan churn:** Examine cancellation reasons, pricing, and customer experience for Basic subscribers.
2. **Review escalated support cases:** Explore whether customers with escalations are more likely to churn.
3. **Monitor churn-risk categories:** Use the existing churn scores to prioritize further investigation of high-risk customers.
4. **Improve support analysis:** Collect more complete complaint histories to better understand the relationship between support experience and churn.
5. **Validate findings:** Repeat the analysis on a larger dataset and test whether the observed patterns persist.

These are potential actions for further investigation, not proven causal conclusions.

## 🚀 How to Run the Project

### Prerequisites

Install Python and Jupyter Notebook.

### 1. Clone the repository

```bash
git clone https://github.com/keshav-86/customer-churn-analysis.git
cd customer-churn-analysis
```

### 2. Install the required libraries

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

SQLite support is available through Python's standard-library `sqlite3` module.

### 3. Open Jupyter Notebook

```bash
jupyter notebook
```

Open `DA_Project.ipynb` and run the cells in order.

**Important:** Update the database connection path in the notebook to match the location of `customer_churn.db` on your computer. The notebook currently contains a local Windows file path in its initial connection cell.

## 📁 Project Files

- `DA_Project.ipynb` — data cleaning, feature engineering, KPI calculations, visualizations, and SQL practice.
- `customer_churn.db` — SQLite database used for the analysis.
- `README.md` — project documentation.

## ⚠️ Limitations

- The current merged dataset contains only 21 customer records, so the findings are illustrative rather than broadly generalizable.
- The support table contains fewer records than the customer and subscription tables.
- The escalation–churn correlation indicates an association in this sample; it does not establish causation.
- The notebook's tenure calculation uses the current date for customers without a cancellation date, so results can change when the notebook is rerun.

## 👨‍💻 Author

**Keshav Verma**

GitHub: [keshav-86](https://github.com/keshav-86)

---

*This project demonstrates practical data analytics skills in database exploration, data cleaning, feature engineering, exploratory analysis, KPI calculation, and data visualization.*
