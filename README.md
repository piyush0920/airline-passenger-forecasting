# ✈️ Airline Passenger Demand Forecasting

A comprehensive time series analysis project applying **13 forecasting models** to real-world airline passenger data, with the goal of optimising resource planning and demand management.

---

## 📌 Problem Statement

An airline company has collected monthly passenger count data over several years and wants to **forecast future passenger counts** to effectively plan budgeting, staffing, and operational resources.

> Given historical monthly passenger data (1949–1960), build and evaluate multiple time series models to forecast future demand.

---

## 📂 Dataset

| Attribute | Description |
|---|---|
| `Month` | Month of observation (yyyy-mm format) |
| `Passengers` | Number of air passengers recorded that month |

- **Source:** Classic AirPassengers dataset
- **Period:** January 1949 – December 1960
- **Frequency:** Monthly (144 observations)
- **Train/Test Split:** 120 months training | 24 months testing

---

## 🧪 Models Implemented

### Simple / Baseline Models
| Model | Description |
|---|---|
| Naive | Uses the last observed value as the forecast |
| Simple Average | Mean of all training observations |
| Simple Moving Average | Rolling mean over a fixed window |
| Linear Regression | Trend-based regression on time index |

### Exponential Smoothing Models
| Model | Description |
|---|---|
| Simple Exponential Smoothing (SES) | Weighted average with single smoothing parameter |
| Holt's Method | Captures level + trend |
| Holt-Winters' Additive | Captures level + trend + additive seasonality |
| Holt-Winters' Multiplicative | Captures level + trend + multiplicative seasonality |

### ARIMA Family Models
| Model | Description |
|---|---|
| AR | Autoregressive model |
| MA | Moving Average model |
| ARMA | Autoregressive Moving Average |
| ARIMA | Autoregressive Integrated Moving Average |
| SARIMA | Seasonal ARIMA with Box-Cox transformation |

---

## 🔬 Methodology

### Data Preparation
- Datetime parsing and chronological sorting
- Train/test split (120/24 months)
- Stationarity assessment via ACF and PACF plots
- Seasonal decomposition (trend, seasonality, residual)

### Feature Engineering & Transformations
- **Box-Cox transformation** applied prior to SARIMA to stabilise variance
- Contextual lag features for ARIMA-family parameter selection
- ACF/PACF analysis used to determine optimal p, d, q parameters

### Final SARIMA Configuration
```
SARIMA(p=7, d=1, q=4)(P=0, D=1, Q=0, m=3)
```
- Non-seasonal differencing order: 1
- Seasonal differencing applied to capture annual patterns
- Box-Cox inverse transformation applied to predictions

### Evaluation Metrics
All models evaluated on the **24-month held-out test set** using:
- **RMSE** — Root Mean Squared Error (penalises large errors)
- **MAPE** — Mean Absolute Percentage Error (interpretable % accuracy)

---

## 📊 Key Findings

- Baseline models (Naive, Simple Average) fail to capture seasonal growth patterns
- Holt-Winters' Multiplicative outperforms additive due to the multiplicative nature of seasonality in airline data
- SARIMA with Box-Cox transformation delivers the best performance by jointly modelling trend, seasonality, and autocorrelation structure
- ACF/PACF analysis was critical in guiding ARIMA parameter selection and confirming stationarity after differencing

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core programming language |
| Pandas / NumPy | Data manipulation and numerical operations |
| Statsmodels | ARIMA, SARIMA, Exponential Smoothing models |
| Scikit-learn | Linear Regression, RMSE computation |
| Matplotlib / Seaborn | Visualisation and model comparison plots |
| SciPy | Box-Cox transformation |

---

## 📁 Repository Structure

```
├── TSA_Graded_Exercise.ipynb   # Main notebook with full analysis
├── AirPassengers.csv           # Dataset
└── README.md                   # Project documentation
```

---

## 🚀 How to Run

```bash
# Clone the repository
git clone https://github.com/piyush0920/airline-passenger-forecasting.git
cd airline-passenger-forecasting

# Install dependencies
pip install pandas numpy matplotlib seaborn statsmodels scikit-learn scipy

# Launch the notebook
jupyter notebook TSA_Graded_Exercise.ipynb
```

---

## 💡 Business Relevance

This project mirrors real-world demand forecasting challenges faced by global companies — including supply chain planning, inventory optimisation, and resource allocation. The systematic model comparison framework (from naive baselines to seasonal ARIMA) demonstrates a rigorous, evidence-based approach to selecting the right forecasting model for a given dataset.

---

## 👤 Author

**Piyush Sharma**
- 📧 piyushsh0920@gmail.com
- 🔗 [LinkedIn](https://linkedin.com/in/piyush-sharma-6591171ba)
- 💻 [GitHub](https://github.com/piyush0920)
