# Early Warning of Forced Displacement Risk (R) 

This repository contains the R codebase behind a predictive early warning risk model designed to anticipate forced displacement risks. 
It ingests multiple data streams and generates forecasts at the monthly national level to support anticipatory action.

> **Note**: Due to the sensitive nature of the data and outputs, only code is shared here. The full Shiny app and datasets are restricted.

---

## Overview

The system builds a monthly forecasting pipeline using publicly available and internal indicators, including:

- **ACLED**: conflict event data
- **GDELT**: media reporting indicators
- **INFORM**: vulnerability and hazard indices
- **FAO**: market price data
- **TheGlobalEconomy**: economic, political, and demographic indicators 

Forecasts are produced using gradient boosting models (via `h2o`) and fed into a modular Shiny app for internal decision-making.

---

## Repository Structure
early-warning-r/
  - acled_data.R # Load and process ACLED event data
  - gdelt_data.R # Load and aggregate GDELT indicators
  - inform_data.R # Fetch INFORM scores
  - FAO_prices.R # Preprocess FAO food price data

  - meta_script/
      - ImputedMonthlyData.R # Master script: merge + impute
      - monthly_lags_differences.R # Generate lagged predictors
      - monthly_cp.R # Find changepoints in country time series
      - reweigh.R # Transform, normalise and standardise variables
      - h2o_monthly.R # Train model via H2O
      - prepare_shiny_data.R # Format data for Shiny app


---

## Model Logic

The system:
1. Loads multi-source indicators
2. Imputes missing values and harmonizes time/frequency
3. Finds changepoints in country time series 
4. Engineers lags and composite predictors
5. Trains models using H2O's scalable machine learning framework
6. Outputs probabilistic risks for forced displacement

---

## Data & Shiny App Access

This repo does **not** include:
- The original datasets
- The Shiny application interface
- Output files or internal thresholds

However, the code is modular and can be adapted to public or alternative datasets with the same structure.

---

## Evaluation & Results

An evaluation has been conducted on historical data across data from 2020 to 2024, which can be found here:
[View Interactive Evaluation Report](https://geraldine28.github.io/EarlyWarning/evaluation_report.html)


  
---

## How to Run
Run scripts in the following order:

```r
# Data sets
source("acled_data.R")
source("gdelt_data.R")
source("inform_data.R")
source("FAO_prices.R")

# Prepare model input
source("meta_script/ImputedMonthlyData.R")
source("meta_script/monthly_lags_differences.R")
source("meta_script/monthly_cp.R")
source("meta_script/reweigh.R")

# Model training and Shiny prep
source("meta_script/h2o_monthly.R")
source("meta_script/prepare_shiny_data.R")
```

