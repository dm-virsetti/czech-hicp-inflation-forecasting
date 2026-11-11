# Model specification and reported results

## Research question

Which factors are associated with short-term changes in Czech HICP inflation, and how does the selected dynamic model perform when forecasting the period January 2023–March 2025?

## Data

- Frequency: monthly.
- Source documented in the report: Eurostat.
- Report coverage: January 2008–March 2025.
- Estimation sample: March 2008–December 2022.
- Forecast/evaluation period: January 2023–March 2025.

The source report does not provide a separate raw data file in the materials supplied for this repository.

## Selected dynamic specification

```text
d_HICP_t = α + β1·d_ENERGY_t + β2·d_ULC_t
           + γ·d_HICP_(t-1) + Σ(δ_m·D_m,t) + ε_t
```

Seasonal dummies: `dm2`–`dm12`.

- Dependent variable: `d_HICP`.
- Explanatory variables: `d_ENERGY`, `d_ULC`, `d_HICP(-1)`, and monthly dummy variables.
- `d_UNEMP` and `d_EURCZK` were considered but excluded as statistically insignificant in the report.

## ADF test results reported

| Series | Levels p-value | First-difference p-value |
|---|---:|---:|
| HICP | 0.197 | 0.00003 |
| ENERGY | 0.069 | 0.005 |
| ULC | 0.770 | < 0.001 |

The report concludes that the series are integrated of order one and uses first differences for modelling.

## Reported coefficient interpretations

| Term | Approximate interpretation |
|---|---|
| `d_ENERGY` | +0.136 p.p. in `d_HICP` for a 1 p.p. increase in `d_ENERGY` |
| `d_ULC` | +0.083 p.p. in `d_HICP` for a 1 p.p. increase in `d_ULC` |
| `d_HICP(-1)` | +0.246 p.p. in current `d_HICP` for a 1 p.p. increase in the previous month's `d_HICP` |

These are the marginal-effect interpretations stated in the report, not a reconstructed coefficient table.

## Fit and forecast metrics

- R-squared: `0.64`.
- Mean ex-ante forecast error: approximately `0.38`.
- MAE: `0.418`.
- MSE: `0.505`.
- Forecast confidence intervals: `95%`.

## Diagnostics reported

| Test | p-value / range |
|---|---:|
| VIF | 1.02–1.95 |
| Ramsey RESET | 0.0000 |
| Doornik–Hansen normality | 0.00001 |
| Breusch–Godfrey autocorrelation | 0.0006 |
| Ljung–Box autocorrelation | 0.0012 |
| White heteroskedasticity | 0.000001 |

The report applies OLS with HAC-robust standard errors. It also reports that the RESET, residual normality, autocorrelation, and heteroskedasticity tests reject their respective null hypotheses. These limitations should be kept visible when interpreting model results.

## Reproducibility note

The available source material is the original project report in PDF form. It does not include a separate original estimation script, econometric workfile, or raw Eurostat data extract. This summary documents the model and results from the report; it is not a replacement for the original estimation environment.
