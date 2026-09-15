# Fed Funds Rate Impact Study

A time series study of how changes in the U.S. Federal Funds Rate pass through to Treasury
yields, the macroeconomy, financial market volatility and consumer sentiment.

**Site:** <https://elliotzli.com/dsan5600-project-site/>
**Author:** Zhengze (Elliot) Li · DSAN 5600, Georgetown University

---

## What the study found

Fourteen series from [FRED](https://fred.stlouisfed.org/) at four frequencies, modelled with
five classes of method. The main results:

| Section | Result bearing on the Federal Funds Rate |
| --- | --- |
| Exploratory analysis | The three short-maturity spreads are stationary; every other level series has a unit root |
| ARMA / ARIMA | Shocks to the gap between short yields and the policy rate decay with half-lives of 4.1 and 2.3 quarters |
| ARIMAX, inflation | The policy rate lagged twelve months has a coefficient of 0.008 (s.e. 0.009) and adds nothing to forecasts |
| ARIMAX, 30-year yield | A one-point move in the policy rate raises the 30-year yield 0.13 points in the same month |
| VAR, Treasury curve | The policy rate Granger-causes yields out to one year and no further; every yield Granger-causes the policy rate |
| VAR, macroeconomy | A 0.9-point tightening lowers real GDP 0.5% and raises unemployment 0.16 points over two to three years |
| ARCH / GARCH | Volatility is higher in months the rate moves; volatility Granger-causes rate changes, not the reverse |
| Deep learning | The policy rate does not improve one-month forecasts of consumer sentiment in any model class |

The pattern that runs through the study is that at short horizons the policy rate is the variable
being predicted rather than the predictor. Every Treasury yield Granger-causes the Federal Funds
Rate; dollar volatility Granger-causes changes in it; and it adds nothing to one-month forecasts
of inflation or sentiment. Its own effects appear at the short end of the yield curve within
weeks and in output and employment over two to three years.

## Pages

| File | Page |
| --- | --- |
| `index.qmd` | Introduction — the transmission channels the study tests |
| `datasource.qmd` | Data source — every series, its FRED identifier, frequency and units |
| `datavis.qmd` | Visualization — three interactive Plotly charts |
| `eda.qmd` | Exploratory analysis — ACF, PACF and stationarity tests for twelve series |
| `arma.qmd` | ARMA, ARIMA and SARIMA models |
| `arimax.qmd` | ARIMAX and VAR models, with Granger tests and impulse responses |
| `fin-ts-model.qmd` | ARCH and GARCH models of dollar and S&P 500 volatility |
| `deeplearning.qmd` | RNN, LSTM and GRU against ARIMA on consumer sentiment |
| `conclusions.qmd` | Conclusion |

## Repository layout

```
.
├── _quarto.yml           # site configuration, sidebar, theme, grid widths
├── _environment          # sets QUARTO_PYTHON to the project virtualenv
├── styles.css            # site theme
├── theme-head.html       # web-font link, injected into every page head
├── theme-sidebar.html    # "← elliotzli.com" link above the sidebar title
├── citation.bib          # bibliography
├── *.qmd                 # the nine pages listed above
└── data/data/            # 18 spreadsheets downloaded from FRED
```

## Building the site

```bash
quarto render          # whole site, about 15 minutes
quarto render eda.qmd  # one page
```

Output goes to `_site/`. Every page sets `embed-resources: true`, so each HTML file is
self-contained: figures, fonts and JavaScript are all inlined and the pages work offline.
The exceptions are two FRED chart iframes and a YouTube embed on the introduction page.

The long render time is dominated by three things: the rolling GARCH forecasts
(1,346 one-day-ahead refits), the rolling-origin cross-validations in the ARMA and VAR
sections, and training the recurrent networks five times each.

### Requirements

Quarto 1.10, R 4.6 and Python 3.11.

**R packages** — `forecast`, `tseries`, `astsa`, `vars`, `rugarch`, `fGarch`, `FinTS`,
`moments`, `xts`, `readxl`, `dplyr`, `lubridate`, `ggplot2`, `gridExtra`, `knitr`,
`sandwich`, `lmtest`.

```r
install.packages(c("forecast","tseries","astsa","vars","rugarch","fGarch","FinTS",
                   "moments","xts","readxl","dplyr","lubridate","ggplot2","gridExtra",
                   "knitr","sandwich","lmtest"))
```

**Python** — the deep-learning page runs in a virtualenv at `.venv/`, which `_environment`
points Quarto at. TensorFlow is pinned to 2.15 because the page is written in Keras 2 idiom.

```bash
python3.11 -m venv .venv
.venv/bin/pip install "tensorflow==2.15.1" "numpy<2" pandas statsmodels \
                      matplotlib plotly tabulate openpyxl
```

Do not delete `_environment`: without it Quarto picks the system Python and the Jupyter
engine fails.

## Reproducibility

Every number in the prose is taken from output rendered on the same page, and the analysis
re-runs from the spreadsheets in `data/data/` on each render. The neural networks are
estimated with fixed seeds under TensorFlow's deterministic mode, so the deep-learning
results are identical between renders; without that flag they vary by roughly 0.2 index
points of RMSE.

## Notes on the data

Four identifiers end in `FF` — `T3MFF`, `T6MFF`, `T1YFF`, `T5YFF`. These are not yields but
*spreads*: the Treasury yield at that maturity minus the effective Federal Funds Rate on the
same day, in percentage points. The `DGS` series are constant-maturity yields. The data source
page explains the distinction and documents every series.

The 20-year constant-maturity yield has a gap: the Treasury discontinued it at the end of 1986
and reinstated it in October 1993. The exploratory analysis uses only the continuous segment
from 1993.

## Licence

Course project, shared for reference. The underlying data is public domain, published by the
Federal Reserve Bank of St. Louis.
