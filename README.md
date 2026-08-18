# UK GDP Nowcasting with Machine Learning

## Research Question

Can machine learning improve UK quarterly GDP growth nowcasts relative to conventional econometric benchmarks, and how does forecast accuracy evolve as new information becomes available within the quarter?

## Target

UK quarterly real GDP growth (QoQ).

## Core Predictors

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

Monthly indicators are mapped into quarterly M1/M2/M3 features. Indicator-specific publication lags are used to construct ragged edge datasets, so each information set contains only observations that would plausibly have been available at that point in the quarter.

This allows the project to evaluate not only end-of-quarter nowcast performance, but also how GDP nowcasts improve as additional information arrives during the quarter.

## Data

The dataset combines UK macroeconomic indicators primarily from the Office for National Statistics (ONS), together with the Bank of England, OECD and GfK Consumer Confidence Barometer.

The modelling sample begins in 2006, reflecting the common availability of the predictor series.

### Consumer Confidence

UK consumer confidence data were manually compiled from publicly reported GfK Consumer Confidence Barometer values available through the Moneycontrol economic calendar. Selected observations were cross-checked against official GfK/NIQ releases.

Manual collection was used because a freely accessible historical API providing the complete series was not available. The sample begins in January 2006, consistent with GfK/NIQ's stated availability of historical back data from 2006.

A gap in the Moneycontrol historical series between May 2012 and February 2013 was reconstructed using contemporaneous publicly available reports of the GfK Consumer Confidence Barometer. These observations were sourced from reported GfK values rather than interpolated or statistically estimated.

## Planned Models

### Benchmarks

- Naive forecast
- Autoregression (AR)
- Ridge regression

### Machine Learning

- Random Forest
- Gradient Boosting / XGBoost

## Evaluation

Models will be evaluated using an expanding-window pseudo-real-time framework across the M1, M2 and M3 information sets.

Performance will be compared using:

- RMSE
- MAE
- Directional accuracy

The M1/M2/M3 structure will also be used to examine how forecast accuracy changes as additional monthly information becomes available within the quarter.

## Interpretation

SHAP values will be used to investigate which indicators contribute most strongly to the machine-learning GDP nowcasts using the final M3 information set.