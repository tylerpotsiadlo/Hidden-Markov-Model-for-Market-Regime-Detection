# Hidden Markov Model Classification for Equity Regime Detection
This project implements a regime classification framework for equity markets using a Gaussian Hidden Markov Model.
The goal is to identify distinct market regimes (e.g., rebound, bear/crash prone, expansion) and design regime-specific portfolio allocations.


---

## Table of Contents
- [Overview](#overview)
- [Gaussian Hidden Markov Model](#gaussian-hidden-markov-model)
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
- Identifies historical market regimes using a Gaussian Hidden Markov Model on market/technical features.  
- Profiles each regime based on return distributions, volatility, and technical signals.  
- Backtests simple regime-aware allocation rules (e.g., shift to cash in crash-prone regime).  
- Evaluates performance metrics such as Sharpe ratio, drawdowns, alpha, and beta relative to the S&P 500.
- Trains on interval from 1994-2015 and evaluates on backtest from 2016-2025.

---

## Gaussian Hidden Markov Model
- A **Hidden Markov Model (HMM)** is a statistical/machine learning model that describes how systems evolve over time when the underlying state is not directly observable (it is "hidden") but must be inferred from observable data. I use a **Gaussian HMM** which assumes the observed data for each hidden state follows a multivariable Gaussian distribution.
1. **Key Ideas**
   - **Hidden States (my Regimes):** The market can be in different unobserved (you can't see them directly just by looking at S&P closing prices) regimes (rebound, bear, expansion). Each state has its own probability distribution governing returns and volatility.
   - **Transition Probabilities:** The likelihood of moving from one regime to another is modeled with a transition matrix, which captures persistence or switching between states.
   - **Gaussian Emissions:** For each hidden state, returns are modeled as coming from a Gaussian distribution.
   - **Training:** Given a sequence of observed returns and volatility, the HMM uses the Baum-Welch algorithm to find the transition matrix.
   - **Inference:** With the transition matrix from the Baum-Welch algorithm, the HMM then uses the Viterbi algorithm to find the most likely sequence, and from this we get our regimes. The transition matrix found from the training data is applied to the testing data to prevent overfitting.
   
2. Why did I use this model for equity markets?
   - Financial markets often exhibit regime-switching behavior where return distributions switch over time. A Gaussian HMM is fit to capture these dynamics and classify them into discrete regimes.

---

## Methodology
1. **Feature Engineering**  
   - Technical indicators (e.g., RSI, moving averages).  
   - Market returns and volatility estimates.
   - Settled on a feature set of past week return, past month return, VIX (volatility index), Price-to-200-day moving average, 20-day exponential moving average of Relative Strength Index, and Price-to-20-day exponential moving average. 

2. **Classification**  
   - Gaussian HMM applied to standardized features.  
   - Each state represents a distinct regime.

3. **Regime Profiling**  
   - Compute average feature values and frequency of each regime.  
   - Visualize regimes over time relative to the S&P 500.
   - Regimes named based on their profiles (e.g. "steady expansion" characterized by relatively low volatility and positive returns).

4. **Backtesting**  
   - Map each regime to a portfolio allocation (`SPY`, `BIL`, `MTUM`,`SPUU`,`SH`,`SPXU`).  
   - Compute performance metrics including CAGR, Sharpe, Calmar, and alpha/beta.  

---

## Data
- **S&P 500 Index (SP500)**: Benchmark returns.  
- **Treasury Yield (WGS3MO, FRED)**: Used to estimate the risk-free rate.  
- **ETFs**: Price data for SPY, BIL, MTUM, SPUU, SH, SPXU.

---

## Project Structure

---

## Usage
- Use this link to access the notebook: [![Launch Binder](https://mybinder.org/badge_logo.svg)](https://hub.gesis.mybinder.org/user/tylerpotsiadlo--egime-detection-fbvs9d55/doc/workspaces/auto-P/tree/RegimeProject.ipynb)

