# GARCH-Volatility-Forecasting-S-P500-FTSE100
Modelling S&P and FTSE using GARCH family!

---

## Project Workflow

### 1. Data Collection
- Daily price data for SPX and FTSE 100 retrieved from **Stooq**.  
- Sample period: 2015-01-01 to present.  
- Adjusted close prices extracted for analysis.  

### 2. Data Transformation
- Prices converted into **log returns** in percentage terms:  

  r_t = 100 * log(P_t / P_{t-1})

- Returns series prepared for modeling.  

### 3. Exploratory Analysis
- Plotted **returns** and **squared returns** to inspect volatility clustering.  
- Conducted **ARCH LM tests** → strong ARCH effects detected.  
- Plotted **ACF of returns and squared returns**:  
  - Returns: little to no autocorrelation.  
  - Squared returns: strong persistence, confirming volatility clustering.  

### 4. Model Estimation
- **GARCH(1,1)-t** estimated for SPX and FTSE:  
  - High persistence (α + β ≈ 0.99).  
  - Fat tails captured by Student-t degrees of freedom (ν ≈ 6–9).  
  - Small but significant mean returns.  
- **EGARCH(1,1)-t** estimated:  
  - Significant negative γ → leverage effect (negative shocks increase volatility more than positive shocks).  
  - Captures asymmetric volatility dynamics.  

### 5. Parameter Interpretation
- **α (shock response):** sensitivity of volatility to new shocks.  
- **β (persistence):** long memory of volatility.  
- **α + β:** overall persistence.  
- **γ (leverage term, EGARCH):** asymmetry of volatility response.  
- **ν (degrees of freedom):** tail thickness relative to normal distribution.  

### 6. Rolling Forecasting
- Implemented **rolling window estimation** (1500 days):  
  - Refit GARCH model at each step.  
  - Produced **one-step-ahead conditional volatility forecasts**.  
- Realized volatility proxied by absolute daily returns.  

### 7. Forecast Evaluation
- Plotted results in three panels:  
  1. **Forecasted vs realized volatility** (forecasts track overall patterns, smoother than realized).  
  2. **Forecast errors** (errors cluster, especially in crisis periods).  
  3. **Actual returns** (volatility spikes align with large return shocks).  

### 8. Key Findings
- Both SPX and FTSE exhibit **persistent, clustered, and fat-tailed volatility**.  
- EGARCH improves on GARCH by capturing **asymmetric (leverage) effects**.  
- Rolling forecasts provide valuable forward-looking risk measures, though they lag sudden spikes.  
