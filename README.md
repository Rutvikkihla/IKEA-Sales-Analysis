# IKEA-Sales-Analysis :  Customer Analytics & RFM Segmentation

> *An end-to-end data analytics project using **SQL, Python, and Power BI***  
---

## 📌 Disclaimer
**IKEA Sales** is a fictional company name created for this educational portfolio project. It is not affiliated with, endorsed by, or representative of the real IKEA corporation. All metrics are derived from a public, anonymized transactional dataset.

---

## 💡 Project Overview
Imagine running an online gifting and home decor store. Do you know who your most valuable customers are? Do you know who is about to stop buying?

In this project, I simulated a real-world analytics engagement for **IKEA Gifting**, taking raw, messy transactional data through the entire analytics pipeline:
1. **Defined business goals** first via a Business Requirements Document.
2. **Cleaned and structured** the data in **SQL**.
3. **Calculated RFM metrics** and customer segments in **Python**.
4. **Built an interactive report** in **Power BI** for business leadership.

---

## 🔍 Business Problem & Questions Answered

### **The Problem:**
Leadership lacked a structured view of customer value, making customer retention efforts reactive rather than targeted.

### **Key Questions Answered:**
- **Who are our most valuable customers**, and how much revenue do they generate?
- **Which customers are inactive** and at risk of churning?
- **How do customer value and retention trend** over months, quarters, and years?
- **What actionable steps** should the business take for each customer segment?

---

## 📊 Key Insights & Findings

- 🏆 **The 80/20 Rule in Action:** **Champions** represent **~22%** of the customer base but generate **~68% of total revenue**.
- ⚠️ **High Churn Risk:** Total customer churn sits at **50.86%** (based on a 90-day inactivity threshold).
- 📈 **Seasonal Spikes:** Revenue shows clear peaks during **Q4**, aligning with holiday gifting trends.

---

## 🛠️ Tools & Tech Stack

| Tool | Purpose in Project |
| :--- | :--- |
| **SQL Server / SSMS** | Data import, cleaning, deduplication, and handling mixed date formats across 1M+ rows. |
| **Python (pandas)** | RFM calculations, scoring logic (1–5 scale), and 90-day churn flagging. |
| **Jupyter Notebook** | Interactive development environment for Python script development. |
| **Power BI Desktop** | 3-page interactive dashboard (Executive Summary, Business Overview, RFM Deep Dive). |
| **DAX** | Custom measures for total revenue, active customer counts, and average customer value. |

---

## 🚶‍♂️ Project Workflow

1. **Requirements Gathering:** Defined business questions, KPIs, and metrics beforehand.
2. **SQL Cleaning:** Corrected mixed date formats, removed **32,907 duplicate rows**, and organized raw tables.
3. **Python Segmentation:** Calculated **Recency, Frequency, and Monetary (RFM)** scores to assign 5,881 customers into 6 distinct segments (*Champions, Loyal, At Risk, New, Needs Attention, Lost*).
4. **Power BI Dashboard:** Merged data into a single unified star-schema table and built an interactive report.

---

## 💻 Sample Code Snippets

### 1️⃣ SQL: Handling Mixed Date Formats
```sql
SELECT
    Invoice, StockCode, Description, Quantity,
    COALESCE(
        TRY_CONVERT(datetime2, InvoiceDate, 120),
        TRY_CONVERT(datetime2, InvoiceDate, 105)
    ) AS InvoiceDate,
    TRY_CONVERT(decimal(10,2), Price) AS Price,
    Customer_ID, Country
INTO dbo.RetailCombined
FROM dbo.[Year 2009-2010];
```
### 2️⃣ Python : Score customers from 1 to 5 for Recency, Frequency, and Monetary values
```Python 
rfm['R_Score'] = pd.qcut(rfm['Recency'], 5, labels=[5, 4, 3, 2, 1]).astype(int)
rfm['F_Score'] = pd.qcut(rfm['Frequency'].rank(method='first'), 5, labels=[1, 2, 3, 4, 5]).astype(int)
rfm['M_Score'] = pd.qcut(rfm['Monetary'], 5, labels=[1, 2, 3, 4, 5]).astype(int)
