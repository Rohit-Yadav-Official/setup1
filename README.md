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

**Formula**:
