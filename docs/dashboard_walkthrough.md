## Purpose

This document explains the intended structure of the Power BI report and how each page answers a specific stakeholder question.

## Dashboard design principles

The report follows several guardrails:

- keep each page focused on one analytical lens
- do not mix total expenditure, per-head expenditure, and percentage-of-total casually
- use totals for executive reporting
- reserve subcategories for drill-down and diagnostics
- provide clear benchmark context when comparing boards


### Page 1 — Spending Pressures & Growth Drivers

**Question answered:** Which service areas are driving expenditure growth?

#### Core KPIs
- Total Expenditure
- YoY Change
- YoY Growth %
- Highest-growth category
- Largest category by spend

#### Visuals
- line chart: total expenditure over time
- clustered bar chart: current spend by category
- bar chart: YoY absolute change by category
- bar chart: YoY growth % by category
- watchlist table: categories with sustained growth

#### Interpretation guidance
This page should separate **large categories** from **fast-growing categories**. A service area can be systemically important even if it is not the fastest grower, and vice versa.



### Page 2 — Equity & Per-Head Resource Efficiency

**Question answered:** Are resources allocated proportionally across health boards?

#### Core KPIs
- Total Per Head
- Wales benchmark
- Difference vs Wales
- Spread between highest and lowest boards
- Consistency flag

#### Visuals
- ranking chart by per-head spend
- deviation-from-Wales chart
- category spread table
- min / median / max comparison by category
- optional small multiples by board

#### Interpretation guidance
This page should avoid implying that any deviation is automatically “good” or “bad”. Persistent deviation is a prompt for further discussion about need, geography, case mix, or service configuration.


### Page 3 — Allocation Shifts & Funding Mix

**Question answered:** How are funding priorities changing over time?

#### Core KPIs
- Current share of total spend
- Baseline share
- Percentage-point shift
- Biggest gainers
- Biggest losers

#### Visuals
- stacked area chart of category share over time
- bar chart of percentage-point gainers and losers
- table showing baseline, current share, and change
- scatter plot: current share vs share change

#### Interpretation guidance
Absolute spending often rises in many categories at once. Share-of-total reveals strategic reprioritisation more clearly because it shows relative winners and losers.

## Slicers and filters

global filters:

- Financial Year
- Health Board
- Service Area / Category
- Category Type
- Metric Type (if used only on supporting pages)

page-specific filters:

- **Page 1:** totals only
- **Page 2:** per-head metrics only
- **Page 3:** percentage-of-total only


## KPI definitions

### Total Expenditure
Sum of expenditure values for the selected context.

### Expenditure YoY Change
Current year expenditure minus previous-year expenditure.

### Expenditure YoY Growth %
YoY change divided by previous-year expenditure.

### Wales Per Head
Benchmark per-head value for the Wales aggregate.

### Difference vs Wales
Selected board per-head value minus Wales per-head value.

### Percentage Point Shift
Current category share minus baseline-year category share.
