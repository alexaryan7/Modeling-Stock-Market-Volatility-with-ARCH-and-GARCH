# 📈 Modeling Stock Market Volatility with ARCH and GARCH: A Case Study on Apple (AAPL)

## 🔹 Objective  
The goal of this project is to model **volatility clustering** in financial time series using **ARCH** (Autoregressive Conditional Heteroskedasticity) and **GARCH** (Generalized ARCH) models.  
We use **Apple Inc. (AAPL)** daily stock returns to test for volatility clustering, fit ARCH/GARCH models, and compare their performance.  

---

## 🔹 Methodology  

### 1. Stationarity Check (ADF Test)  
We first check whether returns are stationary using the **Augmented Dickey-Fuller (ADF)** test.  

- **ADF Test Statistic**: –15.55  
- **p-value**: 2.1e–28  
- **Critical values**: {1%: –3.43, 5%: –2.86, 10%: –2.56}  

✅ Since the statistic is far below the critical values and p-value ≪ 0.05, the series is **stationary** → suitable for ARCH/GARCH modeling.  

---

### 2. Volatility Clustering Test (ARCH LM Test)  
- **p-value**: ~1.17e–79  

✅ The extremely small p-value rejects homoskedasticity → strong evidence of **ARCH effects** (volatility clustering).  

---

### 3. ARCH(1) Model Results  

- Mean return (μ): **0.135%** per day  
- Volatility equation:  

\[
\sigma_t^2 = \omega + \alpha_1 \epsilon_{t-1}^2
\]

- ω (constant): 2.44  
- α₁ (lagged squared return): 0.244 (**significant**)  

📌 **Interpretation**: About **24% of today’s volatility** is explained by yesterday’s squared return (shock). ARCH captures **short-term shocks** but is too reactive.  

---

### 4. GARCH(1,1) Model Results  

- Volatility equation:  

\[
\sigma_t^2 = \omega + \alpha_1 \epsilon_{t-1}^2 + \beta_1 \sigma_{t-1}^2
\]

- ω: ~0.29  
- α₁: ~0.10  
- β₁: ~0.85  

📌 **Interpretation**:  
- 10% weight on yesterday’s shock  
- 85% weight on past volatility  
- Since α + β ≈ 0.95 < 1 → volatility is **persistent but mean-reverting**.  
- GARCH(1,1) better captures the **long memory of volatility** compared to ARCH(1).  

---

### 5. Visualization  

- **Returns (gray line)** → exhibit spikes during events (e.g., 2020 COVID crash).  
- **ARCH(1) volatility (blue)** → reacts sharply to shocks, jagged.  
- **GARCH(1,1) volatility (orange)** → smoother, persistent, realistic.  

---

## 🔹 Key Takeaways  

1. AAPL returns are **stationary** and exhibit **volatility clustering**.  
2. **ARCH(1)** captures short-term shocks but overreacts.  
3. **GARCH(1,1)** provides a smoother, persistent volatility estimate.  
4. Useful applications:  
   - Portfolio risk management  
   - Option pricing (volatility input)  
   - Value-at-Risk (VaR) estimation  

---

## 🔧 Requirements  

```bash
pip install yfinance arch matplotlib pandas statsmodels

## 📂 Project Structure  

