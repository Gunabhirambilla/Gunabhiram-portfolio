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
Final SQL formula:

```sql
score = 
   0.3 * normalized_nps + 
   0.3 * engagement_score + 
   0.2 * (100 - support_score) + 
   0.2 * tenure_score
