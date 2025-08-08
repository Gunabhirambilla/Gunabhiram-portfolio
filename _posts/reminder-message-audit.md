# Building a Lightweight Reminder Message Audit System

## 📌 Background
Text reminders are essential to patient engagement, but inconsistent templates and formatting often lead to inflated SMS costs. I created a lightweight auditing process to monitor reminder content, character usage, and SMS segment count.

---

## 🔧 Tech Stack
- **SQL (Snowflake)** – for extracting outbound SMS logs  
- **Excel / Python** – for length and segment analysis  
- **SMS Logs** – as the data source  
- **CRM** – for linking templates to accounts

---

## ⚙️ What I Built

### Step 1: Extract SMS Content and Metadata
- Pulled fields like:
  - Message body  
  - Character count  
  - Segment estimate  
  - Patient ID and timestamp  

### Step 2: Flag High-Segment Messages
- Calculated estimated segments per message  
- Highlighted messages >1 segment  
- Grouped by customer and template

### Step 3: Identify Optimization Opportunities
- Isolated messages with long openings (e.g., “Hi [Name], We are writing to remind...”)  
- Recommended template rewrites to reduce filler text  
- Suggested shortening URLs or using branded short links

### Step 4: Monthly Audit Summary
- Delivered Excel reports to Product and Ops teams  
- Included breakdown of savings potential by account  
- Logged high-volume repeat offenders for follow-up

---

## 🧠 Results

| Metric                      | Value        |
|-----------------------------|--------------|
| Multi-segment messages cut  | 55%          |
| Estimated savings / month   | $100–200     |
| Turnaround time per audit   | ~1 hour      |

---

## ✨ Key Takeaways
- Even basic auditing can identify real cost-saving opportunities  
- SMS optimization benefits both Ops and Customer Success teams  
- Message consistency supports better patient experience  

---

## 📁 What’s Next
- Automate audit script to run weekly  
- Add alerting for templates >1 segment  
- Build message simulator for live previews  

---
