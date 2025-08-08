# Designing a Patient Funnel Drop-Off Report Using Self-Scheduling Data

## 📌 Background
Understanding where patients drop off in the self-scheduling journey can help optimize user experience and improve appointment completion rates. I designed a reporting workflow to visualize drop-offs across each stage of the scheduling funnel.

---

## 🔧 Tech Stack
- **SQL (Snowflake)** – for stage-wise drop-off metrics  
- **Excel / Python** – for chart generation and reporting  
- **Self-Scheduling Logs** – as the data source  
- **Word + PDF** – for stakeholder-facing output

---

## ⚙️ What I Built

### Step 1: Define Funnel Stages
- Identified key milestones:  
  1. Widget Visit  
  2. Answered Qualification Questions  
  3. Selected Location  
  4. Selected Slot  
  5. Confirmed Appointment

### Step 2: Aggregate Data by Stage
- Counted unique patients at each step  
- Calculated conversion and drop-off % between each stage  
- Segmented by date range and location

### Step 3: Visualize Trends
- Created funnel bar charts using Excel  
- Highlighted top 5 departments by drop-off rate  
- Updated dynamic charts based on filters (month, location)

### Step 4: Deliver Monthly Funnel Report
- Populated Word template with charts and insights  
- Converted to PDF and shared with CX and Product teams  
- Tracked MoM changes in drop-off rates

---

## 🧠 Results

| Metric                  | Value         |
|-------------------------|---------------|
| Funnel conversion rate  | 54% avg       |
| Top drop-off stage      | Slot selection|
| Report delivery time    | 5 minutes     |

---

## ✨ Key Takeaways
- Funnel reporting helps target UX improvements where it matters  
- Visual drop-off trends are easier for non-technical teams to act on  
- Small optimizations in high-drop stages can yield major gains

---

## 📁 What’s Next
- A/B test new slot picker designs  
- Add device/browser breakdown to identify friction  
- Automate alerting when drop-offs spike unusually  

---
