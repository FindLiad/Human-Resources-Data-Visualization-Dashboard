# Human Resources Data Visualization Dashboard

A leadership-facing dashboard to **track workforce health** using clean, comparable metrics across attrition, hiring funnel, diversity, and compensation.

- 🔗 **Live Dashboard (Tableau Public):**  
  [Live Dashboard](https://public.tableau.com/app/profile/liad.mizrachi/viz/HRProject_17554488176360/hr_dashboard?publish=yes)

- 📦 **Repository:**  
  [GitHub Repo](https://github.com/FindLiad/Human-Resources-Data-Visualization-Dashboard)

---

## Summary
A productized analytics workflow that lets HR leaders **monitor, diagnose, and act** on key people metrics.  
The dashboard visualizes **Attrition Trends, Hiring Funnel Conversion, Diversity Mix, and Compensation Bands** to enable **data-driven workforce planning**.

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## Table of Contents
- [Objective & Success Criteria](#objective--success-criteria)
- [What I Built & Why](#what-i-built--why)
- [End-to-End Walkthrough](#end-to-end-walkthrough)
  - [1) Data In](#1-data-in)
  - [2) Clean & Transform](#2-clean--transform)
  - [3) Guardrails (Data Quality Checks)](#3-guardrails-data-quality-checks)
  - [4) Derive Metrics](#4-derive-metrics)
  - [5) Visualize in Tableau](#5-visualize-in-tableau)
  - [6) Publish & Share](#6-publish--share)
- [Design Notes](#design-notes)
- [Results (Screenshots)](#results-screenshots)
- [Files & Folders](#files--folders)
- [How to Reproduce](#how-to-reproduce)
- [Limitations & Next Steps](#limitations--next-steps)
- [Credits](#credits)

---

## Objective & Success Criteria
**Problem:** Workforce planning is often reactive and anecdotal.  
**Objective:** Ship a repeatable workflow that surfaces **early warning signs** for attrition, bottlenecks in hiring, DEI representation, and comp band alignment.

**Success Criteria**
1. Unified view of workforce health across departments and levels.  
2. Explain *why* a trend is occurring (transparent inputs).  
3. Refresh quickly when new HR data arrives.  

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## What I Built & Why
- A **single CSV-based dataset** created with a **Python generator script**.  
- A **clean dataset** (`dataset.csv`) stored in the repo for transparency.  
- A **Tableau workbook** (`HR Project.twbx`) that surfaces actionable HR KPIs.  
- A **GitHub Pages site** (this page) that documents assumptions, steps, and outcomes.

**Why this approach?** It’s **fast, portable, and auditable**—teams can open the script, CSVs, and workbook to understand exactly how metrics are produced.

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## End-to-End Walkthrough

### 1) Data In
- **Raw input:** `assets/data/dataset.csv`  
  Columns include `employee_id`, `gender`, `department`, `job_title`, `education_level`, `salary`, `performance_rating`, `overtime`, etc.

### 2) Clean & Transform
- Generated via: `assets/scripts/generate_hr_dataset.py`  
- Includes logic for demographics, hiring/termination dates, job roles, salary, and attrition.

### 3) Guardrails (Data Quality Checks)
- **Row count** — ~8,950 employees generated.  
- **Column & type sanity** — salary numeric, job titles categorical, dates valid.  
- **Duplicates** — unique `employee_id` values.

### 4) Derive Metrics
- **Attrition Rate** = `# exits / avg headcount`.  
- **Time-to-Hire** = request open → accepted offer.  
- **Diversity Mix** = representation across gender/state/education.  
- **Comp Band Fit** = midpoint variance vs. performance rating.

### 5) Visualize in Tableau
- Workbook: `assets/visualizations/HR Project.twbx`  
- Data source: `assets/data/dataset.csv`  

**Dashboard Components**
- KPI tiles for Attrition, Avg Salary, Hiring Funnel metrics.  
- Breakdown by Department, Job Role, Gender.  
- Funnel view for recruitment stages.  
- Salary distribution plots.

### 6) Publish & Share
- Published to **Tableau Public**, linked at the top of this page.  
- Repo includes dataset, generator script, workbook, and documentation.

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## Design Notes
- **Why synthetic dataset?** Avoids PII, reproducible with generator script.  
- **Why these KPIs?** They balance *stability* (attrition), *growth* (hiring funnel), *inclusion* (diversity), and *fairness* (comp).  
- **Why Tableau?** Fast iteration and publishing for non-technical stakeholders.

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## Results (Screenshots)

<figure class="centered-figure">
  <a href="/Human-Resources-Data-Visualization-Dashboard/assets/images/mockup-dashboard.png" target="_blank" rel="noopener">
    <img src="/Human-Resources-Data-Visualization-Dashboard/assets/images/mockup-dashboard.png" alt="Mock Up">
  </a>
  <figcaption>Mock Up</figcaption>
</figure>

<figure class="centered-figure">
  <a href="/Human-Resources-Data-Visualization-Dashboard/assets/images/finished-dashboard.png" target="_blank" rel="noopener">
    <img src="/Human-Resources-Data-Visualization-Dashboard/assets/images/finished-dashboard.png" alt="Final Interface">
  </a>
  <figcaption>Final Interface</figcaption>
</figure>

<figure class="centered-figure">
  <a href="/Human-Resources-Data-Visualization-Dashboard/assets/images/tableu-container-design.png" target="_blank" rel="noopener">
    <img src="/Human-Resources-Data-Visualization-Dashboard/assets/images/tableu-container-design.png" alt="Tableau Container Design">
  </a>
  <figcaption>Tableau Container Design</figcaption>
</figure>

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## Files & Folders
- **Dataset (final):**  
  [/assets/data/dataset.csv](/Human-Resources-Data-Visualization-Dashboard/assets/data/dataset.csv)  
- **Dataset Generator Script:**  
  [/assets/scripts/generate_hr_dataset.py](/Human-Resources-Data-Visualization-Dashboard/assets/scripts/generate_hr_dataset.py)  
- **Tableau workbook:**  
  [/assets/visualizations/HR Project.twbx](/Human-Resources-Data-Visualization-Dashboard/assets/visualizations/HR%20Project.twbx)  
- **Documentation:**  
  [/assets/docs/Product_Requirements_Document.pdf](/Human-Resources-Data-Visualization-Dashboard/assets/docs/Product_Requirements_Document.pdf)  
- **Screenshots:**  
  - Mockup → `/assets/images/mockup-dashboard.png`  
  - Container Design → `/assets/images/tableu-container-design.png`
  - Final Dashboard → `/assets/images/finished-dashboard.png`  

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## How to Reproduce
1. **Clone** this repo.  
2. Run `assets/scripts/generate_hr_dataset.py` → creates `assets/data/dataset.csv`.  
3. Open `HR Project.twbx` in **Tableau** and point it at `dataset.csv`.  
4. Explore the dashboard; publish to Tableau Public if desired.  
5. To refresh later: rerun the script → re-open workbook (data updates automatically).

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## Limitations & Next Steps
- Synthetic dataset (not real HRIS).  
- Attrition not split into voluntary vs involuntary.  
- Hiring funnel simplified to static assumptions.  
- Next: connect to live HRIS export for scheduled refresh.  
- Add predictive attrition risk modeling.

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>

---

## Credits
Adapted from the open-source HR Analytics tutorial by [Data With Baraa](https://www.datawithbaraa.com/tableau/tableau-hr-project-thank-you/).  
This version re-implements the workflow with my own repo, structure, and documentation.  
© Liad Mizrachi.

<div align="right"><a href="#table-of-contents">↑ Back to top</a></div>
