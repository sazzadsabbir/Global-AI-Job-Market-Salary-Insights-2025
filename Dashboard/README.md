# AI Job Market & Salary Trend Dashboard ( Excel)
![Dashboard_AI](https://github.com/user-attachments/assets/0b8e7ed6-b30f-4d1b-8b90-7445562fe1a3)

## Introduction 
An interactive Excel dashboard to analyze compensation, job availability, and industry demand across AI, ML, and Data roles. With slicers for Job Title, Employment Type, and Location, users can quickly explore market segments and extract insights.

### Primary KPIs
- Median Salary — Typical pay for the selected context (robust to outliers).
- Job Count — Number of postings under active filters.
- Top Industry — Most frequent hiring industry for the selection.

## 🔎 Problem Statement
AI professionals and hiring teams need a single, reliable view of market compensation and demand by role, country, and employment type. This dashboard centralizes that view, enabling salary benchmarking, geographic comparison, and industry demand discovery—all inside Excel, without macros.

## 📥 Download
My final dashboard file: [AI Job Dashboard.xlsx](https://github.com/sazzadsabbir/Global-AI-Job-Market-Salary-Insights-2025/blob/main/Dashboard/AI%20Job%20Dashboard.xlsx)

## 🧰 Excel Skills Used
- 📊 Charts (Bar, Filled Map; conditional multi‑series highlighting)
- 🔢 Dynamic Arrays (FILTER, UNIQUE, SORT, RANK.EQ, MODE, etc.)
- 🧮 Multi‑criteria array formulas with IF + MEDIAN
- 🛡️ Data Validation (clean dropdowns for slicer inputs)
- 🧱 Helper/Calculation tables powering KPIs and visuals

  
## 🧾 Dataset
This project uses the Global AI Job Market & Salary Trends 2025 dataset (~15k postings).
Fields used in the dashboard:

- 💰 Salary (USD)
- 🏭 Industry
- 📌 Job Title
- 📝 Employment Type
- 🌍 Company Location (Country)


## 🗂️ Project Folder Structure
📦 Global-AI-Job-Market-Salary-Insights-2025
├─ 📁 Dashboard/
│  └─ AI Job Dashboard.xlsx
├─ 📁 Images/
│  ├─ dashboard_overview.png
│  ├─ filters_panel.png
│  ├─ kpis.png
│  ├─ chart_job_title.png
│  ├─ chart_location_map.png
│  ├─ chart_employment_type.png
│  ├─ sheet_location_calcs.png
│  ├─ sheet_industry_calcs.png
│  └─ data_validation_setup.png
└─ README.md

## 🧱 Dashboard Build
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
- 💰 Median Salary — robust against outliers; better than average for skewed pay distributions.
- 🔢 Job Count — count of postings within current filter context.
- 🏭 Top Industry — the most frequent industry under the active filters.

### Why Median vs Average?
- Salary data is typically right-skewed. Median reflects the central tendency more reliably.
<img width="1663" height="485" alt="KPIs" src="https://github.com/user-attachments/assets/0aac0272-8795-499f-94bf-d8d893e7a9de" />

### 🧮 Formulas & Calculation Tables
All formulas respect the slicer cells:
- Title (Job Title), Type (Employment Type), Country (Location)

### Median Salary (KPI & charts):
`=MEDIAN(
      IF((
       AI[Job Title]=A2)*
        (AI[Employment Type]=Type)*
         (AI[Company Location]=Country),
           AI[Salary (USD) ]))`

Logic: Multi‑criteria IF filters salaries; MEDIAN returns robust central tendency.

### Job Count (KPI)
`=COUNT(
     IF((
         AI[Job Title]=A2)*
           (AI[Employment Type]=Type)*
            (AI[Company Location]=Country),
             AI[Salary (USD) ]))`

Logic: Counts matched postings (cleaning already removed 0/NULL salaries).

### Top Industry (KPI) — Median‑then‑Sort Approach

- Median by Industry (helper table)
`=MEDIAN(
      IF((AI[industry]=A2)*
      (AI[Job Title]=Title)*
      (AI[Employment Type]=Type)*
       (AI[Company Location]=Country),
       AI[Salary (USD) ]))`
  
- Rank industries by median (remove errors, sort desc)
  `=SORT(FILTER(A2:B16,ISNUMBER(B2:B16)),2,-1)`

The first row of the sorted result is used for Top Industry.

image

-  Series Split for Conditional Highlighting (Charts)
To highlight Top‑1 (or Top‑N) in bar charts without VBA, two series are created:
Top‑1 Highlight
`=IF(D2=MAX($D$2:$D$16),D2,NA())`
- Base (Others)
`=IF(D2<>MAX($D$2:$D$16),D2,NA())`
Excel treats NA() as gaps, so only the intended series plots (perfect for different bar colors).

image

## ❎ 6) Data Validation (Dropdowns)
What & Why?
- Dropdowns ensure consistent inputs for Job Title, Employment Type, and Location.
- Prevents typos and keeps dynamic array formulas stable.

Source lists (clean)
=UNIQUE(AI[Job Title])

=SORT(UNIQUE(AI[Employment Type]))

=SORT(UNIQUE(AI[Company Location]))




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













