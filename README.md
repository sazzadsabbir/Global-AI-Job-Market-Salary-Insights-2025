# AI Job Market Dashboard 2025 (Excel)
![Dashboard_AI](https://github.com/user-attachments/assets/0b8e7ed6-b30f-4d1b-8b90-7445562fe1a3)

## 📘Introduction 
An interactive Excel dashboard to analyze compensation, job availability, and industry demand across AI, ML, and Data roles. With slicers for Job Title, Employment Type, and Location, users can quickly explore market segments and extract insights. Primary KPIs : 
- Median Salary — Typical pay for the selected context (robust to outliers).
- Job Count — Number of postings under active filters.
- Top Industry — Most frequent hiring industry for the selection.

## ❓Problem Statement
AI professionals and hiring teams need a single, reliable view of market compensation and demand by role, country, and employment type. This dashboard centralizes that view, enabling salary benchmarking, geographic comparison, and industry demand discovery—all inside Excel, without macros.

## ⬇️Download file
My final dashboard file: [AI Job Dashboard.xlsx](https://github.com/sazzadsabbir/Global-AI-Job-Market-Salary-Insights-2025/blob/main/Dashboard/AI%20Job%20Dashboard.xlsx)

## Excel Skills Used
- 📊 Charts (Bar, Filled Map; conditional multi‑series highlighting)
- 🔢 Dynamic Arrays (FILTER, UNIQUE, SORT)
- 🧮 Multi‑criteria formulas using IF + MEDIAN
- ❎ Data Validation (clean dropdowns for slicers)
- 🧱 Helper & Calculation Tables powering KPIs and visuals

  
## 📂Dataset
This project uses the Global AI Job Market & Salary Trends 2025 dataset (~15k postings).
Fields used in the dashboard:

- 💰 Salary (USD)
- 🏢 Industry
- 📌 Job Title
- 📝 Employment Type
- 🌍 Company Location (Country)


## 🛠️Dashboard Build
### 🧹Data Preparation
- Remove Duplicates: Based on job_id.
- Handled Missing Value: Drooped missing value where salary(USD) = NULL / 0.
- Standardized Fields:
    - Changed the column's type to appropriate type.
    - Formatted the column's header.

### 🎛️Filters Used (Slicers)
- 📌 Job Title
- 📝 Employment Type
- 🌍 Location

#### Why these filters?
-	These three dimensions drive the most meaningful salary and demand segmentation for data roles without overwhelming users.
- They directly impact on the KPIs (Median Salary, Job Count, Top Industry) and visuals (bar charts and maps), creating a tight feedback loop.

#### Interactions with KPIs and charts:
- All KPIs and visuals recalculate based on current slicer selections.
- The Median Salary updates using dynamic, multi-criteria arrays.
- Job Count and Top Industry respond immediately to the active filter context.

<img width="1608" height="392" alt="Filter_Panel" src="https://github.com/user-attachments/assets/ba9b1522-de60-4770-89a3-6f0cc965669d" />


### 📊KPI Cards
- 💰 Median Salary — robust against outliers; better than average for skewed pay distributions.
- 🔢 Job Count — count of postings within current filter context.
- 🏭 Top Industry — the most frequent industry under the active filters.

#### Why Median vs Average?
- Salary data is typically right-skewed. Median reflects the central tendency more reliably.
<img width="1663" height="485" alt="KPIs" src="https://github.com/user-attachments/assets/0aac0272-8795-499f-94bf-d8d893e7a9de" />

### 📈Charts
### 📌Median Salarey by Job Title (Bar Chart)
<img width="546" height="365" alt="Median Salarey by Job Title" src="https://github.com/user-attachments/assets/7f3d5183-50a1-4a89-a620-7a1e34ebe3e2" />

- 🛠️**Excel Features**:
Horizontal bar, USD data labels, sorted descending; conditional highlight via two series (= vs <> + NA()).
- 🎨**Design Choice**:
Horizontal layout improves readability for long titles and quick comparison.
- 📉**Data Logic**:
Median from multi‑criteria arrays; helper columns for highlight series.
- 💡**Insights**:
Quickly shows highest‑paying roles and relative differences.

### 🌍Median Salary by Location (Map Chart)
![Map_Chart](https://github.com/user-attachments/assets/32c0df27-6e7c-4154-a7bb-ae2c7c449c42)

- 🛠️ **Excel Features**:
Filled map with color gradient; country helper table; standardized country names
- 🎨 **Design Choice**:
Immediate geographic context; darker shades for higher medians
- 📉 **Data Logic**:
 Plots median salary (or job count) at the country level.
- 💡 **Insights**:
Reveals salary hotspots and regions with stronger demand.

### 📝Median Salary by Employment Type (Bar Chart) 
<img width="522" height="380" alt="employment_type" src="https://github.com/user-attachments/assets/5b0d91e7-93e9-401b-b7a2-44b91817836d" /> 

- 🛠️Excel Features: Horizontal bar with dynamic ranges and USD labels; sorted descending, conditional highlight via two series (= vs <> + NA()).
- 🎨Design Choice: Clear side‑by‑side comparison across Full‑time, Part‑time, Contract, Freelance, etc.
- 📉Data Logic: Median via multi‑criteria arrays responding to slicers.
- 💡Insights: Highlights how compensation varies by employment type.


### 🧮Formulas & Calculation Tables
All formulas respect the slicer cells: Title (Job Title), Type (Employment Type), Country (Location).

### 💰Median Salary (KPI & charts):
- Logic: Multi‑criteria IF filters salaries; MEDIAN returns robust central tendency.
- `=MEDIAN(
      IF((
       AI[Job Title]=A2)*
        (AI[Employment Type]=Type)*
         (AI[Company Location]=Country),
           AI[Salary (USD) ]))`

<img width="312" height="457" alt="median_Table" src="https://github.com/user-attachments/assets/a6469e5a-8b7e-4002-9d9e-e27a7a4b851f" />


### 🔢Job Count (KPI)
- Logic: Counts matched postings (cleaning already removed 0/NULL salaries).
- `=COUNT(
     IF((
         AI[Job Title]=A2)*
           (AI[Employment Type]=Type)*
            (AI[Company Location]=Country),
             AI[Salary (USD) ]))`

<img width="286" height="462" alt="Count_Table" src="https://github.com/user-attachments/assets/1e3edda7-1f9e-41e4-a637-d7fc107574f0" />



### 🏢Top Industry (KPI) 
The first row of the sorted result is used for Top Industry.
- Median by Industry (helper table)
- `=MEDIAN(
      IF((AI[industry]=A2)*
      (AI[Job Title]=Title)*
      (AI[Employment Type]=Type)*
       (AI[Company Location]=Country),
       AI[Salary (USD) ]))`
  
- Rank industries by median (remove errors, sort desc)
- `=SORT(FILTER(A2:B16,ISNUMBER(B2:B16)),2,-1)`
  
<img width="567" height="395" alt="Industry_count" src="https://github.com/user-attachments/assets/8c2e485c-95f8-4b20-ab1f-bacf901ff02c" />


### ⚡Conditional Highlighting
To highlight the top value in a bar chart , the data is split into two series using IF + NA(). Excel plots real numbers but ignores NA(), so the top bar appears in a different color while the rest stay in the base series.
- Highlight Series (Top‑1):
- `=IF(D2=MAX($D$2:$D$16),D2,NA())`

- Base Series (Others):
- `=IF(D2<>MAX($D$2:$D$16),D2,NA())`

<img width="162" height="441" alt="Conditional_highlighting" src="https://github.com/user-attachments/assets/f24d56b1-b71e-4d3e-b83d-e05ce4c20cc1" />


### ❎Data Validation (Dropdowns)
Data validation was used to ensure clean and consistent filter inputs for Job Title, Employment Type, and Location.
How it was done:

- Created clean source lists using dynamic arrays:
  - =UNIQUE(AI[Job Title])
  - =SORT(UNIQUE(AI[Employment Type]))
  - =SORT(UNIQUE(AI[Company Location]))
  
- Applied Data → Data Validation → List and linked each dropdown to its corresponding dynamic list.
- Used FILTER where needed to remove blank or invalid entries.

#### Why it matters:
- Prevents typing errors
- Ensures formulas and slicers work correctly
- Keeps the dashboard consistent and error‑free

### 💡Insights Summary
- Engineering roles (AI/ML Engineer, Senior‑level positions) consistently show higher median salaries compared to Analyst and entry‑level roles.
- High‑income regions such as the United States and Western Europe offer significantly higher compensation than emerging markets.
- Full‑time and Contract roles generally pay more than Part‑time or Freelance positions.
- Top hiring industries vary by filter selection but commonly include Technology, Retail, Telecommunications, and Education, indicating strong demand across these sectors.

### 🔚Conclusion 
This dashboard provides a clear, interactive view of AI job salaries, demand, and industry trends across roles, countries, and employment types—all powered by dynamic Excel formulas and clean data modeling. It offers a simple way to compare compensation and understand market patterns, making it useful for both job seekers and anyone analyzing AI talent trends.







