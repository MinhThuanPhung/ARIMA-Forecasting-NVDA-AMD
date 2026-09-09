# ARIMA Stock Price Forecasting: NVIDIA and AMD

Time series forecasting of NVDA and AMD closing prices using ARIMA, with full 
stationarity diagnostics, model selection, and out of sample validation.

## Overview

This project tests whether short term technical forecasting adds real 
predictive value for two high volatility tech stocks. It builds ARIMA models 
from first principles: confirming non stationarity, applying the correct 
transformation, testing multiple candidate specifications, and validating the 
selected model against held out data rather than just in sample fit.

## Data

Daily closing prices for NVDA and AMD, retrieved via GOOGLEFINANCE, 
2 January 2026 to 20 July 2026.

## Methodology

1. Established non stationarity in both raw series through slow decaying ACF 
   (NVDA from 0.947 to 0.508, AMD from 0.983 to 0.711 across 16 lags) and a 
   significant Box Ljung statistic at all 16 lags (p < .001)
2. Applied first differencing (d=1), with AMD additionally log transformed to 
   stabilise variance
3. Identified candidate p and q values from PACF/ACF of the differenced series
4. Estimated three ARIMA specifications per stock (NVDA: (0,1,0), (1,1,0), 
   (1,1,1); AMD: (0,1,0), (1,1,0), (2,1,0)) rather than relying on ACF/PACF 
   alone
5. Selected the best model by normalised BIC and checked residuals for white 
   noise
6. Validated the selected model with a rolling out of sample forecast

## Key Findings

<img width="975" height="605" alt="image" src="https://github.com/user-attachments/assets/64fa91c0-1f73-488c-9145-87c1d6c24ec7" />


1. Best fitting model for both stocks was ARIMA(0,1,0), the lowest BIC in each 
   case (NVDA: 3.157), and no richer AR/MA term survived scrutiny once the 
   near unit root behaviour was accounted for (e.g. AR(1)=.932, MA(1)=.999 in 
   the alternative NVDA model)
2. Residual diagnostics confirmed white noise for both selected models 
   (Ljung Box failed to reject the null at lag 18)
3. The constant (drift) term was non significant for both stocks in every 
   specification tested; neither stock has a reliable average daily drift
4. The 20 day ahead forecast for NVDA moved from $203.39 to $205.42 with a 
   widening confidence interval; the AMD forecast likewise carried increasing 
   uncertainty over the horizon
<img width="975" height="303" alt="image" src="https://github.com/user-attachments/assets/5ab14ce8-7e82-4354-b23c-4d7dfa045e6e" />


5. Rolling out of sample validation (re estimating on the first 116 
   observations, forecasting the last 20) gave MAE = $10.93 for NVDA and 
   $53.85 for AMD

## Conclusion

Both stocks reduce to a pure random walk once differenced. Since drift is 
statistically zero, point forecasts are simply today's price held flat; the 
models carry no directional trading signal and are best understood as a 
baseline/risk band tool rather than a forecasting edge.

## Tools & Technologies

SPSS, Google Sheets (GOOGLEFINANCE), ARIMA time series modeling

## Skills Demonstrated

1. Stationarity testing and differencing (ACF, PACF, Box Ljung)
2. ARIMA model specification and comparison across multiple candidates
3. Model selection using normalised BIC rather than fit alone
4. Residual diagnostics for white noise
5. Out of sample forecast validation (MAE)
6. Honest interpretation of a model's limits rather than overstating forecast value

## Files

Full report: [report/ARIMA_Forecasting_Report.docx](report/ARIMA_Forecasting_Report.docx)
