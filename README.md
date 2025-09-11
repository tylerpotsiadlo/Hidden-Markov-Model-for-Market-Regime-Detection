# Hidden-Markov-Model-for-Market-Regime-Detection
Classifies market regime with Gaussian Hidden Markov Model based on S&amp;P500 closing prices since 1994 (test since 2016). Achieves superior Sharpe ratio &amp; alpha with various portfolio allocation mappings.

# Regime Classification for Equity Markets

This project implements a regime classification framework for equity markets using unsupervised learning and performance analysis.  
The goal is to identify distinct market regimes (e.g., bear, rebound, expansion) and design regime-specific portfolio allocations.

---

## Table of Contents
- [Overview](#overview)
- [Methodology](#methodology)
- [Data](#data)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [Results](#results)
- [Key Functions](#key-functions)
- [Next Steps](#next-steps)
- [References](#references)

---

## Overview
- Identifies historical market regimes using clustering on market/technical features.  
- Profiles each regime based on return distributions, volatility, and technical signals.  
- Backtests simple regime-aware allocation rules (e.g., shift to cash in crash-prone regimes).  
- Evaluates performance metrics such as Sharpe ratio, drawdowns, alpha, and beta relative to the S&P 500.

---

## Methodology
1. **Feature Engineering**  
   - Technical indicators (e.g., RSI, moving averages).  
   - Market returns and volatility estimates.  

2. **Clustering**  
   - KMeans applied to standardized features.  
   - Each cluster represents a distinct regime.  

3. **Regime Profiling**  
   - Compute average feature values and frequency of each regime.  
   - Visualize regimes over time relative to the S&P 500.  

4. **Backtesting**  
   - Map each regime to a portfolio allocation (`SPY`, `BIL`, `MTUM`).  
   - Compute performance metrics including CAGR, Sharpe, Calmar, and alpha/beta.  

---

## Data
- **S&P 500 Index (SP500)**: Benchmark returns.  
- **Treasury Yield (WGS3MO, FRED)**: Used to estimate the risk-free rate.  
- **Yahoo Finance / Other APIs**: Price data for SPY, MTUM, and BIL.  

---

## Project Structure
