Below is a GitHub-ready `README.md` you can paste into your repo and adjust (paths, screenshots, etc.) as needed. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

***

# Titanic Survival Analysis – Power BI Capstone Project

## 📌 Project Overview

This project explores the famous **Titanic** passenger dataset to understand how factors like passenger class, gender, age, family size, and embarkation port are related to survival outcomes. The focus is on **data cleaning, exploratory data analysis (EDA), and interactive visualization in Power BI**—no machine learning or prediction models are used. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

The final deliverable is a **Power BI dashboard** that allows users to interactively analyze survival patterns across different passenger segments.

***

## 🎯 Objectives

- Clean and preprocess the Titanic dataset for analysis. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)
- Perform descriptive exploratory data analysis to uncover key survival patterns. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)
- Build an interactive **Power BI dashboard** with KPIs, charts, and slicers to visualize insights. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)
- Document the full analytics workflow for reproducibility.

***

## 📂 Dataset

- **File:** `Titanic-Dataset.csv`  
- **Rows:** Passenger-level records  
- **Key columns:**  
  - `Survived` – 0 = did not survive, 1 = survived  
  - `Pclass` – Ticket class (1st, 2nd, 3rd)  
  - `Name`, `Sex`, `Age`  
  - `SibSp`, `Parch` – Family relations on board  
  - `Ticket`, `Fare`, `Cabin`, `Embarked` [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

### Data Quality Notes

- Missing values in **Age**, **Cabin**, and a few rows of **Embarked**.  
- `Cabin` is highly sparse and is not used for high-level analysis. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

***

## 🧹 Data Cleaning & Feature Engineering

All transformations are done using **Power Query** and **DAX** inside Power BI. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

### Cleaning Steps

- Set correct data types (numeric vs text).  
- Impute:
  - `Age` → median age (overall or by class/sex).  
  - `Embarked` → most frequent value (`S`).  
- Keep `Cabin` only for detailed views or drop it from core visuals due to many nulls. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

### New Columns

- **Age Group**

  ```DAX
  Age Group =
  VAR a = 'Titanic'[Age]
  RETURN
  IF (
      a < 18, "Child",
      IF ( a < 60, "Adult", "Senior" )
  )
  ```

- **Family Size**

  ```DAX
  Family Size = 'Titanic'[SibSp] + 'Titanic'[Parch] + 1
  ```

- **Sex Num** (optional numeric encoding)

  ```DAX
  Sex Num = IF ( 'Titanic'[Sex] = "female", 1, 0 )
  ```  
 [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

***

## 📊 Exploratory Data Analysis (EDA)

The analysis is purely descriptive and visual.

Key questions explored:

- How does **survival rate** vary by:
  - Passenger class (`Pclass`)  
  - Gender (`Sex`)  
  - Age and `Age Group`  
  - `Embarked` port  
  - `Family Size`  
- How are **fare levels** distributed across classes and survival outcome? [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

Example insights (you will see these in the dashboard):

- Higher survival rates for **1st class** and **female** passengers.  
- Children and smaller families often show better survival rates than some adult or very large-family groups. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

***

## 📈 Power BI Dashboard

The main report page is titled **“Titanic Survival Analysis”** and is organized as follows. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

### Measures (DAX)

```DAX
Total Passengers = COUNTROWS('Titanic')
Total Survived   = SUM('Titanic'[Survived])
Survival Rate    = DIVIDE([Total Survived], [Total Passengers])
```

These power the KPI cards and update dynamically with filters. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

### Layout

**Top Row – KPIs**

- Card: `Total Passengers`  
- Card: `Total Survived`  
- Card: `Survival Rate` (formatted as %)  

**Middle – Who Survived?**

- Stacked/clustered column: **Survival by Class** (`Pclass` vs `Survived`)  
- Stacked/clustered column: **Survival by Sex**  
- Column chart: **Survival by Age Group** (Child / Adult / Senior)  

**Bottom – Distributions**

- Age histogram (Age bins, colored by `Survived`)  
- Fare vs Class / Fare vs Survival (e.g., box plot or bar chart) [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

**Slicers**

- `Pclass`  
- `Sex`  
- `Age Group`  
- `Embarked`  
- `Family Size`  

Slicers let users filter the entire page and see updated metrics instantly. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

***

## 🚀 How to Run This Project

1. **Clone the repository**

   ```bash
   git clone https://github.com/<your-username>/titanic-powerbi-capstone.git
   cd titanic-powerbi-capstone
   ```

2. **Open the dataset**

   - Ensure `Titanic-Dataset.csv` is in the project root (or `data/` folder). [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

3. **Open Power BI Desktop**

   - Get Data → **Text/CSV** → select `Titanic-Dataset.csv`.  
   - Apply the cleaning and feature engineering steps described above.  
   - Recreate visuals and measures (or open the provided `.pbix` file if included). [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

4. **Publish (optional)**

   - Sign in to the Power BI Service and publish the report to share it online.

***

## 📁 Repository Structure (Suggested)

```text
.
├── data/
│   └── Titanic-Dataset.csv
├── reports/
│   └── Titanic_Survival_Analysis.pbix
├── docs/
│   └── Capstone_Report_Titanic.pdf
└── README.md
```


***

## 🧠 Skills Demonstrated

- Data cleaning & transformation (Power Query)  
- Feature engineering (Age groups, family size, encodings)  
- Descriptive statistics & EDA  
- DAX measures and calculated columns  
- Dashboard design and storytelling with Power BI [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

***

## 🔮 Future Improvements

- Add basic statistical tests (e.g., chi-square for survival vs class/sex).  
- Enrich dashboard with drill-through pages and custom tooltips.  
- Optionally extend the project with a simple ML model (e.g., logistic regression) in a separate branch, keeping this main branch purely descriptive. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88020393/c2002e68-c10e-4d9b-87bf-7e6e42ee588e/Titanic-Dataset.csv)

***

You can now customize the title, repo URL, screenshots section (add `![Dashboard](path)`), and your name/contact details before pushing this `README.md` to GitHub.
