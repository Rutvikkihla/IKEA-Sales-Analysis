# IKEA-Sales-Analysis :  Customer Analytics & RFM Segmentation

> *An end-to-end data analytics project using **SQL, Python, and Power BI***  
---

## 📌 Overview & Business Problem
**IKEA Gifting** (a fictional UK-based e-commerce brand) lacked a structured view of customer value and churn, making retention efforts reactive. This project turns messy transactional data into an actionable Power BI dashboard to answer key questions:
* **Who are our most valuable customers?** 
* **Which customers are at risk of churning?**
* **What concrete actions should be taken for each segment?**

---

## 🛠️ Tech Stack & Workflow
* **SQL Server / SSMS:** Data cleaning, removing **32,907 duplicate rows**, and fixing mixed date formats across 1M+ rows.
* **Python (pandas):** Calculating Recency, Frequency, & Monetary (RFM) metrics, scoring customers (1–5 scale), and flagging 90-day churn.
* **Power BI:** Building an interactive 3-page dashboard (*Home, Business Overview, RFM Deep Dive*).

---

## 📊 Key Findings
* 🏆 **80/20 Rule:** **Champions** make up ~22% of customers but drive **~68% of total revenue**.
* ⚠️ **High Churn:** Total customer churn sits at **50.86%** (90-day inactivity threshold).
* 📈 **Seasonality:** Revenue spikes significantly in **Q4** due to holiday gifting trends.

---

## 💻 Code Snippets

<table>
<tr>
<th>SQL: Date Conversion</th>
<th>Python: RFM Scoring</th>
</tr>
<tr>
<td>

```sql
SELECT Invoice, StockCode, Quantity,
    COALESCE(
        TRY_CONVERT(datetime2, InvoiceDate, 120),
        TRY_CONVERT(datetime2, InvoiceDate, 105)
    ) AS InvoiceDate,
    TRY_CONVERT(decimal(10,2), Price) AS Price,
    Customer_ID, Country
INTO dbo.RetailCombined
FROM dbo.[Year 2009-2010];
Python


# Score Recency, Frequency, & Monetary (1-5)
rfm['R_Score'] = pd.qcut(rfm['Recency'], 5, 
                         labels=[5,4,3,2,1]).astype(int)
rfm['F_Score'] = pd.qcut(rfm['Frequency'].rank(method='first'), 5, 
                         labels=[1,2,3,4,5]).astype(int)
rfm['M_Score'] = pd.qcut(rfm['Monetary'], 5, 
                         labels=[1,2,3,4,5]).astype(int)
