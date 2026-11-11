# Czech HICP Inflation Forecasting

An applied time-series econometrics project developed for the **Econometrics I** course at the SGH Warsaw School of Economics. The project models monthly changes in the Harmonised Index of Consumer Prices (HICP) in Czechia and evaluates forecasts for the period from January 2023 to March 2025.

> The repository includes the original project report in Polish and an English technical summary. The underlying Eurostat data file and original estimation-workfile or source-code file were not included in the supplied materials.

## Project overview

The objective was to explain short-term movements in Czech HICP inflation and assess whether a dynamic econometric model could be used for short-term forecasting. Monthly observations were obtained from Eurostat. The report covers the period **January 2008 – March 2025**.

The analysis considered static and dynamic specifications. The selected specification was a dynamic model with a lagged dependent variable and monthly seasonal indicators.

## Model specification

The dependent variable is the first difference of HICP:

```text
d_HICP_t = α + β1·d_ENERGY_t + β2·d_ULC_t
           + γ·d_HICP_(t-1) + Σ(δ_m·D_m,t) + ε_t
```

where:

| Variable | Description |
|---|---|
| `d_HICP` | Monthly first difference of Czech HICP; dependent variable |
| `d_ENERGY` | Monthly first difference of the HICP energy component |
| `d_ULC` | Monthly first difference of unit labour costs |
| `d_HICP(-1)` | One-month lag of the dependent variable |
| `dm2`–`dm12` | Monthly dummy variables used to control for seasonality |

The report also considers unemployment (`UNEMP`) and the EUR/CZK exchange rate. Their differenced forms were excluded from the final specification because they were statistically insignificant in the reported tests (`p = 0.3843` and `p = 0.7939`, respectively).

## Time-series preparation

The report applies Augmented Dickey–Fuller (ADF) tests and first-differences the non-stationary series before estimation. Reported p-values include:

| Series | In levels | First difference |
|---|---:|---:|
| HICP | 0.197 | 0.00003 |
| Energy component | 0.069 | 0.005 |
| Unit labour costs (ULC) | 0.770 | < 0.001 |

The first-differenced series are reported as stationary. Monthly dummy variables are included to account for seasonality.

## Estimation and forecast periods

| Stage | Period |
|---|---|
| Model estimation | March 2008 – December 2022 |
| Forecast and ex-post evaluation | January 2023 – March 2025 |

The report states that 95% confidence intervals were calculated for the forecasts.

## Main results

The report gives the following interpretations for the selected model:

- A 1 percentage-point increase in the monthly change in energy prices is associated with an approximately **0.136 percentage-point** increase in the monthly change in HICP, ceteris paribus.
- A 1 percentage-point increase in the monthly change in unit labour costs is associated with an approximately **0.083 percentage-point** increase in the monthly change in HICP, ceteris paribus.
- A 1 percentage-point increase in the previous month's change in HICP is associated with an approximately **0.246 percentage-point** increase in the current month's change in HICP, ceteris paribus.

The reported coefficient of determination is **R² = 0.64**.

### Forecast evaluation

| Metric | Reported result |
|---|---:|
| Mean ex-ante forecast error | Approximately 0.38 |
| MAE | 0.418 |
| MSE | 0.505 |

These values are reproduced from the course report. They should be interpreted alongside the diagnostic results below rather than as a standalone guarantee of forecast quality.

## Diagnostic checks and limitations

The report records several diagnostic concerns:

| Check | Reported result | Interpretation in the report |
|---|---:|---|
| VIF | Approximately 1.02–1.95 | No material multicollinearity indicated |
| Ramsey RESET | p = 0.0000 | Rejects the null of correct specification |
| Doornik–Hansen normality test | p = 0.00001 | Rejects residual normality |
| Breusch–Godfrey test | p = 0.0006 | Evidence of residual autocorrelation |
| Ljung–Box test | p = 0.0012 | Evidence of residual autocorrelation |
| White test | p = 0.000001 | Evidence of heteroskedasticity |

The report applies OLS (MNK/KMNK) estimation with **HAC-robust standard errors** to address the inference issues associated with heteroskedasticity and autocorrelation. However, the reported RESET result and other diagnostics remain important limitations of the model. The model should therefore be viewed as an academic forecasting exercise, with its assumptions and diagnostic weaknesses made explicit.

## Repository contents

```text
czech-hicp-inflation-forecasting/
├── README.md
├── model/
│   └── model_specification.md
└── report/
    └── czech_hicp_econometric_model_report.pdf
```

## How to explore the project

1. Read this README for the English overview of the research question, model, and reported results.
2. Open `model/model_specification.md` for a concise technical summary of the variables, estimation setup, diagnostics, and forecast metrics.
3. Open `report/czech_hicp_econometric_model_report.pdf` for the original five-page course report in Polish.

## Tools and data source

- **Data source:** Eurostat monthly HICP data, as documented in the report.
- **Methods:** time-series analysis, ADF stationarity testing, first differences, dynamic DL/ADL specification, seasonal dummy variables, OLS estimation, HAC-robust standard errors, and forecast evaluation with MAE and MSE.

The supplied materials did not include a separate data extract or original econometric software workfile / code script. No such files have been recreated or presented as original project files.
