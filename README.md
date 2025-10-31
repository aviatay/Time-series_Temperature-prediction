# 🌤️ Time Series Forecasting of Weekly Temperature in Nashik (1980–2024)

---

## 🧠 Overview

This project analyzes and forecasts **weekly average temperature** in Nashik, India, using historical hourly weather data collected from **1980–2024**.
The goal is to evaluate and compare the predictive performance of three time series models:

* **SARIMA**
* **Exponential Smoothing (Holt–Winters)**
* **Prophet**

Each model was tested **with and without an external regressor** (Vapor Pressure Deficit).

---

## 🎯 Objectives

1. Forecast weekly temperature averages from long-term hourly data.
2. Detect **annual seasonality** and **long-term trends** in temperature.
3. Compare model performance based on **RMSE** and **MAE**.
4. Explore the effect of adding an external explanatory variable on forecasting accuracy.
5. Identify **anomalies** and **climate irregularities** using control chart analysis.

---

## 🧩 Dataset

**Source:**

* Hourly weather observations for Nashik (India) from **Kaggle (1980–2024)**.
* Converted into **daily** and **weekly averages** to reduce noise and improve interpretability.

**Variables:**

* Temperature 🌡️
* Humidity 💧
* Dew point 🌫️
* Precipitation 🌧️
* Atmospheric pressure ⏱️
* Cloud cover ☁️
* **Vapor Pressure Deficit** (external regressor)
* Wind speed & direction 🌬️

**Weekly Aggregation:**
The original 389,496 hourly records were reduced to **2,319 weekly records**, allowing seasonal modeling at a frequency of **52 (weeks per year)**.

---

## 🔍 Exploratory Analysis

### Seasonal Decomposition

* **Trend:** Gradual increase from early 2000s (~23.5°C → 25°C).
* **Seasonality:** Strong annual cycle (~8°C amplitude).
* **Residuals:** Randomly distributed around 0 with few outliers.

### Monthly Patterns

* Temperature peaks: **March–May**
* Temperature troughs: **December–January**
* Outliers indicate **rare climatic events** (e.g., storms, heavy rainfall).

---

## ⚙️ Methodology

### Models Used

| Model                                    | Description                                 | Seasonal Handling | External Variable Support |
| ---------------------------------------- | ------------------------------------------- | ----------------- | ------------------------- |
| **SARIMA**                               | Seasonal ARIMA with annual frequency        | Yes               | Yes                       |
| **Exponential Smoothing (Holt–Winters)** | Additive trend + additive seasonality       | Yes               | ❌                         |
| **Prophet**                              | Trend + yearly seasonality + event handling | Yes               | Yes                       |

### Model Selection

* ACF/PACF analysis indicated an **AR(1)** process with **annual seasonality (52 lags)**.
* Best SARIMA configuration chosen based on **lowest AIC/BIC**.
* Prophet and Holt–Winters models configured for **yearly frequency**.

### Training & Testing

* Data split: **80% train**, **20% test**.
* Evaluated using:

  * **RMSE** — Root Mean Squared Error
  * **MAE** — Mean Absolute Error

---

## 📈 Results Summary

### 🔹 Without External Regressor

| Model                 | RMSE     | MAE      | Performance       |
| --------------------- | -------- | -------- | ----------------- |
| SARIMA                | 2.16     | 1.67     | Moderate accuracy |
| Exponential Smoothing | 1.80     | 1.35     | Improved accuracy |
| **Prophet**           | **1.32** | **1.06** | 🏆 Best performer |

📊 *Prophet outperformed SARIMA by ~40% (RMSE) and ~37% (MAE).*

---

### 🔹 With External Regressor (Vapor Pressure Deficit)

| Model                 | RMSE              | MAE               | Δ Improvement            |
| --------------------- | ----------------- | ----------------- | ------------------------ |
| SARIMA                | 1.45 *(↓33%)*     | 1.14 *(↓32%)*     | Significant improvement  |
| Exponential Smoothing | 1.80 *(–)*        | 1.35 *(–)*        | No change (unsupported)  |
| **Prophet**           | **0.67 *(↓50%)*** | **0.90 *(↓15%)*** | 🏆 Strongest improvement |

📈 Prophet achieved **~54% lower RMSE** and **~21% lower MAE** compared to SARIMA, confirming that incorporating the external regressor greatly enhanced forecasting accuracy.

---

## 🚨 Anomaly Detection — Shewhart Control Chart

* Model residuals mostly within ±3σ → system is **statistically stable**.
* Two anomalies detected:

  * **Jan 2022:** Unexplained temperature drop (no records found).
  * **Mar 2023:** Confirmed **heavy rainfall event** — highest in 8 years ([Times of India, 2023](https://timesofindia.indiatimes.com/city/nashik/nashik-rainfall-in-march-highest-for-month-in-8-years/articleshow/99234263.cms)).

---

## 💬 Key Insights

* **Prophet** is the most accurate model for this dataset, especially with external regressors.
* **SARIMA** benefits from external variables but remains less flexible.
* **Exponential Smoothing** performs well for internal seasonal structure only.
* **External regressors** can significantly improve forecast accuracy when strongly correlated (r=0.57).
* **Shewhart analysis** effectively detects rare climatic anomalies.

---

## 🧭 Key Takeaways

> **Prophet** demonstrated the highest forecasting precision (RMSE ↓54%, MAE ↓15%) when incorporating the **Vapor Pressure Deficit** as an external regressor.
> These findings highlight Prophet’s robustness for **long-term seasonal forecasting** and its ability to capture **climatic anomalies** for predictive early-warning systems.
