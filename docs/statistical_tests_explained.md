## Purpose

This document explains the main tests used in the NHS Wales expenditure project and why they were appropriate for the questions being asked.



## Welch’s t-test

### What it tests
Welch’s t-test compares the means of two groups when equal variance cannot safely be assumed.

### Why it was used here
The project compares expenditure before and after the COVID shock. The pandemic period is likely to have changed both the scale and the variability of spending, so a method that does not rely on equal variances is a sensible default.

### Typical use in this project
Examples include:

- pre-COVID vs post-COVID total expenditure
- pre-COVID vs post-COVID per-head expenditure
- pre-COVID vs post-COVID allocation share for selected categories

### Interpretation
- `p < 0.05`: evidence of a statistically meaningful change in average level
- `p >= 0.05`: no strong evidence of a mean shift at the chosen threshold

### Practical warning
A statistically significant result does **not** by itself prove a policy cause. It tells us that the observed difference is unlikely to be explained by random sampling variation alone under the model assumptions.



## Levene’s test

### What it tests
Levene’s test checks whether two or more groups have different variances.

### Why it was used here
In healthcare finance, the question is not only whether average expenditure changed, but also whether spending became more volatile after the pandemic shock.

### Typical use in this project
- comparing variance in category expenditure before and after COVID
- checking whether volatility increased in specific service areas
- distinguishing controlled reallocation from erratic funding patterns

### Interpretation
- `p < 0.05`: evidence that volatility changed
- `p >= 0.05`: no strong evidence of a variance shift



## Correlation analysis

### What it tests
Correlation analysis measures the strength and direction of association between variables.

### Why it was used here
The technique is useful for seeing whether expenditure categories tend to move together or in opposite directions. This can help identify areas that appear to co-expand or relative trade-offs in the budget mix.

### Interpretation
- positive values: categories tend to move together
- negative values: one tends to rise when another falls
- values near zero: weak linear relationship

### Warning
Correlation is descriptive. It should not be framed as causal without stronger evidence.



## Augmented Dickey-Fuller test

### What it tests
The Augmented Dickey-Fuller test evaluates whether a time series has a unit root, which is a common way of testing for non-stationarity.

### Why it matters here
ARIMA-family models generally require careful treatment of non-stationary series. If the financial series has a strong trend or level shift, differencing or alternative modelling choices may be required before or during forecasting.

### Interpretation
- low p-value: evidence against a unit root
- high p-value: the series may need differencing or alternative treatment



## Ljung-Box test

### What it tests
The Ljung-Box test evaluates whether residual autocorrelation remains in a model.

### Why it matters here
A forecasting model should not leave systematic structure unexplained. If residuals still contain autocorrelation, the model may be under-specified.

### Interpretation
- low p-value: residuals still contain autocorrelation
- high p-value: residual autocorrelation is less evident



## SARIMA / SARIMAX

### What it is
SARIMA extends ARIMA by modelling seasonal structure. SARIMAX adds exogenous regressors if needed.

### Why it suits this project
NHS finance data is an ordered time series where trend, persistence, and possible structural shifts matter. SARIMA-type models are transparent and diagnostic-friendly, which makes them attractive for a portfolio project where you want to explain the modelling choices.

### What to document
For any SARIMA/SARIMAX model, record:

- target series
- train/test split
- differencing logic
- order selection logic
- information criteria used
- residual checks
- forecast horizon



## Prophet

### What it is
Prophet is a forecasting library designed around decomposable trend and seasonality, with built-in handling for changepoints and tools for cross-validation and performance measurement.

### Why it suits this project
Prophet is useful as a benchmark model when structural change matters. In this NHS project, the COVID shock is precisely the kind of event that should make you think about changepoints and abnormal periods.

### What to document
For any Prophet model, record:

- whether yearly seasonality was used
- whether COVID-era periods were annotated or treated specially
- changepoint sensitivity settings
- cross-validation horizon
- RMSE / MAE / MAPE or other reported metrics
