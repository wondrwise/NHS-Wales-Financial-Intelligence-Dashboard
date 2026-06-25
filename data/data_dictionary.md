# Data Dictionary


## Scope and note

This dictionary covers every dataset, table, and field that is explicitly evidenced in the available NHS project materials. Where the original Drive exposes assets but the raw spreadsheet headers are not fully visible in the retrieved materials, fields are marked as **inferred** and should be confirmed against the source files during repository clean-up.


## Dataset catalogue

| Dataset / table | Layer | Description |
|---|---|---|
| `NHS Expenditure by Budget Category and Year` | Raw source | Annual total expenditure by NHS budget category |
| `NHS Expenditure Per Head by Budget Category and Year` | Raw source | Annual expenditure per resident by budget category |
| `NHS Expenditure as a Percentage of Total by Budget Category and Year` | Raw source | Annual budget share by category |
| `DimCategory` | Model dimension | Category hierarchy and governance table |
| `DimFinancialYear` | Model dimension | Sortable financial-year reference |
| `DimHealthBoard` | Model dimension | Health-board context and population layer |
| `FactFinance` | Unified fact table | Consolidated long-format reporting layer |
| `dashboard_ready_dataset` | Processed output | Clean export used for Power BI or related reporting |


## Raw source datasets


### NHS Expenditure by Budget Category and Year

| Column | Type | Description | Example |
|---|---|---|---|
| `HealthBoard` *(inferred)* | text | NHS board or Wales aggregate | `Cardiff and Vale`, `Wales` |
| `BroadCategory` | text | High-level service grouping used for filtering totals | `Totals` |
| `CategoryBreakdown` *(inferred / likely explicit in source)* | text | Service category or subcategory label | `Mental Health Problems Total` |
| `FinancialYear_*` columns | numeric | Annual expenditure values in wide format before reshaping | `2009-10`, `2010-11` |
| `LHBPrimary` *(mentioned as dropped)* | text | Original health-board-related field not retained in final analysis | `Primary` |
| `LHBSecondary` *(mentioned as dropped)* | text | Original secondary board/breakdown field not retained | `Secondary` |


### NHS Expenditure Per Head by Budget Category and Year

| Column | Type | Description | Example |
|---|---|---|---|
| `HealthBoard` *(inferred)* | text | NHS board or Wales aggregate | `Hywel Dda` |
| `BroadCategory` | text | High-level grouping | `Totals` |
| `CategoryBreakdown` *(inferred)* | text | Service category | `Cancers & Tumours Total` |
| `FinancialYear_*` columns | numeric | Per-head values by financial year | `2019-20` |
| `ValueUnit` *(inferred)* | text | Unit context for per-head measure if stored | `£ per head` |


### NHS Expenditure as a Percentage of Total by Budget Category and Year

| Column | Type | Description | Example |
|---|---|---|---|
| `HealthBoard` *(inferred)* | text | NHS board or Wales aggregate | `Betsi Cadwaladr` |
| `BroadCategory` | text | High-level grouping | `Totals` |
| `CategoryBreakdown` *(inferred)* | text | Service category | `Infectious Diseases Total` |
| `FinancialYear_*` columns | numeric | Share-of-total values by year | `2020-21` |
| `ValueUnit` *(inferred)* | text | Unit context if stored | `% of total` |


### Population reference data

| Column | Type | Description | Example |
|---|---|---|---|
| `HealthBoard` | text | Board name | `Cwm Taf Morgannwg` |
| `Population` | numeric | Population count for benchmark context | `450000` |
| `PopulationBand` | text | Board-size grouping | `Medium` |


## Dimension tables


### DimCategory

| Column | Type | Description | Example |
|---|---|---|---|
| `CategoryBreakdown` | text | Exact reporting category label | `Mental Health Problems Total` |
| `ServiceArea` | text | Broader service family | `Mental Health` |
| `HasBreakdown` | boolean / text | Whether subcategories exist under the total | `TRUE` |
| `CategoryType` | text | Governance label for safe aggregation | `Total`, `Subcategory` |
| `NotesFlag` | text | Caveat marker for categories with structural notes | `Review for hierarchy caveat` |


### DimFinancialYear

| Column | Type | Description | Example |
|---|---|---|---|
| `FinancialYear` | text | Financial year label as displayed | `2020-21` |
| `FY_StartYear` | integer | Start year of the financial year | `2020` |
| `FY_EndYear` | integer | End year of the financial year | `2021` |
| `FY_StartDate` | date | Derived start date for ordering and date logic | `2020-04-01` |
| `FY_EndDate` | date | Derived end date | `2021-03-31` |
| `FY_Order` | integer | Sort key for chronological order | `12` |


