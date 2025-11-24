## Vehicle Demand Forecasting & Inventory Risk Report

## Project Overview
This project performs a time-series analysis on global BMW sales records to **forecast future vehicle demand** and generate an **Inventory Risk Report**. The primary goal is to provide a data-driven recommendation on potential inventory shortages or surpluses against a planned stocking level.

* **Dataset:** BMW Worldwide Sales Records (2010–2024, Annual Aggregation).
* **Methodology:** Time-Series Analysis using the **ARIMA** (Autoregressive Integrated Moving Average) model.
* **Tool:** Python (Pandas, Statsmodels, Matplotlib) executed in a Google Colab environment.

---

## Methodology and Analysis

### 1. Data Preparation
The raw data, which consisted of 50,000 individual sales records, was aggregated by year to create a single **Annual Total Sales Volume** time series, indexed from 2010 to 2024.

### 2. Model Selection (ARIMA)
* **Stationarity Test:** The Augmented Dickey-Fuller (ADF) test revealed a **p-value of 0.457**, indicating the data was **non-stationary**. This required one order of differencing ($d=1$).
* **Parameter Refinement:** Initial fitting of ARIMA(1, 1, 1) showed statistically insignificant Autoregressive ($p=1$) and Moving Average ($q=1$) components.
* **Final Model:** The model was simplified to the **ARIMA(0, 1, 0)**, which is equivalent to a **Random Walk with Drift**. This model was selected due to its **lower AIC (419.516)** and increased stability compared to the initial model.

### 3. Forecasting Results (2025-2027)
The model forecasted demand based on the last observed sales value (2024) plus the historical average change (drift), which was near zero due to the data's volatility.

| Year | Forecasted Sales | Planned Inventory (17.2M) | Inventory Gap | Risk Assessment |
| :--- | :--- | :--- | :--- | :--- |
| 2025 | 17,527,854 | 17,200,000 | +327,854 | Shortage Risk |
| 2026 | 17,527,854 | 17,200,000 | +327,854 | Shortage Risk |
| 2027 | 17,527,854 | 17,200,000 | +327,854 | Shortage Risk |

---

## Key Findings and Business Implications

### 1. Persistent Shortage Risk
The baseline forecast indicates a consistent **Shortage Risk** of approximately **327,854 units** annually against the planned inventory level of 17.2 million units. Management should consider increasing production or adjusting inventory targets upward.

### 2. High Volatility and Uncertainty
The most critical finding is the **rapidly widening 95% Confidence Interval (CI)**, indicating high volatility and uncertainty in demand forecasting:
* **Maximum Potential Shortage (2027, Upper CI):** $\approx 19.89$ million units, leading to a shortage of **2.7 million units**.
* **Maximum Potential Surplus (2027, Lower CI):** $\approx 15.15$ million units, leading to a surplus of **2.04 million units**.

This wide range suggests that while the central forecast is slightly high, the historical data contains significant, unmodeled volatility (likely due to economic cycles or external factors not captured by ARIMA).

## Visualization: Demand Forecast & Inventory Risk

The plot below illustrates the historical sales, the flat forecast, the planned inventory, and the high uncertainty band.

That's a great idea! Adding a specific description for the visualization ensures that anyone looking at your GitHub repository immediately understands the key takeaways from the chart without having to read the entire report.

Here is a concise, analytical description you can place right before the image in your `README.md` file:

---

## 🖼️ Visualization: Demand Forecast & Inventory Risk Description
The plot below illustrates the historical sales, the flat forecast, the planned inventory, and the high uncertainty band.

* **Historical Data (Blue Line):** Shows the global annual BMW sales volume from 2010 to 2024, highlighting the overall **volatility** but relative stationarity (mean remains stable).
* **Planned Inventory (Red Line):** Represents the management's target of **17,200,000 units** annually, serving as the benchmark for risk assessment.
* **Forecast (Orange Dashed Line):** The $\text{ARIMA}(0, 1, 0)$ forecast for 2025–2027 predicts a static demand of **$17,527,854$ units**, indicating a **base Shortage Risk**.
* **95% Confidence Interval (Shaded Orange Area):** This area represents the model's uncertainty. It clearly demonstrates the most critical finding: the band **widens dramatically** in future years, quantifying the substantial **inventory volatility risk** (potential shortage up to 2.7M units or surplus up to 2.04M units) inherent in the current sales pattern.


---

## How to Run the Code

The analysis is contained entirely within the **`Vehicle_Demand_Forecasting.ipynb`** Jupyter Notebook.

1.  **Open the Notebook:** Open the file in Google Colab or a local Jupyter environment.
2.  **Run Cells:** Run all cells sequentially. The code will load the data, process the time series, fit the ARIMA model, and generate the final report and plot.
