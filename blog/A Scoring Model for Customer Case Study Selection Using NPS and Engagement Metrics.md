# A Scoring Model for Customer Case Study Selection Using NPS and Engagement Metrics

## 📌 Background
Choosing the right customers for public-facing case studies is a strategic decision. Instead of relying on anecdotal feedback or manual recommendations, I built a **data-driven scoring model** to consistently identify top-fit customers based on usage, satisfaction, and stability.

The result? A framework that helps Marketing, Customer Success, and Product teams focus on the right candidates — backed by data.

---

## 🎯 Objective
Build a system to:
- Surface the best-performing customers for case study outreach
- Score them based on satisfaction, adoption, and consistency
- Provide an updated list every month for stakeholder review

---

## 🧱 Scoring Criteria

The model scores customers across four dimensions:

| Category                    | Weight (%) | Data Source            |
|----------------------------|------------|------------------------|
| NPS / LTR Feedback         | 30%        | Survey Results         |
| Feature Engagement         | 30%        | Usage Logs (SQL)       |
| Support Ticket History     | 20%        | CRM / Ticketing System |
| Tenure (Go-Live Duration)  | 20%        | CRM / Internal Records |

---

## ⚙️ Implementation Steps

### 1. Data Collection & Normalization

Collected and normalized data into a 0–100 range for consistency:
- NPS and LTR scores from surveys
- Product engagement (e.g., completed actions, feature adoption)
- Count of support tickets and their levels (L1–L3)
- Days since go-live (tenure)

### 2. Scoring Formula

Used weighted scoring to calculate a final score:

```sql
score = 
   0.3 * normalized_nps + 
   0.3 * engagement_score + 
   0.2 * (100 - support_issue_score) + 
   0.2 * tenure_score
Note: Lower support_issue_score = fewer issues = higher adjusted score

### 3. Output Generation
Exported the top-ranked customers into a final table with scores broken down:

+-------------------+--------+-----+--------+---------+--------+
| Customer Name     | Score  | NPS | Usage  | Support | Tenure |
+-------------------+--------+-----+--------+---------+--------+
| HealthOne         | 92.3   | 95  | 88     | 90      | 95     |
| Metro Wellness    | 88.7   | 92  | 85     | 88      | 90     |
| Core Primary Care | 75.4   | 70  | 80     | 75      | 76     |
+-------------------+--------+-----+--------+---------+--------+


### 4. Monthly Refresh
Set up a process to refresh scores monthly by:

Pulling data from production systems

Recalculating scores

Highlighting customers with increasing or declining scores

Exporting to CSV / dashboard for marketing and CS teams

---

## Benefits
Objective & Repeatable — Removes guesswork

Cross-Team Alignment — Shared visibility for Marketing, CS, Product

Scalable — Easily applied to 100+ customers

Actionable — Generates a data-backed shortlist

