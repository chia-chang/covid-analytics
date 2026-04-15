# COVID Analytics Automation
Recreating the analytics system I built at IBM that cut COVID-19 reporting time by 80% (3–4 hours → 15 minutes) — while ensuring the right metrics reached the right decision-makers, every day.
Note: This is a recreation of my work at IBM using synthetically generated data. No proprietary IBM information included.

## Overview
During my time at IBM, I built an end-to-end analytics system that automated COVID-19 data reporting, from data cleaning and integration to metric calculation and report generation serving **100K+** daily users across **50+** public health organizations.
The technical challenge was real, but the harder problem was analytical: **figuring out which metrics actually mattered for decision-making**, and making sure those metrics were delivered reliably and on time.
This portfolio project recreates that system to demonstrate both sides of that work.

## Analytical Decisions
Before writing a single line of code, the more important work was deciding what to measure and why. These choices shaped everything downstream.
**Why positivity rate, not just case counts**
Raw case counts are misleading without context. A spike in cases means something very different if testing volume doubled that week. Tracking positivity rate (cases ÷ tests) separates a real outbreak signal from a testing artifact and keeps decision-makers from overreacting to noise.
**Why 7-day rolling averages, not daily numbers**
Daily case counts are volatile: weekend reporting lags, data submission delays, and batch corrections all create artificial spikes and drops. Using 7-day rolling averages smooths out this noise and reveals the actual trend , so responses are calibrated to what’s really happening, not a one-day artifact.
**Why connect hospitalizations to cases**
Cases and hospitalizations measure different things. Cases reflect current spread; hospitalizations reflect where the system will be under pressure in 1–2 weeks. Tracking both together and understanding the lag between them lets health leaders anticipate capacity needs before a crisis hits, rather than reacting after.
**Why surface week-over-week change alongside cumulative totals**
Cumulative totals show scale; week-over-week change shows momentum. A region with 10,000 total cases but declining weekly growth is a very different situation from one with 5,000 cases and accelerating growth. Both numbers together tell a more complete story.

What to include, how to calculate it and how to present it were the core analytical work. The automation made those choices scalable.

## The Problem
Some critical data challenges healthcare organizations faced during the pandemic:
- Hours of manual data aggregation from multiple sources daily
- Inconsistent metric calculations across teams led to conflicting reports
- Delayed reporting meant decisions were made on outdated information
- Manual processes couldn't scale with increasing reporting demands

## The Solution
Python-based analytics system that addresses the entire workflow:
- **Data Integration Pipeline**:
  Automates cleaning, validation, and standardization from multiple COVID data sources. Handles missing values, standardizes date formats, and generates derived metrics
- **Standardized metrics**
  Ensures consistency across all outputs:
  - 7-day rolling averages for smoothing daily volatility
  - Test positivity rates with WHO benchmark comparisons
  - Week-over-week change calculations for trend analysis
  - Cumulative totals for long-term tracking
- **Automated Reporting**:
  Generates publication-ready outputs:
  - Multi-sheet Excel report with daily, weekly, and summary
  - Visualizations for executive audiences

## Impact
- **80% reduction of reporting time**: From 2~3 hours to 10 minutes
- **Metrics consistency**: Eliminated discrepancies between teams
- **Same-day insights**: Enables real-time decision-making with current data
- **Scalable Solutions**: Handles increasing data volumes without additional changes

## The Process
### Notebooks
These two main notebooks cover a different stage of the analysis pipeline.

- [Data Cleaning and Integration](../notebooks/Data_Cleaning_and_Integration.ipynb)  
  Shows data loading, cleaning steps, and integration of sources
  - Generates a raw dataset (`covid_raw_data.csv`) for use in this file
  - Cleans column names, handles missing values, and standardizes date formats
  - Generates derived metrics such as 7-day averages, cumulative totals, and week-over-week changes
  - Exports the processed dataset (`covid_integrated_data.csv`) for downstream reporting
  Input: `covid_raw_data.csv` (synthetic raw data that is generated in this notebook)
  Output: `covid_integrated_data.csv` (cleaned and enhanced dataset)

- [Automated Reporting](../notebooks/Automated_Reporting.ipynb)  
  Demonstrates how the reporting process can be run automatically
  - Loads the processed dataset (`covid_integrated_data.csv`)
  - Calculates key metrics (averages, trends, cumulative totals)
  - Generates publication-ready visualizations
  - Produces a multi-sheet Excel report that includes daily, weekly, and summary data (`COVID_Report_YYYYMMDD.xlsx`)
  Input: `covid_integrated_data.csv`
  Output: `COVID_Report_YYYYMMDD.xlsx` (multi-sheet report) + charts

### Data
- [Raw Data](../data/raw/covid_raw_data.csv) (`covid_raw_data.csv`)   
  Synthetic daily time series mimicking COVID-19 pandemic data (2020-03-01 to 2024-01-31):  
  - `Date`: calendar date  
  - `Cases`: daily new confirmed cases  
  - `Tests`: daily diagnostic tests performed  
  - `Hospitalizations`: daily hospital admissions  
  - `Deaths`: daily reported deaths  
  - `Vaccinations`: daily vaccinations administered

- [Processed Data](../data/processed/covid_integrated_data.csv) (`covid_integrated_data.csv`)   
  Cleaned, merged, and enhanced the dataset with additional calculated features:  
  - 7-day rolling averages  
  - Positivity rate (cases/tests)  
  - Week-over-week changes  
  - Cumulative totals

 
## Outputs
- [Excel Report](../outputs/reports/COVID_Report_20251113.xlsx) (`COVID_Report_YYYYMMDD.xlsx`)  
  Summarizes daily and weekly key COVID-19 metrics and compares recent performance against prior weeks
  - Sheet 1: Summary (Key metrics at a glance)
  - Sheet 2: Daily Data (Last 90 Days of detailed metrics)
  - Sheet 3: Weekly Summary (Week-over-week comparisons)
  - Sheet 4: Key Metrics Comparison

- [Charts](../outputs/charts)
  - **1_daily_cases_trend.png**: Daily Cases with 7-Day Moving Average
  - **2_hospitalizations_trend.png**: Daily hospitalization with 7-Day Moving Average
  - **3_positivity_rate.png**: 7-day average COVID-19 test positivity rate with a 5% reference line recommended by the WHO, indicating concerning level of virus spread  

## Design Principles
- Analytical clarity first:
  Metric choices are documented and justified, not just implemented.
- System-level thinking:
  The solution addresses the entire workflow, not just isolated pieces. From data ingestion to executive reporting, each component works together to deliver end-to-end value.
- Reliability and maintainability:
  Keeping the code clean and robust, so it would be easy for anyone to understand and modify the logic without extensive documentation.
- Business-focused outputs
  Reports and visualizations are designed for stakeholder consumption, not just technical audiences. Clean formatting, clear messaging, and actionable insights.


## Technologies Used
- Python 3.x  
- Pandas & NumPy for data processing  
- Matplotlib & Seaborn for visualization  
- OpenPyXL / XlsxWriter for Excel report automation


👉 **[See this project in a product perspective](https://github.com/chia-chang/pm-portfolio/blob/main/covid-automation-product.md)** 


made with ✨ + 🌿 + 💛 by Chia Chang
