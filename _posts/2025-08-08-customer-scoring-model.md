---
layout: post
title: "A Scoring Model for Customer Case Study Selection Using NPS and Engagement Metrics"
date: 2025-08-08
---

# A Scoring Model for Customer Case Study Selection Using NPS and Engagement Metrics

## 📌 Background
Case studies are powerful marketing assets—but selecting the right customer isn’t always straightforward. To remove subjectivity, I created a scoring model that ranks customers based on satisfaction, engagement, tenure, and support history.

---

## 🔧 Tech Stack
- **SQL** – for data extraction and score calculations  
- **Excel / Python** – for output formatting and visualization  
- **Survey + Usage Logs + CRM** – as data sources  
- **Scheduler (cron / task)** – for monthly refresh

---

## ⚙️ What I Built

### Step 1: Define Scoring Metrics
Each customer was evaluated on:
- NPS / LTR scores (from surveys)
- Product usage activity
- Ticket volume (weighted by severity)
- Time since go-live (tenure)

### Step 2: Normalize and Weight
Scaled values 0–100, applied weightings:
- 30%: NPS / LTR  
- 30%: Product engagement  
- 20%: Support ticket score  
- 20%: Tenure

### Step 3: Score Calculation
Calculated a composite score by applying weights to each normalized metric:
- Combined survey scores, engagement rates, support history, and tenure
- Higher scores indicated better candidates for marketing use
- Created a master table with breakdowns by customer

### Step 4: Schedule Monthly Refresh
- Pulled updated data from all relevant sources on the first of each month  
- Recalculated NPS, engagement, support, and tenure scores for each customer  
- Ranked customers based on final weighted scores  
- Exported the top-scoring customers into a shared file for Marketing and CS teams  

---

## 🧠 Results

| Metric                    | Value         |
|---------------------------|---------------|
| Shortlisted candidates    | 12 per cycle  |
| Monthly scoring time      | ~5 minutes    |
| Selection time saved      | ~80%          |

---

## ✨ Key Takeaways
- Scoring models add structure and repeatability to customer selection  
- Aligns teams with consistent data for outbound campaigns  
- Encourages high-ROI outreach based on engagement—not guesswork  

---

## 📁 What’s Next
- Add opt-in flag (PR consent) into scoring  
- Track historical score trends for retention signals  
- Build dashboard view for stakeholders  

---
