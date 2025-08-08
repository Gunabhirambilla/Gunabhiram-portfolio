# How I Automated My Reporting Using Snowflake + Python + Word

## 📌 Background
In many data-driven environments, recurring reports often involve time-consuming steps: querying data, exporting it to Excel, generating charts, placing those charts in Word templates, converting to PDF, and emailing stakeholders. While the report content is critical, the manual process is tedious and error-prone.

So I built an **end-to-end automation pipeline** that transformed this workflow into a 5-minute job, using **Snowflake**, **Python**, **Excel**, and **Word automation**.

---

## 🔧 Tech Stack
- **Snowflake** – for SQL-based data extraction  
- **Python** – for orchestration and automation  
- **openpyxl** – to manipulate Excel charts dynamically  
- **python-docx** – to insert updated content and visuals into Word  
- **comtypes / docx2pdf** – to convert the final output to PDF  
- **Windows Task Scheduler / cron** – for scheduled automation

---

## ⚙️ What I Automated

### Step 1: Querying Data from Snowflake
Used `snowflake-connector-python` to extract:
- Monthly KPIs for different customer features
- Time-stamped usage metrics
- Top locations by performance

### Step 2: Updating Excel Charts
Using `openpyxl`, I:
- Replaced old data ranges with fresh outputs
- Updated chart titles (e.g., “Top 5 Locations – August 2025”)
- Maintained consistent formatting

### Step 3: Embedding Charts in Word
Using `python-docx`, I:
- Replaced placeholders with actual KPI summaries
- Inserted exported chart images
- Structured sections based on data length

### Step 4: Exporting to PDF
Used `docx2pdf` to convert the final document and name it like:
`ABCGroup_Metrics_Aug2025.pdf`

### Step 5: Scheduling
Set up a scheduled job to:
- Pull the latest data
- Generate customer reports
- Save PDFs to a shared drive or email automatically

---

## 🧠 Results

| Metric                  | Manual   | Automated |
|-------------------------|----------|-----------|
| Time per report         | 2 hrs    | 5 mins    |
| Accuracy                | Inconsistent | Reliable |
| Stakeholder Satisfaction| Moderate | High      |

---

## ✨ Key Takeaways
- Reporting automation improves speed, consistency, and credibility
- Python allows seamless orchestration of Excel + Word workflows
- Combining Snowflake’s data power with Office tools supports traditional and modern workflows

---

## 📁 What’s Next
- Adding error logging and exception handling
- One-click refresh via Streamlit interface
- Integrating cloud-based delivery (e.g., Google Drive or Slack bot)

---

