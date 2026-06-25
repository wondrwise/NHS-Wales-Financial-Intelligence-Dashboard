## Data limitations

### Aggregated public finance data
The analysis is based on aggregated expenditure data rather than patient-level operational records. This means the project can describe spending patterns, but it cannot directly explain patient outcomes, case complexity, or causal effects.

### Category hierarchy complexity
Some service areas contain both totals and detailed subcategories. If totals and subcategories are combined indiscriminately, the result can double count expenditure. The repository deals with this by treating totals as the executive reporting layer and subcategories as diagnostic only.

### Potential metadata inconsistency
The original project materials were stored across folders, versions, and exported outputs. A cleaned repository improves clarity, but some original filenames, paths, and file metadata need final confirmation before publication.

### Financial-year granularity
The series is annual by financial year. That is good for long-run strategy and budgeting, but it reduces sensitivity to within-year changes and limits the number of observations available for forecasting.


## Analytical limitations

### Pre/post-COVID comparisons are simplified
The split around 2020-21 is analytically sensible, but it remains a simplification of a complex, overlapping policy and health-system shock.

### Statistical significance is not policy proof
A significant result from Welch’s t-test or Levene’s test supports the existence of a measurable change, but it does not prove why the change happened.

### Correlation is descriptive
Correlation can reveal co-movement between categories, but it should not be presented as evidence of direct substitution, complementarity, or causal relationships without additional evidence.


## Forecasting limitations

### Short annual series
Annual NHS expenditure series do not provide the same depth as long monthly or quarterly series. Forecasts should therefore be presented as indicative rather than fully decision-ready.

### Structural breaks
COVID-era shocks may distort model fit and increase uncertainty. Any forecast that spans the pandemic period should explicitly discuss this issue.

### Model risk
SARIMA and Prophet can produce different answers because they encode trend and structural change differently. Divergence between models should be used as a cue for scenario thinking, not hidden.


## Dashboard limitations

### Dashboard ≠ explanation
A Power BI report improves accessibility, but it does not replace analytical interpretation. Users can still misread charts if metric definitions and hierarchy rules are not documented clearly.

### Comparability caveats
Cross-board comparisons may reflect genuine differences in need, geography, service model, or population structure, not simply management performance.
