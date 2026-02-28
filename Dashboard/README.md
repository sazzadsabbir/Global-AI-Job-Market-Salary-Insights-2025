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

## Excel skills used:
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
### 📋Data Preparation
- Remove Duplicates: Based on job_id.
- Handled Missing Value: Drooped missing value where salary(USD) = NULL / 0.
- Standardized Fields:
    - Changed the column's type to appropriate type.
    - Formatted the column's header.

### 🎛️Filters Used (Slicers)
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

### 📊KPI Cards
### Primary KPIs: 
- 💰 Median Salary — robust against outliers; better than average for skewed pay distributions.
- 🔢 Job Count — count of postings within current filter context.
- 🏭 Top Industry — the most frequent industry under the active filters.

### Why Median vs Average?
- Salary data is typically right-skewed. Median reflects the central tendency more reliably.

### Formulas 
- Median Salarey (array formula):
`=MEDIAN(
      IF((
       AI[Job Title]=A2)*
        (AI[Employment Type]=Type)*
         (AI[Company Location]=Country),
           AI[Salary (USD) ]))`


- Job Count
`=COUNT(
     IF((
         AI[Job Title]=A2)*
           (AI[Employment Type]=Type)*
            (AI[Company Location]=Country),
             AI[Salary (USD) ]))`

- Top Industry
`=MEDIAN(
      IF((AI[industry]=A2)*
      (AI[Job Title]=Title)*
      (AI[Employment Type]=Type)*
       (AI[Company Location]=Country),
       AI[Salary (USD) ]))`

<img width="1663" height="485" alt="KPIs" src="https://github.com/user-attachments/assets/0aac0272-8795-499f-94bf-d8d893e7a9de" />

### 📈Charts
### Median Salarey by Job Title (Bar Chart)
<img width="546" height="365" alt="Median Salarey by Job Title" src="https://github.com/user-attachments/assets/7f3d5183-50a1-4a89-a620-7a1e34ebe3e2" />

- 🛠️**Excel Features**:
Used a horizontal bar chart with USD‑formatted labels, sorted in descending order for clarity.
- 🎨**Design Choice**:
Horizontal layout improves readability for long job titles and simplifies salary comparison.
- 📉**Data Logic**:
Median salary is calculated using dynamic multi‑criteria array formulas based on selected filters.
- 💡**Insights**:
Reveals the highest‑paying roles and makes cross‑title salary comparison straightforward.

###  Median Salary by Location (Map Chart)
![Map_Chart](https://github.com/user-attachments/assets/32c0df27-6e7c-4154-a7bb-ae2c7c449c42)

- 🛠️ **Excel Features**:
Used a filled map chart with color gradients, a country‑level helper table, and standardized country names for accurate mapping.
- 🎨 **Design Choice**:
A map chart gives instant global context and makes high‑vs‑low salary regions easy to compare.
- 📉 **Data Logic**:
Displays either median salary or job count by country, depending on the dashboard configuration.
- 💡 **Insights**:
Reveals geographic hotspots and shows where specific job titles and employment types are most in demand.

### Median Salary by Employment Type (Bar Chart) 
<img width="522" height="380" alt="employment_type" src="https://github.com/user-attachments/assets/5b0d91e7-93e9-401b-b7a2-44b91817836d" /> 

- 🛠️Excel Features: Used a horizontal bar chart linked to dynamic ranges with USD‑formatted labels.
- 🎨Design Choice: Horizontal layout ensures easy comparison between employment categories with clear readability.
- 📉Data Logic: Median salary is computed using multi‑criteria formulas that update automatically with slicer filters.
- 💡Insights: Clearly shows which employment types offer higher median salaries across the filtered dataset.













