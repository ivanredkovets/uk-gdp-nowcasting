# UK GDP Nowcasting with Machine Learning

## Research Question

Can machine learning improve UK quarterly GDP growth nowcasts relative to conventional forecasting benchmarks, and how does forecast accuracy evolve as new information becomes available within the quarter?

## Target

UK quarterly real GDP growth (QoQ).

## Data

The dataset combines UK macroeconomic indicators primarily from the Office for National Statistics (ONS), together with data from the Bank of England, OECD and the GfK Consumer Confidence Barometer.

The modelling sample begins in 2006, reflecting the common availability of the predictor series.

### Predictors

- Monthly GDP
- Services output
- Industrial production
- Construction output
- Retail sales
- Unemployment rate
- Vacancies
- Wage growth
- Consumer confidence
- CPI inflation
- Bank Rate
- OECD Composite Leading Indicator (CLI)

## Nowcasting Design

The project uses three within-quarter information sets to approximate the flow of information available to a forecaster during each quarter:

- **M1** — information available during the first month of the quarter
- **M2** — information available during the second month of the quarter
- **M3** — information available during the third month of the quarter

Monthly indicators are mapped into quarterly M1/M2/M3 features. Indicator-specific publication lags are used to construct ragged-edge datasets, so each information set contains only observations that would plausibly have been available at that point in the quarter.

This structure allows the analysis to examine whether forecast accuracy improves as additional macroeconomic information becomes available within the quarter.

## Forecasting Models

### Benchmarks

- Naive forecast
- AR(1)

### Regularised Regression

- Ridge regression

### Machine Learning

- Random Forest
- Gradient Boosting

## Evaluation Framework

Models are evaluated using an expanding-window pseudo-real-time forecasting framework over a common out-of-sample period from **2017Q1 to 2026Q1**.

For each forecast quarter, models are estimated using only observations preceding that quarter. The forecasting exercise is repeated separately for the M1, M2 and M3 information sets.

Forecast performance is evaluated using:

- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- Directional Accuracy (DA)
- Out-of-Sample R² relative to the Naive benchmark

The evaluation also compares performance during the COVID-19 period with the remaining out-of-sample observations because the extreme GDP movements during the pandemic have a substantial effect on aggregate forecast errors.

## Key Results

Ridge M3 achieves the strongest overall performance by RMSE, with an RMSE of **3.929** and an out-of-sample R² of **71.6%** relative to the Naive benchmark.

Gradient Boosting M3 achieves an RMSE of **4.266**, while Random Forest M3 records the lowest MAE of **1.556**.

Forecast performance improves from M1 to M3 across all three model families, providing consistent evidence that additional within-quarter information improves GDP nowcasts. The gains are particularly large for Random Forest and Gradient Boosting.

The results therefore provide evidence that richer within-quarter information improves GDP nowcasts. However, the machine-learning models do not consistently outperform Ridge regression, suggesting that a relatively simple regularised linear model remains highly competitive in this small macroeconomic dataset.

Forecast errors are strongly concentrated around the COVID-19 shock. Outside the pandemic period, forecast errors are substantially smaller across all models.

## Model Interpretation

Model interpretation focuses on the final M3 information set.

- Random Forest feature importance is used to identify the indicators most heavily used by the fitted tree ensemble.
- SHAP values are used to examine the contribution of individual predictors to Gradient Boosting forecasts.
- Standardised Ridge coefficients are used to examine the direction and relative magnitude of relationships in the best-performing linear model.

The three approaches highlight a broadly consistent group of informative predictors. Services activity, the OECD Composite Leading Indicator, retail sales, consumer confidence and monthly GDP appear prominently across the models.

Ridge places the greatest weight on services activity, while the OECD CLI and construction also show relatively stable positive relationships with predicted GDP growth. Random Forest relies most heavily on the OECD CLI, consumer confidence, services activity and monthly GDP.

SHAP analysis of Gradient Boosting identifies retail sales, consumer confidence, the OECD CLI and services activity as the strongest contributors to out-of-sample forecasts. Their effects are nonlinear and concentrated in particular forecasting periods, while inflation, vacancies and Bank Rate make relatively small contributions to the Gradient Boosting predictions.

Overall, the interpretation results suggest that real-activity, sentiment and leading indicators contain the most useful information for the M3 GDP nowcasts, although their relative importance varies across model specifications.

## Consumer Confidence Data

UK consumer confidence observations were manually compiled from publicly reported GfK Consumer Confidence Barometer values available through the Moneycontrol economic calendar and cross-checked against selected official GfK/NIQ releases.

A gap between May 2012 and February 2013 was reconstructed using contemporaneous reports of published GfK values. These observations were sourced from reported historical values rather than interpolated or statistically estimated.

## Limitations

Several limitations should be considered when interpreting the results.

First, the quarterly sample is relatively small, limiting the amount of data available for training more complex machine-learning models.

Second, the COVID-19 shock generates exceptionally large GDP movements and therefore has a substantial influence on full-sample forecast metrics.

Third, the M1/M2/M3 datasets approximate the historical information available to forecasters using indicator-specific publication lags. They do not constitute a complete real-time vintage database and therefore cannot fully account for subsequent revisions to historical macroeconomic data.

Finally, part of the historical consumer confidence series was manually compiled from publicly reported GfK values because a complete freely accessible historical API was not available.

## Repository Structure

- `data/raw/` — original macroeconomic series
- `data/processed/` — cleaned and transformed datasets
- `data/results/` — model evaluation results
- `notebooks/` — data collection, engineering, modelling and evaluation notebooks
- `figures/` — figures used in the analysis