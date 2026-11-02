# Airline Passenger Demand Forecasting

A time-series modeling project comparing **13 forecasting approaches** on monthly airline passenger counts. The objective is to examine how trend and seasonality affect forecast quality and to compare statistical baselines with exponential-smoothing and ARIMA-family methods.

## Problem statement

Use historical monthly passenger counts to forecast future demand and support planning for staffing, capacity, and operational resources.

## Dataset

The repository includes `AirPassengers.csv`, containing the classic monthly AirPassengers series.

| Attribute | Description |
|---|---|
| `Month` | Observation month |
| `Passengers` | Monthly passenger count |
| Period | January 1949 – December 1960 |
| Frequency | Monthly |
| Observations | 144 |
| Training period | First 120 months |
| Test period | Final 24 months |

The train/test split is chronological, preserving the time ordering of the observations.

## Forecasting approaches

The notebook compares 13 models:

| Family | Models |
|---|---|
| Baselines and trend | Linear Regression, Naive, Simple Average, Simple Moving Average |
| Exponential smoothing | Simple Exponential Smoothing, Holt's Method, Holt-Winters Additive, Holt-Winters Multiplicative |
| Autoregressive models | AR, MA, ARMA, ARIMA, SARIMA |

## Methodology

1. Parse and sort the monthly date column.
2. Reserve the last 24 observations as a chronological test set.
3. Explore the series trend and seasonal structure.
4. Compare baseline forecasts with exponential smoothing models.
5. Use ACF/PACF plots and differencing to inform AR-family model specification.
6. Apply a Box-Cox transformation with `lambda=0` (a natural-log transformation) for the AR-family experiments and reverse the transformation for forecast evaluation.
7. Evaluate forecasts on the held-out observations using RMSE and MAPE.

## Test-set performance

The values below are read from the saved notebook outputs. Lower is better for both metrics.

| Model | RMSE | MAPE |
|---|---:|---:|
| Linear Regression | 74.81 | 11.22% |
| Naive | 137.33 | 23.58% |
| Simple Average | 219.44 | 44.23% |
| Simple Moving Average | 120.51 | 19.27% |
| Simple Exponential Smoothing | 137.33 | 23.58% |
| Holt's Method | 115.70 | 18.41% |
| Holt-Winters Additive | 35.76 | 6.64% |
| **Holt-Winters Multiplicative** | **32.49** | **6.39%** |
| AR | 70.57 | 11.62% |
| MA | 76.28 | 15.33% |
| ARMA | 83.36 | 17.20% |
| ARIMA | 79.35 | 13.84% |
| SARIMA | 77.65 | 10.00% |

### Main finding

**Holt-Winters Multiplicative** has the lowest RMSE and MAPE among the reported models. This is consistent with a series where seasonal variation grows with the overall level.

The notebook's SARIMA specification is `(7,1,4) × (0,1,0,3)`. Because the data are monthly, `m=3` represents a three-observation seasonal lag, not a 12-month annual seasonal cycle. The README previously described this as annual seasonality; that interpretation should not be made without re-running the experiment using `m=12` and comparing results.

The ARIMA branch's inverse-differencing/reconstruction steps should also be checked before relying on its reported metric as a fully comparable forecast result. The performance table is reproduced from the notebook outputs, not independently re-run here.

## Technology stack

- Python, pandas, NumPy
- Statsmodels: exponential smoothing, ARIMA, SARIMA
- scikit-learn: Linear Regression and RMSE
- SciPy: Box-Cox transformation
- Matplotlib and Seaborn: visualization

## Repository contents

```text
.
├── AirPassengers.csv
├── TSA_Graded_Exercise.ipynb
└── README.md
```

## How to run

```bash
git clone https://github.com/piyush0920/airline-passenger-forecasting.git
cd airline-passenger-forecasting

pip install pandas numpy matplotlib seaborn statsmodels scikit-learn scipy jupyter
jupyter notebook TSA_Graded_Exercise.ipynb
```

Run the notebook cells in order. The CSV is already included in the repository.

## Limitations and next steps

- This is a small, historical, univariate dataset; it does not include explanatory drivers such as price, capacity, or macroeconomic conditions.
- Validate seasonal periods and forecast reconstruction steps before making model-selection claims.
- Use rolling-origin validation to test stability across multiple forecast origins.
- Compare seasonal models with a consistent 12-month annual period for monthly data.

## Author

**Piyush Sharma**  
[GitHub](https://github.com/piyush0920) · [Portfolio](https://piyush0920.github.io/) · [LinkedIn](https://linkedin.com/in/piyush-sharma-6591171ba)
