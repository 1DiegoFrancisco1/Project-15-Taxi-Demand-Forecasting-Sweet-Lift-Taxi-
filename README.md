# 🚕 Project 15 — Taxi Demand Forecasting (Sweet Lift Taxi)

### 🏢 Project Context
**Sweet Lift Taxi**, an airport-based taxi service, wants to **predict the number of hourly ride requests** to better allocate drivers during peak hours.  
Your task was to build a **time series forecasting model** to predict the number of taxi orders for the next hour.

The model must achieve an **RMSE ≤ 48** on the test dataset.

---

## 🎯 Project Objectives
1. Load and resample the dataset to hourly intervals.  
2. Analyze temporal patterns — trend, seasonality, and variability.  
3. Create **time-based features** (lags, rolling means).  
4. Train several models with different hyperparameters.  
5. Evaluate their performance and choose the best one.

---

## 🧭 Data Overview
**Dataset:** `/datasets/taxi.csv`  
**Target Variable:** `num_orders` — number of taxi orders per hour.

---

## 📊 Exploratory Analysis

### 1. General Trend
- The number of orders shows a **slight upward trend** over time, particularly during July and August.  
- Starting mid-August, peaks become more frequent and higher — possibly due to holiday season or increased airport traffic.  
- The hourly data shows significant variability, with spikes reaching **over 400 orders per hour**.

### 2. Average Orders by Day of the Week
- Demand increases toward the end of the week.  
- Highest order volumes occur on **Mondays and Fridays**.  
- Lowest activity is on **Sundays**, suggesting the influence of flight schedules and work-week travel patterns.

### 3. Average Orders by Hour of the Day
- A **clear daily pattern** is present:
  - Sharp peak around **midnight (00:00)** — likely tied to late-night or early flights.  
  - Drop between **04:00–07:00**, corresponding to low airport activity.  
  - Gradual increase during the day, with sustained demand between **15:00–23:00**.

🧠 **Conclusion:**  
The time series exhibits both **weekly and daily seasonality**, plus a mild long-term upward trend.  
Time-derived features such as **hour, day of week, lag values, and rolling means** are essential for accurate forecasting.

---

## 🧩 Feature Engineering
Created lag and rolling window features to incorporate temporal dependencies:
- **Lag variables:** `num_orders(t-1)` to `num_orders(t-24)`  
- **Rolling means:** 3-hour and 6-hour moving averages  
- **Temporal features:** hour of day, day of week, weekend flag  

All features were standardized to ensure consistency across models.

---

## ⚙️ Model Training and Evaluation

Three main models were trained to forecast taxi demand for the next hour:

| Model | RMSE (≈ orders/hour) | Training Time (s) | Comment |
|--------|----------------------:|------------------:|----------|
| **Linear Regression** | 45.78 | 5.45 | Meets requirement (RMSE < 48), but limited with nonlinear patterns. |
| **Random Forest** | 43.41 | 5.45 | Better handling of nonlinearity; improved stability. |
| **Gradient Boosting** | **41.50** | 5.45 | ✅ Best performance — lowest RMSE and most consistent results. |

---

## 📈 Model Interpretation

- **Linear Regression**: Fast and reliable benchmark; captures trend but not seasonality effectively.  
- **Random Forest**: Handles complex interactions, improving accuracy.  
- **Gradient Boosting**: Outperforms all — models subtle temporal dependencies with minimal error.

💡 **Average model error:** ±42 taxi orders per hour.

This level of precision is acceptable, given actual values range between 100–400 orders/hour.

---

## 🧠 Final Conclusions

- The **Gradient Boosting** model achieved an **RMSE = 41.5**, comfortably below the 48-threshold.  
- It successfully follows the real demand curve, even across different weeks and peak periods.  
- The model **accurately captures daily and weekly fluctuations** in taxi demand.  
- Deviations mainly occur during extreme peaks — common in real-world time series.

📊 **Interpretation:**  
> The model’s predictions are stable and reliable enough for real-time operational use.

---

## 🚀 Business Impact
The final model empowers **Sweet Lift Taxi** to:
- **Anticipate demand peaks** and proactively allocate drivers.  
- **Improve customer satisfaction** by reducing waiting times.  
- **Optimize workforce scheduling and resource planning.**  
- **Increase revenue** through dynamic supply management during peak hours.

---

## 🧰 Tools and Libraries
- **Python:** pandas, numpy, scikit-learn  
- **Models:** Linear Regression, Random Forest, Gradient Boosting  
- **Metrics:** RMSE  
- **Visualization:** matplotlib, seaborn  
- **Time Features:** datetime, resampling, rolling windows  

---

## 👨‍💻 Author
**Diego Francisco Domínguez Aguilar**  
Data Science Bootcamp – TripleTen (2025)
