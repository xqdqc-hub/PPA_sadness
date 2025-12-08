# Philadelphia Eviction Forecasting Project

## Project Description

This project develops a spatiotemporal predictive model to forecast quarterly eviction filings at the census tract level in Philadelphia, one quarter (≈ 3 months) in advance. The goal is to provide city agencies and community organizations with an early-warning tool to identify emerging eviction hotspots and more effectively target rental assistance, legal aid, and outreach.

## Data Sources

The analysis integrates multiple datasets:

- **Eviction filings** from Eviction Lab (weekly data aggregated to tract–quarter level)
- **ACS 2022 5-year estimates** (income, race, tenure, rent burden, education, poverty)
- **OPA property assessments** (market value, low-value parcels, tax delinquency)
- **Crime incidents** (crime offenses, converted to crime rate per 1,000 residents)
- **SEPTA transit stops** (number of stations within 800m of each tract centroid)
- **Census TIGER/Line shapefiles** (tract geometries for mapping and spatial weights)

All data are cleaned, joined by GEOID and spatial relationships, and assembled into a tract–quarter panel suitable for modeling.

## Methods

We follow a model-building pipeline that includes:

- **Exploratory Data Analysis (EDA)**: spatial maps, distributions, correlation matrices, Moran’s I, LISA cluster maps, and VIF checks.
- **Baseline models**: OLS and time-lagged OLS to assess temporal persistence and baseline fit.
- **Count models**: Poisson and Negative Binomial regression to account for skewed, non-negative eviction counts and overdispersion.
- **Spatial models**: spatial lag (SLX/SAR) specifications and Moran’s eigenvector filtering to model spatial dependence and remove residual spatial autocorrelation.
- **Model comparison**: AIC, deviance, log-likelihood, out-of-sample RMSE/MAE, and residual diagnostics.

The final preferred model is an Eigenvector-Filtered Negative Binomial specification that combines temporal lag, structural neighborhood characteristics, property conditions, crime, transit access, and spatial structure.


