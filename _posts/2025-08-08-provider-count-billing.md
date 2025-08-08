# Creating a Standard Provider Count Workflow for Accurate Billing

## 📌 Background
Billing accuracy often hinges on the correct number of active providers. I created a reconciliation workflow to validate provider counts monthly, minimizing errors and ensuring that customers are billed appropriately.

---

## 🔧 Tech Stack
- **SQL (Snowflake)** – for pulling provider and activation data  
- **Excel** – for manual verification and reporting  
- **CRM / Intake Logs / Billing System** – as data sources

---

## ⚙️ What I Built

### Step 1: Identify Billing-Eligible Providers
- Pulled active provider records from intake logs  
- Filtered by:  
  - Live status  
  - Enabled products  
  - Valid departments

### Step 2: Compare with CRM Records
- Matched provider data from CRM with operational logs  
- Flagged mismatches in name, ID, or status  
- Verified go-live dates to exclude non-billable providers

### Step 3: Reconcile With Billing System
- Checked provider count billed vs. actual used  
- Flagged underbilling and overbilling scenarios  
- Created discrepancy column with reasons (missing from CRM, inactive, etc.)

### Step 4: Finalize and Deliver Monthly Report
- Exported clean provider count sheet  
- Shared with Finance and Customer Success teams  
- Stored monthly snapshots for trend tracking

---

## 🧠 Results

| Metric                   | Value         |
|--------------------------|---------------|
| Discrepancies resolved   | 20–30/month   |
| Time saved in invoice prep | ~3–5 hours  |
| Accuracy improvement     | +95% billing match rate |

---

## ✨ Key Takeaways
- Standardizing the provider count process reduces billing risk  
- Cross-verifying systems helps prevent financial leakage  
- Monthly reviews support scalable growth and accurate forecasting

---

## 📁 What’s Next
- Automate discrepancy detection using Python  
- Integrate approval workflow for disputed counts  
- Build live dashboard for provider count by account  

---
