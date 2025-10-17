# Benchmarking Spatiotemporal Forecast Models

Implementation for comparing Baseline Temporal, Graph Neural Networks and Time-Series Foundation Models for spatio-temporal temperature forecasting.

> **Paper**: "No One-Model-Fits-All: Uncovering Spatio-Temporal Forecasting Trade-offs with Graph Neural Networks and Foundation Models"

## Overview

Systematic comparison of forecasting models under varying sampling rates (5-60 min) and spatial coverage (8-25 nodes):

- **Classical(Baseline)**: VAR, GRU, Transformer
- **TSFMs**: Moirai, Chronos, TimesFM  
- **STGNNs**: GRUGCN, TGCN
  
## Dataset

**IoBT Meteorological Data**: 25 sensor towers, 10km × 10km area, 9 days at 5-min sampling
- Train: 5 days | Val: 2 days | Test: 2 days
- Features: **Temperature**, Humidity, Rainfall, Pressure


## Experiment Setup

- **Context Window**: 8 hours (480 min)
- **Prediction Horizon**: 4 hours (240 min)
- **Sampling Rates**: 5, 15, 30, 45, 60 minutes
- **Node Counts**: 8, 16, 25 sensors
- **Graph Redundancy** (STGNNs): 0%, 20%, 60%, 100%

## Repository Structure

```
├── data/                    # IoBT dataset and adj_maps
    ├── post_processed
    ├── visualization
├── models/
    ├── baseline/            # VAR, GRU, Transformer
    ├── tsfm/               # Moirai, TimesFM, Chronos
    └── stgnn/              # GRUGCN, TGCN
```

## Citation

```bibtex
@inproceedings{gupta2024noonemodel,
  title={No One-Model-Fits-All: Uncovering Spatio-Temporal Forecasting Trade-offs 
         with Graph Neural Networks and Foundation Models},
  author={Gupta, Ragini and Raina, Naman and Chen, Bo and Chen, Li and 
          Danilov, Claudiu and Eckhardt, Josh and Bernard, Keyshla and Nahrstedt, Klara},
  booktitle={ACM Workshop},
  year={2024}
}
```
