# NHS Wales Financial Intelligence Dashboard v01

An end-to-end healthcare finance analytics case study combining Python-based data cleaning, statistical analysis, forecasting, and Power BI dashboard development to examine how NHS Wales spending changed over time, how funding priorities shifted, and where financial pressure points emerged.

> **Status:** v1 complete  
> **Author:** Edward Mbuthia  
> **Licence:** L001


## Executive summary

This project analyses NHS Wales expenditure from three complementary perspectives:

- **Total expenditure** by budget category and year
- **Expenditure per head** by budget category and year
- **Expenditure as a percentage of total spend** by budget category and year

The project was framed as a **Business Intelligence problem**, not just a charting exercise. The data was assessed for structural consistency, transformed to a common reporting grain, validated for hierarchy and reconciliation issues, then used to build a set of decision-focused dashboards around:

- **Spending pressures and growth drivers**
- **Equity and per-head resource efficiency**
- **Allocation shifts and funding mix**

The resulting portfolio project demonstrates how public-sector finance data can be turned into a validated analytical model and an interactive Power BI reporting product.


## Problem statement

NHS Wales operates under sustained financial pressure. Public finance data can show whether expenditure growth is broad-based or concentrated, whether spending is scaling proportionately with population, and whether budget allocation has shifted structurally since COVID-19.

This project addresses five stakeholder-style questions:

1. Which service areas are driving expenditure growth?
2. Are resources being allocated proportionally across health boards?
3. How is the balance of funding changing between service areas over time?
4. Which boards behave differently from the Wales benchmark?
5. What signals suggest medium-term financial sustainability risks?


## Project objectives

- Standardise and validate multiple NHS Wales financial datasets
- Prevent double counting by separating executive reporting totals from diagnostic subcategories
- Build a unified reporting layer at a consistent analytical grain
- Analyse long-run spending patterns before and after the COVID-19 shock
- Test whether observed changes are statistically meaningful
- Compare total expenditure, per-head spend, and share-of-total allocation
- Forecast selected expenditure series using time-series methods
- Deliver a Power BI dashboard suitable for stakeholder review


## Datasets

The core analytical inputs are:

| Dataset | Description | Primary analytical use |
|---|---|---|
| NHS Expenditure by Budget Category and Year | Total annual spend by category | Absolute growth, spending pressure, largest categories |
| NHS Expenditure Per Head by Budget Category and Year | Spend normalised by population | Cross-board comparability and equity analysis |
| NHS Expenditure as a Percentage of Total by Budget Category and Year | Budget share by category | Allocation shifts and strategic reprioritisation |
| Population estimates | Health-board context and per-head interpretation | Benchmarking and segmentation |
| Dashboard-ready unified fact table | Consolidated analytical layer with metric type | Power BI reporting |


### Current file inventory from the Drive materials


| Path | Type | Size | Last modified |
|---|---|---:|---|
| `/data/` | Folder | 1.67 MB | 2026-06-24 |
| `/Presentation/NHS Wales Financial Dashboard.pptx` | PowerPoint | 52.0 KB | 2026-06-24 |
| `/notebooks/` | Folder | 136 KB | 2026-06-24 |
| `NHS/.../NHS Wales financial dashboard.pbix` | Power BI file | 324 KB | 2026-06-24 |
| `README.md` | Markdown | 5.4 KB | 2026-06-24 |
| `a NHS  BI problem.docx` | Word document | 28.7 KB | 2026-06-24 |
| `nhs_expenditure_analysis.pdf` | PDF | 27.1 KB | 2026-06-24 |
| `nhs_expenditure_cheatsheet.pdf` | PDF | 39.2 KB | 2026-06-24 |



## Tools and technologies

### Analytics stack
- Python
- pandas
- NumPy
- matplotlib
- seaborn / plotly if retained
- SciPy
- statsmodels
- Prophet
- Jupyter Notebook

### BI stack
- Power BI Desktop
- DAX
- Power Query / model relationships

### Version control
- Git
- GitHub

## Repository structure

```text

nhs-wales-financial-intelligence-dashboard/
├── README.md
├── requirements.txt
├── LICENSE
├── data/
│   ├── raw/
│   ├── processed/
│   └── data_dictionary.md
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   ├── 03_statistical_testing.ipynb
│   ├── 04_forecasting.ipynb
│   └── 05_dashboard_preparation.ipynb
├── src/
│   ├── cleaning.py
│   ├── validation.py
│   ├── feature_engineering.py
│   ├── statistical_tests.py
│   ├── forecasting.py
│   └── dashboard_preparation.py
├── reports/
│   ├── figures/
│   ├── NHS_expenditure_analysis_summary.pdf
│   └── NHS_expenditure_cheatsheet.pdf
├── dashboard/
│   ├── NHS_Wales_Financial_Dashboard.pbix
│   ├── dashboard_notes.md
│   └── dashboard_preview.png
├── docs/
│   ├── methodology.md
│   ├── statistical_tests_explained.md
│   ├── dashboard_walkthrough.md
│   ├── project_limitations.md
│   ├── future_improvements.md
│   └── data_dictionary.md

```

## Methodology overview

