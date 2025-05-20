# 📘 Models & Algorithms Documentation

This system simulates the real-time cost of cryptocurrency trades by calculating slippage, exchange fees, and market impact using market microstructure models.

---

## 1. ✅ Expected Slippage Estimation

**Model Used**: Quantile Regression / Linear Regression  
**Purpose**: Estimate the expected slippage (%) or USD cost when placing a market order.

**Input Parameters**:
- Order quantity (converted to USD)
- Order book depth (from WebSocket)
- Recent price movement (volatility proxy)

**Formula**: Slippage = (Executed Avg Price - Mid Price) / Mid Price × 100


**Method**:
- Simulate order fill across levels based on quantity
- Fit regression model: `slippage = f(order size)`

---

## 2. 💸 Fee Estimation Model

**Model Used**: Rule-based from OKX Fee Tier Table  
**Purpose**: Calculate transaction fees using OKX’s tiered fee structure

**Input Parameters**:
- OKB Holding (user input)
- USD Volume of trade

**Fee Logic**:
- Fetch appropriate tier based on OKB
- Apply respective Maker/Taker rate: Fee = Trade Size × Fee Rate
  
---

## 3. 📉 Market Impact Estimation

**Model Used**: Almgren-Chriss Model  
**Purpose**: Estimate market impact from executing a market order

**Reference**: [Understanding Almgren-Chriss](https://www.linkedin.com/pulse/understanding-almgren-chriss-model-optimal-portfolio-execution-pal-pmeqc/)

**Input Parameters**:
- Order size (Q)
- Volatility (σ)
- Orderbook liquidity

**Core Equation**: Market Impact ≈ η × Q + λ × Q²
Where:
- η = temporary impact coefficient  
- λ = permanent impact coefficient

---

## 4. 🧾 Net Cost Calculation

**Formula**:
Net Cost = Slippage + Fees + Market Impact

**Purpose**: Combine all cost components for a full trade cost estimate.

---

## 5. 🔁 Maker/Taker Probability Estimation

**Model Used**: Logistic Regression  
**Purpose**: Predict whether order will be Maker or Taker

**Input Features**:
- Distance to best bid/ask
- Order size
- Time of submission

**Logistic Function**:P(Taker) = 1 / (1 + e^-(w₀ + w₁x₁ + w₂x₂ + ...))
---

## 6. 🕒 Internal Latency Measurement

**Method**: Timestamp Differencing  
**Purpose**: Measure tick processing time (in ms)

**Logic**:
1. Record time on message receive: `t1`
2. Record time after processing: `t2`
3. Calculate: `latency = t2 - t1`

Used to benchmark system responsiveness.

---

## ℹ️ Notes
- Modular implementation under `/metrics/`
- Volatility may be estimated or hardcoded
- Suitable for future backtesting/simulation



 