### DimHealthBoard

| Column | Type | Description | Example |
|---|---|---|---|
| `HealthBoard` | text | Official board name | `Aneurin Bevan` |
| `RegionGroup` | text | Optional regional grouping for aggregation | `South East` |
| `BoardType` | text | E.g. board / Wales aggregate | `Health Board` |
| `Population` | numeric | Population estimate used for context | `600000` |
| `PopulationBand` | text | Size class for benchmarking | `Large` |


## Unified fact table


### FactFinance

| Column | Type | Description | Example |
|---|---|---|---|
| `HealthBoard` | text | Board or Wales aggregate | `Wales` |
| `FinancialYear` | text | Reporting year | `2021-22` |
| `CategoryBreakdown` | text | Service category | `Infectious Diseases Total` |
| `MetricType` | text | Which financial perspective this record belongs to | `Expenditure`, `PerHead`, `PctTotal` |
| `Value` | numeric | Value of the selected metric | `123456789.0` |


## Processed analytical fields

The repository should explicitly document the derived fields used in notebooks and dashboard preparation.

| Column | Type | Description | Example |
|---|---|---|---|
| `BaselineYear` | text | Selected reference year for allocation-shift comparisons | `2009-10` |
| `CurrentValue` | numeric | Current selected value | `12.4` |
| `PreviousYearValue` | numeric | Prior-year value | `11.1` |
| `YoYChange` | numeric | Current minus previous-year value | `1.3` |
| `YoYGrowthPct` | numeric | Year-on-year growth rate | `11.7` |
| `BaselinePctTotal` | numeric | Category share in the baseline year | `3.4` |
| `PercentagePointShift` | numeric | Current share minus baseline share | `1.2` |
| `DifferenceVsWales` | numeric | Board per-head metric minus Wales benchmark | `15.8` |
| `DifferenceVsWalesPct` | numeric | Relative deviation from Welsh benchmark | `4.6` |
| `PerHeadSpread` | numeric | Max minus min per-head value across boards | `72.1` |
| `EquityConsistencyFlag` | text / boolean | Indicates repeated above/below benchmark position | `Above 2 of last 3 years` |


## Forecasting dataset requirements

When creating a forecasting extract, the minimum recommended fields are:

| Column | Type | Description | Example |
|---|---|---|---|
| `FinancialYear` | text | Ordered annual period | `2022-23` |
| `ds` | date | Timestamp field for Prophet | `2023-03-31` |
| `y` | numeric | Target series value | `145000000` |
| `CategoryBreakdown` | text | Category forecasted | `Mental Health Problems Total` |
| `HealthBoard` | text | Board context if modelling by board | `Wales` |
| `IsCovidPeriod` | boolean | Flag for pandemic-era years | `TRUE` |
| `ModelName` | text | Forecast model identifier | `SARIMA`, `Prophet` |
| `ForecastValue` | numeric | Predicted future value | `150500000` |
| `LowerCI` | numeric | Lower confidence / uncertainty interval | `141200000` |
| `UpperCI` | numeric | Upper confidence / uncertainty interval | `160700000` |


## Power BI measure dictionary

Recommended measures to document in the repo:

| Measure | Description |
|---|---|
| `Total Expenditure` | Sum of expenditure values |
| `Total Per Head` | Sum or selected aggregation of per-head metric |
| `Total PctTotal` | Sum / selected aggregation of share-of-total values in appropriate context |
| `Expenditure YoY Change` | Difference from previous year |
| `Expenditure YoY Growth %` | Relative year-on-year growth |
| `Wales PerHead` | Benchmark per-head metric for Wales |
| `Difference vs Wales` | Selected board deviation from Wales benchmark |
| `Difference vs Wales %` | Relative deviation from Wales benchmark |
| `Baseline PctTotal` | Baseline year category share |
| `Percentage Point Shift` | Current share minus baseline share |


## Data-quality rules

The repo should preserve these rules in code and documentation:

- no duplicates at `HealthBoard + FinancialYear + CategoryBreakdown + MetricType`
- totals and subcategories must not be mixed in executive visuals
- percentage metrics must remain within valid ranges
- all boards must share the same year coverage before cross-board comparison
- all board/category combinations should be checked for completeness before plotting
