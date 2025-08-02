# No One-Size-Fits-All: Uncovering Spatio‑Temporal Forecasting Trade‑offs with Graph Neural Networks and Foundation Models

## 📑 Table of Contents
- [Abstract](#abstract)  
- [Background & Motivation](#background--motivation)  
- [Model Overview](#model-overview)  
  - [Classical Baselines](#classical-baselines)  
  - [Time Series Foundation Models (TSFMs)](#time-series-foundation-models-tsfms)  
  - [Spatio‑Temporal GNNs (STGNNs)](#spatio-temporal-gnns-stgnns)  
- [Dataset & Preprocessing](#dataset--preprocessing)  
- [Methodology](#methodology)  
  - [Experimental Design](#experimental-design)  
- [Implementation](#implementation)  

---

## Abstract
Modern IoT deployments produce high‑volume spatiotemporal data for forecasting tasks. We benchmark classical (VAR, GRU, Transformer), Spatio‑Temporal GNNs (GRUGCN, T‑GCN), and Time Series Foundation Models (Moirai, TimesFM) on temperature forecasting in a 25‑node wireless sensor network. By varying sampling rates (5–60 min) and node counts (8, 16, 25), we uncover trade‑offs: STGNNs excel under sparse coverage and moderate frequency, TSFMs shine at high frequency but degrade with reduced spatial context. Our study guides model and deployment choices in large‑scale sensing systems.

---

## Background & Motivation
Environmental sensing and smart‑grid applications rely on dense IoT networks streaming high‑frequency data. While edge sampling strategies aim to reduce data volume, their impact on centralized forecasting models is under‑studied. Different architectures (classical, RNNs, Transformers, STGNNs, TSFMs) exhibit unique sensitivities to temporal resolution and spatial coverage. We ask:  
> **Do graph‑based STGNNs inherently outperform non‑graph alternatives across sampling frequencies and node densities?**

---

## Model Overview

### Classical Baselines
- **VAR**: Multivariate autoregression leveraging all series jointly, no training required.  
- **GRU**: Gated Recurrent Units for sequential temporal modeling.  
- **Transformer**: Self‑attention model for long‑range temporal dependencies.

### Time Series Foundation Models (TSFMs)
| Attribute                  | TimesFM (200 M)      | Moirai‑Small (14 M)     |
|----------------------------|----------------------|-------------------------|
| Zero‑shot                  | ✓                    | ✓                       |
| Multivariate               | ✗ (uni + covariates) | ✓                       |
| Probabilistic Forecasting  | ✗ (point‑wise)       | ✓                       |
| Pretraining Corpus         | 100 B time‑points    | 27 B observations       |
| Architecture               | Decoder‑only         | Encoder‑only            |
| Tokenization               | Fixed patches        | Multi‑resolution patches|

### Spatio‑Temporal GNNs (STGNNs)
- **GRUGCN**  
  1. GRU per‑node for temporal patterns  
  2. GCN aggregation of neighbor states  
- **T‑GCN**  
  1. GCN on raw features per time step  
  2. GRU for sequence modeling  

Graphs encode sensor similarity via Pearson correlation; see [Graph Construction](#graph-construction).

---

## Dataset & Preprocessing
- **Source**: IoBT wireless weather network (25 towers, New Mexico)  
- **Feature**: Temperature (°C) sampled every 5 min over 9 days  
- **Splits**: 5 days train / 2 days validation / 2 days test  
- **Task**: Forecast horizon \(H=4\) h from context window \(W=8\) h  
  $$
    W = 8\text{ h},\quad H = 4\text{ h}
  $$
- **Downsampling**: \{5, 15, 30, 45, 60\} min  

### Preprocessing Steps
1. **Z‑score normalization**  
2. **Window aggregation** to fixed \(W\) per node  
3. **Graph thresholding** by top‑\(p\)% Pearson correlations  

---

## Methodology

### Experimental Design
- **Variables**  
  - Sampling rate: 5–60 min  
  - Node count: 8, 16, 25  
- **Metrics**: MAE, RMSE, MAPE  

Here’s the corrected Markdown with properly formatted equations:
## Implementation
