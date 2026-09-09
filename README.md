# ARIMA Stock Forecasting & Behavioural Drivers of Investment Decisions

Two-part quantitative research project: (1) ARIMA time-series forecasting of 
NVIDIA and AMD stock prices, and (2) a structural equation model (SEM) testing 
which behavioural biases actually drive investment decisions.

## Overview

This project combines two distinct analytical techniques on financial 
decision-making. Element 1 builds and validates ARIMA models to forecast NVDA 
and AMD closing prices and tests whether short-term technical forecasting adds 
real predictive value. Element 2 uses survey data and SEM (via AMOS) to test 
which behavioural finance constructs — Overconfidence, Social Influence, 
Herding Behaviour, Emotional State — actually predict investment decisions, 
after first validating the measurement model through reliability testing, EFA, 
and CFA.

## Element 1: ARIMA Forecasting of NVIDIA and AMD

**Data:** Daily closing prices for NVDA and AMD, retrieved via GOOGLEFINANCE, 
2 January 2026 – 20 July 2026.

**Approach**
- Confirmed non-stationarity in both raw series (slow-decaying ACF; NVDA from 
  0.947 to 0.508, AMD from 0.983 to 0.711 across 16 lags, Box-Ljung p < .001 
  at all lags)
- Applied first differencing (d=1), with AMD additionally log-transformed to 
  stabilise variance
- Tested three ARIMA specifications per stock (NVDA: (0,1,0), (1,1,0), (1,1,1); 
  AMD: (0,1,0), (1,1,0), (2,1,0)) and selected the best fit by normalised BIC

**Key Findings**
![Forecast](assets/figures/fig10_forecast_20day.png)
- Best-fitting model for both stocks: **ARIMA(0,1,0)** — lowest BIC in each 
  case (NVDA: 3.157), and no richer AR/MA term survived scrutiny once the 
  boundary/near-unit-root behaviour was accounted for (e.g. AR(1)=.932, 
  MA(1)=.999 in the alternative NVDA model)
- Residual diagnostics confirmed white noise for both selected models 
  (Ljung-Box failed to reject the null at lag 18)
- The constant (drift) term was non-significant for both stocks in every 
  specification tested — neither stock has a reliable average daily drift
- 20-day-ahead forecasts: NVDA moved from $203.39 to $205.42 with a widening 
  confidence interval; AMD forecast likewise carried increasing uncertainty 
  over the horizon
- Out-of-sample validation (rolling re-estimation on the first 116 
  observations, forecasting the last 20): **MAE = $10.93 for NVDA, $53.85 
  for AMD**

**Conclusion:** Both stocks reduce to a pure random walk once differenced. 
Since drift is statistically zero, point forecasts are simply "today's price 
held flat" — the models carry no directional trading signal and are best 
understood as a baseline/risk-band tool rather than a forecasting edge.

## Element 2: Behavioural Drivers of Investment Decisions (SEM)

**Approach**
- Reliability: Cronbach's Alpha computed for five constructs (Overconfidence, 
  Social Influence, Herding Behaviour, Emotional State, Investment Decision) — 
  all exceeded the 0.70 threshold after item refinement (Overconfidence 
  improved from α = .705 to .713 after removing item OC3)
- EFA run iteratively as weak items were removed: final 19-item, 5-factor 
  solution — KMO = .749, Bartlett's χ² = 1030.55 (df = 171, p < .001)
- CFA identified OC4 as structurally unsound (lowest squared multiple 
  correlation = .285 vs. .453/.747 for OC1/OC2; largest modification index), 
  and it was removed, leaving Overconfidence as a 2-indicator construct
- Path analysis (SEM/AMOS) tested the structural model of all four 
  behavioural constructs predicting Investment Decision

**Key Findings**
![AMOS path diagram](assets/figures/fig12_amos_path_diagram.png)
- **Emotional State** is the strongest driver of investment decisions 
  (β = .466, p = .007)
- **Overconfidence** became significant once OC4 was removed (β = .436, 
  p = .004) — reversing its earlier non-significant status in the initial 
  model specification
- **Herding Behaviour** and **Social Influence** were both non-significant, 
  consistent with prior literature finding no measurable peer effect on 
  financial decisions (Lieber & Skimmyhorn, 2018)
- Together, Emotional State and Overconfidence explain **40.3%** of the 
  variance in Investment Decision
- Model fit: CMIN/df = 2.153 (acceptable, < 3), CFI = .828, GFI = .777, 
  AGFI = .697, RMSEA = .108 — fit is moderate, with CFI/GFI below the 
  conventional 0.90 threshold, a limitation worth flagging rather than 
  glossing over

**Conclusion:** Investment decisions are driven more by affective/emotional 
response to market movements and by overconfidence bias than by social or 
herd dynamics — a finding with direct implications for how investor education 
and robo-advisory nudges should be designed (targeting emotional regulation 
and overconfidence, not social-proof messaging).

## Tools & Technologies

SPSS · AMOS (SEM/CFA/Path Analysis) · Google Sheets (GOOGLEFINANCE) · ARIMA time-series modeling

## Skills Demonstrated

- Time-series stationarity testing, differencing, and ARIMA model selection (BIC, residual diagnostics)
- Out-of-sample forecast validation (MAE)
- Scale reliability testing (Cronbach's Alpha) and iterative EFA/CFA refinement
- Structural equation modeling and path analysis
- Critical interpretation of model fit limitations rather than overstating results

## Repository Structure
