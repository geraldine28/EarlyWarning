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
├── acled_data.R # Load and process ACLED event data
├── gdelt_data.R # Load and aggregate GDELT indicators
├── inform_data.R # Fetch INFORM scores
├── FAO_prices.R # Preprocess FAO food price data

├── meta_script/
│ ├── ImputedMonthlyData.R # Master script: merge + impute
│ ├── monthly_lags_differences.R # Generate lagged predictors
│ ├── monthly_cp.R # Create composite indicators
│ ├── reweigh.R # Apply weight adjustments
│ ├── h2o_monthly.R # Train model via H2O
│ └── prepare_shiny_data.R # Format data for Shiny app

