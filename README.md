# ARIMA Stock Forecasting & Behavioural Drivers of Investment Decisions

Two part quantitative research project: (1) ARIMA time series forecasting of 
NVIDIA and AMD stock prices, and (2) a structural equation model (SEM) testing 
which behavioural biases actually drive investment decisions.

## Overview

This project combines two distinct analytical techniques on financial 
decision making. Element 1 builds and validates ARIMA models to forecast NVDA 
and AMD closing prices and tests whether short term technical forecasting adds 
real predictive value. Element 2 uses survey data and SEM (via AMOS) to test 
which behavioural finance constructs, Overconfidence, Social Influence, 
Herding Behaviour, and Emotional State, actually predict investment decisions, 
after first validating the measurement model through reliability testing, EFA, 
and CFA.

## Element 1: ARIMA Forecasting of NVIDIA and AMD

Data: Daily closing prices for NVDA and AMD, retrieved via GOOGLEFINANCE, 
2 January 2026 to 20 July 2026.

Approach

1. Confirmed non stationarity in both raw series (slow decaying ACF; NVDA from 
   0.947 to 0.508, AMD from 0.983 to 0.711 across 16 lags, Box Ljung p < .001 
   at all lags)
2. Applied first differencing (d=1), with AMD additionally log transformed to 
   stabilise variance
3. Tested three ARIMA specifications per stock (NVDA: (0,1,0), (1,1,0), (1,1,1); 
   AMD: (0,1,0), (1,1,0), (2,1,0)) and selected the best fit by normalised BIC

Key Findings

![Forecast](assets/figures/fig10_forecast_20day.png)

1. Best fitting model for both stocks was ARIMA(0,1,0), the lowest BIC in each 
   case (NVDA: 3.157), and no richer AR/MA term survived scrutiny once the 
   boundary/near unit root behaviour was accounted for (e.g. AR(1)=.932, 
   MA(1)=.999 in the alternative NVDA model)
2. Residual diagnostics confirmed white noise for both selected models 
   (Ljung Box failed to reject the null at lag 18)
3. The constant (drift) term was non significant for both stocks in every 
   specification tested; neither stock has a reliable average daily drift
4. The 20 day ahead forecast for NVDA moved from $203.39 to $205.42 with a 
   widening confidence interval; the AMD forecast likewise carried increasing 
   uncertainty over the horizon
5. Out of sample validation (rolling re estimation on the first 116 
   observations, forecasting the last 20) gave MAE = $10.93 for NVDA and 
   $53.85 for AMD

Conclusion: Both stocks reduce to a pure random walk once differenced. Since 
drift is statistically zero, point forecasts are simply today's price held 
flat; the models carry no directional trading signal and are best understood 
as a baseline/risk band tool rather than a forecasting edge.

## Element 2: Behavioural Drivers of Investment Decisions (SEM)

Approach

1. Reliability: Cronbach's Alpha computed for five constructs (Overconfidence, 
   Social Influence, Herding Behaviour, Emotional State, Investment Decision); 
   all exceeded the 0.70 threshold after item refinement (Overconfidence 
   improved from α = .705 to .713 after removing item OC3)
2. EFA run iteratively as weak items were removed, ending in a final 19 item, 
   5 factor solution (KMO
