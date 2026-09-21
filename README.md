# ARIMA-inflation-forecasting
This project features fitting an ARIMA model for forecasting UK inflation over years 1989-2022 out of 5 candidates, running diagnostics on wellness of fit, and discussing the consequences for implementing policy based on results. 

# README

## Project Overview

This project chooses the best candidate ARIMA (p,d,q) model out of 5 candidates for inflation forecasting based on UK inflation percentage change in price level data from 1982-2022. The candidates were ARIMA (2,0,0), ARIMA (1,0,0), ARIMA (1,0,1), ARIMA (2,0,1), ARIMA (2,0,2). The initial ARIMA (2,0,0) model was suggested from a unit root test under an ADF to find the order of differencing required, and ACF and PACF plots to determine the order of MA and AR components in the model respectively. The best candidate is chosen from the AIC, BIC, MAE and RMSE measures. The objective of the report is to determine if an appropriate ARIMA model can successfully forecast inflation. Diagnostics are run to check if the model is the best fit including looking at residual plots and ACF of residuals. A full research report including a literature review, reproducible Python notebook, and supporting documentation are included in this repository.

## Research Question

The report assesses the suitability of the ARIMA (p,d,q) model for forecasting UK inflation. It aims to evaluate whether a successful ARIMA model can be fitted and whether this can be utilised in practise by central banks when conducting policy decisions in response to inflation fluctuations.

## Dataset

The data is publicly available on Kaggle titled 'UK Inflation Data 1989-2022' with link: <https://www.kaggle.com/datasets/scarfsman/uk-inflation-data-1989-2022>. The dataset is licensed under the Open Government License (OGL) 3.0, and contains public sector information licensed under the OGL 3.0.

It covers 415 observations of monthly inflation from 1989 to 2022 by looking at the CPIH which builds on the CPI index by additionally accounting for costs relating to housing which include rent and mortgage payments — excluding housing costs.

Note that the dataset isn't included directly in this repository and it should be downloaded directly from Kaggle using kagglehub.

## Methodology

### Data cleaning

No data cleaning was required as there were no missing values. Although the box plot suggested there were multiple outliers, this is consistent with periods of high economic volatility and therefore these weren't removed from the time series data. The data was split into an 80:20 test train split.

### EDA

Over the 30-year period, inflation averaged 2.84%, not far from the BoE target. However, the max reached 9.6% during covid and the minimum was 0.2%. A histogram shows the most frequent inflation rate was between 2-3% for more than a third of the observations. The box plot suggests the average was lower, closer to the 2% target and instead classifies any values over 5% as outliers.

The unit root test confirmed stationarity at the 1% significance level suggesting d=0. The PACF indicated an AR order of p=2 but the ACF decayed slowly and therefore the order of MA is inconclusive. An initial model prediction is the ARIMA (2,0,0), however multiple models are tested.

### Models

The following models were tested against the data:

1. ARIMA (2,0,0)
2. ARIMA (1,0,0)
3. ARIMA (1,0,1)
4. ARIMA (2,0,1)
5. ARIMA (2,0,2)

### Forecast Evaluation

The AIC, BIC, RMSE and MAE are collectively used to find the best forecasting model amongst the candidates. Both AIC and BIC models provide a trade-off between data accuracy and model complexity to prevent overfitting — smaller values are preferred. The RMSE and MAE evaluate prediction errors to find how each model performs relative to actual outcomes in the test set.

## Results

<img width="345" height="202" alt="image1" src="https://github.com/user-attachments/assets/d33c19f8-b589-4411-809a-b257a04b5a9b" />

The ARIMA (2,0,1) performed best among the candidate models, achieving the lowest AIC, BIC, RMSE and MAE. Although the PACF suggested an AR order of two, the ACF did not provide a clear indication of the appropriate MA order, highlighting the value of comparing multiple candidate specifications.

## Key Findings

- Unit root test, ACF and PACF plots suggest ARIMA (2,0,0) as a suitable model
- ARIMA (2,0,1) was actually the best performing model
- ARIMA (2,0,1) forecasts don't appear consistent with real life
- ARIMA models are useful for policymaking
- Policymakers must be cautious of ARIMA limitations before implementing policy

## Repository Structure

| File | Description |
|---|---|
| `README_inflation.md` | Project overview, setup instructions, methodology and key findings |
| `Time_series_report.pdf` | Full research report with literature review, methodology, results and discussion |
| `Inflation_ARIMA.ipynb` | ARIMA model implementation and selection with forecasts |
| `requirements_inf.txt` | Required Python packages |
| `LICENSE` | MIT License |
| `.gitignore` | Specifies files ignored by Git |

## Requirements

- Python 3.12
- kagglehub
- matplotlib
- pandas
- seaborn
- numpy
- sklearn
- statsmodels

## How to run

1. Clone the repository
2. Install the required Python packages
3. Open the notebook: `inflation_ARIMA.ipynb`
4. Run all the cells from top to bottom

## Limitations

- Forecasting accuracy deteriorates as the forecast horizon increases. This is because, although past data is used to model the future, structural breaks occur over time which can change inflation dynamics.
- Changing volatility in inflation can violate the constant variance assumption which is necessary for stationarity.
- Too short time series require that sample size should increase with the number of parameters estimated and data noise. Additionally, too long time series can lead to predictable dynamics in the time series process.
- Models produce problems when fitting on training data and evaluating on test data as comparisons on the test set use different forecast horizons and combine results with different variances.

## Future Improvements

- Test additional forecasting models, for example machine/deep learning models.
- Utilise the ARIMA model amongst a combination of models when making policy decisions including human judgement.
