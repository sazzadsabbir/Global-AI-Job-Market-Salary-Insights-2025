# AI Job Market & Salary Trend Dashboard
![Dashboard_AI](https://github.com/user-attachments/assets/0b8e7ed6-b30f-4d1b-8b90-7445562fe1a3)




## Introduction 
The AI Job Market & Salary Trend Dashboard is an interactive tool designed to analyze compensation, job availability, and industry demand across the fast‑growing field of artificial intelligence. Using filters for Job Title, Location, and Job Type, users can explore specific segments of the AI job market and uncover meaningful insights.
The dashboard highlights three key performance indicators:

- Median Salary – Represents the typical pay for the selected role and region.
- Job Count – Shows the number of available positions for the chosen filters.
- Top Industry – Identifies the leading sector hiring for the selected role.

Along with KPI cards, the dashboard includes visualizations of salary distributions, geographic hiring patterns, and job type breakdowns. Overall, this tool provides a clear, data‑driven view of how AI career opportunities and market demands are evolving, helping users benchmark salaries and make informed career decisions.



## Dashboard file 
My final dashboard file: [AI Job Dashboard.xlsx](https://github.com/sazzadsabbir/Global-AI-Job-Market-Salary-Insights-2025/blob/main/Dashboard/AI%20Job%20Dashboard.xlsx)

# Excel skills used:
- 📊 Charts
- 🔢 Formulas and Functions
- 🛡️ Data Validation
  
## AI Job Market Dataset: 
This project uses the Global AI Job Market & Salary Trends 2025 dataset, which contains over 15,000 AI, ML, and Data Science job postings collected from major global job platforms. The dataset includes detailed information on job titles, salaries, experience levels, skills, company attributes, and geographic patterns.
For this dashboard, the following fields were used:

- 💰 Salary (USD)
- 🏭 Industry
- 📌 Job Title
- 📝 Employment Type
- 🌍 Location

## Dashboard Build 
### Data Preparation
- Remove Duplicates: Based on job_id.
- Handled Missing Value: Drooped missing value where salary(USD) = NULL / 0.
- Standardized Fields:
    - Changed the column's type to appropriate type.
    - Formatted the column's header.

### Filters Used (Slicers)
- 📌 Job Title
- 📝 Employment Type
- 🌍 Location

### Why these filters?
-	These three dimensions drive the most meaningful salary and demand segmentation for data roles without overwhelming users.
- They directly impact on the KPIs (Median Salary, Job Count, Top Industry) and visuals (bar charts and maps), creating a tight feedback loop.

### Interactions with KPIs and charts:
- All KPIs and visuals recalculate based on current slicer selections.
- The Median Salary updates using dynamic, multi-criteria arrays.
- Job Count and Top Industry respond immediately to the active filter context.

<img width="1608" height="392" alt="Filter_Panel" src="https://github.com/user-attachments/assets/ba9b1522-de60-4770-89a3-6f0cc965669d" />











