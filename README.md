# UK GDP Nowcasting with Machine Learning

## Research Question

Can machine learning improve end-of-quarter nowcasts of UK quarterly GDP growth relative to conventional econometric benchmarks?

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
- Composite PMI
- Consumer confidence
- CPI inflation
- Bank Rate

## Planned Models

### Benchmarks
- Naive forecast
- Autoregression
- Ridge regression
- Bridge Equatoin

### Machine Learning
- Random Forest
- Gradient Boosting / XGBoost

## Evaluation

- Expanding-window pseudo-real-time evaluation
- RMSE
- MAE
- Directional accuracy

## Interpretation

SHAP values will be used to investigate which indicators drive the model's GDP nowcasts.