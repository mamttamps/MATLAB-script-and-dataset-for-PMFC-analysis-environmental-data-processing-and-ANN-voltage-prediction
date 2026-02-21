# PMFC ANN Voltage Prediction (MATLAB + Dataset)

MATLAB script and dataset for PMFC analysis with environmental data and ANN-based voltage prediction.

---

## 🔍 Overview

This repository contains a MATLAB implementation of a multi-output artificial neural network (ANN) for **one-step-ahead (10 min) voltage prediction** in a Plant-Microbial Fuel Cell (PMFC) system.

The model:

- Uses a **feedforward MLP (fitnet)** with architecture **[20 10]** (two hidden layers).
- Predicts the voltage of multiple PMFC units simultaneously (multi-output regression).
- Combines **environmental / temperature inputs** and **autoregressive voltage lags**.
- Generates figures and `.mat` files for quantitative analysis and visualization.

---

## 📁 Repository Contents

Typical structure:

PMFC-ANN-MATLAB/
├── data/
│   └── ALL_clean_fixed_qc_10_45.csv      # main dataset (time-series)
├── src/
│   └── train_pmfc_ann_fitnet_10min.m     # main training / evaluation script
└── README.md

---

## 🧮 Input Data (CSV)

The script expects a table with at least the following columns:

### Voltage outputs (per PMFC unit)
- PMFC1-V, PMFC2-V, PMFC3-V
- PMFC4-V, PMFC5-V, PMFC6-V

### Per-cell temperatures
- PMFC1-Temp, PMFC2-Temp, PMFC3-Temp
- PMFC4-Temp, PMFC5-Temp, PMFC6-Temp

### Ambient variables
- Temp-Amb (ambient temperature)
- Hum-Amb  (ambient relative humidity)

---

## 🧠 Model Description

- **Network type:** fitnet  
- **Architecture:** [20 10]  
- **Training function:** trainlm  
- **Prediction horizon:** 10 min  
- **Voltage lags:** V(t), V(t-1), V(t-2)  
- **Exogenous lags:** X(t), X(t-1)

### Data normalization
- mapminmax to [0,1] using training statistics only.

### Data split
- Train: 70%  
- Validation: 15%  
- Test: 15%

---

## 🧩 Script Workflow

1. Load CSV  
2. Verify column names  
3. Build lagged matrices  
4. Create +10 min targets  
5. Split Train/Val/Test  
6. Normalize  
7. Train ANN (fitnet)  
8. Predict and denormalize  
9. Compute metrics  
10. Generate figures  
11. Save results  

---

## 📊 Output Files

- pmfc_fitnet_model_10min.mat  
- pmfc_results_final.mat  
- PMFC_2x3_tracking.png  
- PMFC{i}_timeseries_residual.png  
- PMFC{i}_regression.png

---

## 🚀 Quick Start

git clone https://github.com/<your-user>/PMFC-ANN-MATLAB.git
cd PMFC-ANN-MATLAB
cd src
train_pmfc_ann_fitnet_10min

Ensure ALL_clean_fixed_qc_10_45.csv is placed in data/ or MATLAB's current folder.
