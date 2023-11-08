# Project Documentation

## Overview

This repository documents an extensive analysis of the impact of the Fed Funds Rate on various sectors of the economy. The study delves into the dynamics of the bond market, stock market, exchange rates, inflation, and unemployment to understand the broader implications of monetary policy adjustments.

### Table of Contents

-   [Introduction](#introduction)
-   [Data Sources and Visualization](#data-sources-and-visualization)
-   [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
-   [Time Series Modeling](#time-series-modeling)
-   [Financial Modeling](#fin-modeling)
-   [Deep Learning Approaches](#deep-learning-approaches)
-   [Spectral Analysis and Filtering (SAF)](#spectral-analysis-and-filtering-saf)
-   [Conclusions](#conclusions)
-   [References](#references)

### Project Structure

```         
.
├── README.md
├── _quarto.yml
├── arimax.qmd
├── arma.qmd
├── citation.bib
├── conclusions.qmd
├── data
│   ├── data
│   │   ├── [Excel datasets]
│   ├── journal
│   │   └── federal-reserve-hls.pdf
│   └── plot
│       ├── [Image plots]
├── datasource.qmd
├── datavis.qmd
├── deeplearning.qmd
├── eda.qmd
├── fin-ts-model.qmd
├── index.qmd
├── intro.qmd
├── saf.qmd
└── styles.css
```

This repository contains `.qmd` files for analysis, a bibliography file, datasets in Excel format, PDF documents for reference, and image files for visualization.

### Introduction {#introduction}

The introductory `intro.qmd` addresses the importance of the risk-free rate in the financial ecosystem, with a focus on the Treasury Bill (T-Bill) interest rate as a benchmark. It also clarifies the role of the Federal Reserve in influencing the Fed Funds Rate, which impacts the yield curve and overall interest rates.

### Data Source and Visualization {#data-source-and-visualization}

This section (`datasource.qmd` and `datavis.qmd`) covers the datasets used for analysis and the visual representation of our findings.

### Exploratory Data Analysis {#exploratory-data-analysis}

The EDA process is documented in `eda.qmd`, which includes a rigorous analysis of the data related to the Fed Funds Rate and its economic implications.

### Time Series Modeling {#time-series-modeling}

Time series models such as `ARIMA`, `ARIMAX`, `SARIMA`, `ARIMAX`, and `VAR` are explored in `arma.qmd` and `arimax.qmd` files to forecast and understand the temporal patterns in economic data.

### Financial Modeling {#fin-modeling}

These files document `arch.qmd` and `garch.qmd` shows the methodologies and results of financial analysis `ARCH` and `GARCH` conducted on economic data.

### Deep Learning Approaches {#deep-learning-approaches}

`deeplearning.qmd` explores the use of advanced neural networks to model complex economic interactions.

### Spectral Analysis and Filtering (SAF) {#spectral-analysis-and-filtering-saf}

`saf.qmd` covers techniques used to analyze and filter signals in the frequency domain, providing insights into cyclical behaviors within the financial data.

### Conclusions {#conclusions}

The `conclusions.qmd` file synthesizes the insights and findings from the various analyses conducted.

### References {#references}

Refer to `citation.bib` for a comprehensive list of all the academic and data sources referenced throughout the project.
