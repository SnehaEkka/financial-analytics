# Predicting Stock Trading Volume Using Time-Series Data

This project builds predictive models for the daily trading volume of Stock 1 (VolStock1(t)) using historical trading data and related features. It focuses on leveraging time-series features and relevant explanatory variables to forecast trading volumes accurately. The aim is to minimize out-of-sample prediction errors, providing a robust approach to modeling stock market volume fluctuations.

## Tools Used
- Python (pandas, numpy, statsmodels, sklearn, pmdarima)
- Jupyter/Colab Notebook for iterative modeling and documentation

## Dataset Overview

- **Source:** Provided dataset `assign2data.csv` contains 2+ years of daily trading observations.
- **Key Variables:**
  - **VolStock1(t):** Daily trading volume for Stock 1 (target variable)
  - **EADay, EADayBefore, EADayAfter:** Binary flags indicating earnings announcement days and the days surrounding them
  - **DayOfWeek:** Categorical variable indicating the day of the week (Monday to Friday)
  - **Month:** Categorical variable indicating the month of the year
  - **Lagged Trading Volumes:** VolStock1(t-1), VolStock2(t-1), ..., VolStock6(t-1): Previous day's volumes for Stock 1 and 5 related stocks
  
---

## Methodology & Analysis

### Data Preparation
- Examined `EADay`, `EADayBefore`, and `EADayAfter` as important binary indicators linked to trading volume spikes.
- Used lagged values of Stock 1 and related stocks as autoregressive and explanatory features.
- Computed moving averages (EMAs) to smooth short-term fluctuations.

### Models Evaluated

1. **Basic Model (OLS):**  
   Features: `EADay`, `VolStock1(t-1)`  
   Performance: R² ≈ 0.40  
   Insight: Reasonable baseline, capturing earnings announcements and own lagged volume.

2. **Basic Model 2 (Extended Earnings Days):**  
   Features: `EADay`, `EADayBefore`, `EADayAfter`, `VolStock1(t-1)`  
   Performance: R² ≈ 0.196 (lower than Basic Model)  
   Insight: Including days before and after earnings alone did not improve fit.

3. **Comprehensive OLS Model:**  
   Features: `EADay`, `EADayBefore`, `EADayAfter`, Day of Week dummies, Month dummies, moving averages EMA_2 to EMA_6, and lagged volumes of Stock 1 and related stocks (Stock2 to Stock6).  
   Performance: R² ≈ 0.496  
   Insight: Incorporating more features related to calendar effects, earnings day surroundings, and industry peers markedly improves explanatory power.

4. **Reduced OLS Model:**  
   Reduced feature set, maintaining the most important variables.  
   Performance: R² ≈ 0.482  
   Insight: Similar performance with fewer variables, indicating some redundancy in the full model.

### ARIMA Model
- Conducted stationarity tests (ADF test), confirming data stationarity.
- Used automated parameter selection to identify optimal ARIMA orders.
- Model focused solely on past values of VolStock1.
- Performance: Validation MSE ≈ 2.02  
- Insight: A Classic time-series model without external regressors yielded limited accuracy.

### ARIMAX Model (ARIMA with Exogenous Variables)
- Extended ARIMA by adding explanatory variables like earnings days, day of week, month, and lagged volumes of other stocks.
- Captured seasonality and cross-stock influences.
- Performance: Validation MSE ≈ 1.13 (much improved)  
- Insight: Integrating explanatory variables alongside autoregressive terms vastly improves prediction accuracy.

## Key Findings & Conclusion

- Earnings announcement day (EADay) and own previous day’s volume are strong individual predictors.
- Including days before and after earnings alone is not sufficient; a broader context is necessary.
- Calendar effects (Day of Week, Month) and trading volume of related stocks add valuable predictive information.
- ARIMA models alone underperform compared to models augmented with explanatory variables.
- The ARIMAX model, combining autoregressive, seasonal, and exogenous inputs, delivers the best predictive accuracy.
- This demonstrates the importance of including industry peer dynamics and calendar/seasonal features in trading volume forecasting.

## Business Impact & Interpretation

- Accurate trading volume prediction can inform trading strategies and risk management.
- Earnings announcement days and the near surrounding periods warrant particular attention for volume spikes.
- Integrating market and seasonal context leads to more robust volume forecasts.
- Insights from model variables can help trading desks anticipate liquidity and volatility patterns.

## Learning & Takeaways

- Time-series forecasting benefits greatly from combining autoregressive terms with domain-specific event variables.
- Feature engineering for finance includes incorporating earnings announcement timings, trading peers, and calendar effects.
- Evaluation based on out-of-sample MSE is critical to selecting the best model.
- ARIMAX is a flexible framework to merge time series dynamics and explanatory variables for improved predictions.

## Project Details

- **Completed:** Spring 2024
- **Course:** BA870/AC820 Financial Analytics, Boston University MSBA

*This README summarizes the predictive modeling approach to stock trading volume using time-series data, highlighting model development steps, key results, and practical relevance for financial analytics and trading strategy optimization.*
