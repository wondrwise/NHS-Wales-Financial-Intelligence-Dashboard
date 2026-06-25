## Analytical improvements

### Add backtesting
Compare forecast models more formally using:

- rolling-origin validation
- RMSE
- MAE
- MAPE
- residual diagnostics

### Expand operational context
The Drive folder appears to include operational intelligence and KPI monitoring material. Bringing in waiting times, admissions, workforce pressure, or service activity would help relate financial change to service pressure more directly.


### Add scenario analysis
Create explicit scenarios such as:

- baseline trend continuation
- post-COVID normalisation
- elevated structural pressure
- selective priority-growth scenario


## Data engineering improvements

### Add a data dictionary-first workflow
Store all source-to-model mappings in one place so future repo users can trace raw fields to final dashboard measures.

### Add validation tests
Build validation checks into reusable functions or lightweight unit tests to ensure:

- no duplicate grain violations
- valid percentage ranges
- no broken category hierarchy flags
- consistent year ordering

### Add parameterisation
Move hard-coded filepaths, baseline years, and board filters into configuration variables.


## Dashboard improvements

### Add a dedicated landing page
Create a concise landing page that explains the three analytical lenses before users dive into the report.

### Improve benchmarking views
Add:

- distribution bands
- board peer groups
- percentile positioning
- consistency flags over rolling windows

### Publish a service version if appropriate
If governance allows, publish a Power BI Service version and create a lightweight dashboard for executive viewers while preserving the report as the main analytical artefact.