The project followed a structured BI lifecycle rather than an ad hoc plotting workflow.

Define the reporting grain
A common reporting grain was defined as:
HealthBoard × Category Breakdown × FinancialYear × MetricType
This allowed the three core financial perspectives to be consolidated into one reporting layer.

### Build dimension tables

Three supporting dimensions were designed:
•	DimCategory
•	DimFinancialYear
•	DimHealthBoard

These dimensions reduced ambiguity, improved sorting, enabled benchmarking, and supported safe hierarchy handling.

### Consolidate the source datasets

The financial datasets were reshaped from wide to long form and merged into a unified fact table with fields such as:
•	HealthBoard
•	FinancialYear
•	Category Breakdown
•	MetricType
•	Value

### Validate before analyzing

Validation checks included:
•	category completeness
•	year completeness
•	record uniqueness at the reporting grain
•	missing values
•	negative values
•	percentage-range checks
•	outlier screening
•	hierarchy safety checks
•	reconciliation of related measures

### Analyze and model

The analysis then moved through:
1.	trend analysis
2.	pre/post-COVID comparison
3.	category-level comparison
4.	volatility checks
5.	correlation analysis
6.	Forecasting
7.	Dashboard dataset preparation

### Analytical assumptions

•	Executive reporting uses total categories only
•	Subcategories are retained for diagnostic analysis, not for headline totals
•	Financial year ordering is controlled explicitly via a sortable field such as FY_Order
•	For reproducibility in this repository, pre-COVID is defined as up to 2019-20 and post-COVID as 2020-21 onward

## Key findings

### Spending trends

•	NHS spending increased steadily over the long run
•	A prominent step change occurred in 2020-21
•	Spending remained elevated after the acute pandemic shock

## Budget allocation

•	Infectious Diseases was the most notable budget gainer during the COVID-era reallocation
•	Musculoskeletal System Problems showed a statistically significant decline in budget share in the documented analysis

### Per-head analysis

•	Per-head expenditure broadly tracked total expenditure, suggesting that growth in spend was not purely a population-size artefact

### BI insight

•	Absolute expenditure alone was not sufficient
•	Normalizing by population and examining allocation share were both necessary to understand equity and reprioritization

### Statistical approach

The repository explains and uses:
•	Welch’s t-test for pre/post comparison where equal variance assumptions may not hold
•	Levene’s test for variance comparison
•	Correlation analysis for category relationships
•	ADF test for stationarity checks in forecasting
•	Ljung-Box test for residual autocorrelation checks
•	Forecast comparison using SARIMA / SARIMAX and Prophet

### Forecasting approach

Two complementary forecasting families were used or prepared for use:
SARIMA / SARIMAX
Used for structured time-series modeling where trend and seasonality can be represented explicitly, and diagnostics can be checked carefully.
Prophet
Used as a flexible benchmark model, particularly helpful when trend change points or shock handling are important.
COVID handling
The pandemic period is treated as a structural shock rather than “business as usual”. Forecasting work should therefore be presented with explicit sensitivity commentary, and where possible the COVID period should be flagged, annotated, or tested separately rather than folded into the series without discussion.


### How to open the BI artefact
Open the file below in Power BI Desktop:
dashboard/NHS_Wales_Financial_Dashboard.pbix

## Limitations

•	Public, aggregated financial data cannot by itself explain outcomes, demand, or patient-level need
•	Pandemic-era shocks can distort simple trend extrapolation
•	Some categories include both totals and detailed breakdowns; careless aggregation can double count
•	Expenditure growth does not automatically imply inefficiency or poor targeting
•	A polished public repository requires a final pass on metadata, filenames, and export paths from the original Drive folder

## Future work

•	Add automated data ingestion where licensing allows
•	Integrate operational indicators such as admissions, waiting times, or workforce pressure
•	Publish a cleaned, dashboard-ready dataset
•	Add unit tests for validation logic
•	Add formal forecast backtesting and model comparison
•	Publish an optional Power BI Service dashboard if governance allows

### Author
•	GitHub: https://github.com/wondrwise?tab=repositories
•	LinkedIn: www.linkedin.com/in/edward-mbuthia-331813187








## Disclaimer

This project was developed independently for educational, research, and portfolio purposes.

The project is not affiliated with, endorsed by, or commissioned by NHS Wales, Digital Health and Care Wales (DHCW), the Welsh Government, or any NHS organisation.

All datasets used within this repository are publicly available open government data obtained from official Welsh Government and StatsWales sources.

The forecasts, dashboards, analyses, and recommendations presented are experimental and should not be interpreted as official NHS forecasts, financial plans, operational targets, or policy guidance.

Users should consult official NHS Wales publications and data releases for operational decision-making.


## Data Licensing

Unless otherwise stated, source datasets used in this project are available under the UK Open Government Licence (OGL) or other licences specified by the original data provider.

Original data ownership remains with the respective public sector organisations.

Users should review the licensing terms associated with each source dataset before reuse.


## Author

Edward Muigai Mbuthia
MSc Data Science & Analytics
Cardiff University

GitHub: https://github.com/wondrwise


Licensed under the MIT License.
