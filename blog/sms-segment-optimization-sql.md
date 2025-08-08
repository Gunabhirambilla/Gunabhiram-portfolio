# Reducing SMS Message Segments to Save $$$ — A SQL Optimization Story

## 📌 Background

Many organizations use SMS to engage with users. However, most providers charge per **160-character segment**, and even a few extra characters can double the cost. After noticing high messaging expenses, I analyzed our outbound SMS data to reduce unnecessary segment usage.

The solution: **SQL-driven message audits** and **template optimizations**.

---

## 🔍 What I Set Out to Do

- Identify messages exceeding 160 characters
- Analyze patterns in how messages were constructed
- Propose changes to keep high-volume messages within 1 segment
- Quantify the potential cost savings

---

## 🧪 The SQL Audit Process

I worked with a table that tracked outbound SMS messages along with:
- Patient name
- Department or location
- Message body
- Character count (calculated)
- Date/time sent

### Sample Query:
```sql
SELECT
  department,
  COUNT(*) AS total_messages,
  SUM(CASE WHEN LENGTH(sms_body) > 160 THEN 1 ELSE 0 END) AS over_limit,
  ROUND(SUM(CASE WHEN LENGTH(sms_body) > 160 THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS percent_over_limit
FROM
  sms_message_log
GROUP BY
  department
ORDER BY
  percent_over_limit DESC;

Key Functions Used:
LENGTH() — to count characters

LEFT() — to truncate fields like names

CONCAT() — for reconstructing new templates

🔍 Key Insights
40%+ of messages in some departments exceeded 1 segment

Dynamic fields like full patient names inflated message length

Some templates included full URLs or verbose instructions

✅ Optimization Techniques
1. Message Template Redesign
Before:
Hi [Name], your telehealth appointment with Dr. Joseph Sanchez is on Friday, 8/8 at 9:00 AM. Please call us if you have any questions.

After:
Hi [Name], your appt is Fri 8/8 @ 9am. Call 123-456-7890 with questions.

2. Name Truncation
sql
Copy
Edit
LEFT(patient_first_name, 10)
3. Short Link Management
Moved long URLs to emails

Reserved SMS space for key info only

4. Monitoring Flag
Added a flag for segment overages in communication dashboards.

📈 Results
Metric	Before	After
Avg. % messages >1 segment	32%	9%
Est. monthly cost	~$120	~$40
Templates	Varied	Standardized

💡 Takeaways
Text optimization at scale = real cost savings

SQL string functions are underused but powerful

Centralizing message logic makes future analysis easier

Don't let personalization derail performance

🧭 What’s Next
Real-time dashboards for segment usage

Embed checks into template builders

Explore GPT summarization for auto-condensing messages
