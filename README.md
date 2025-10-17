# Benchmarking Spatiotemporal Forecast Models

PyTorch implementation comparing Graph Neural Networks and Foundation Models for spatio-temporal temperature forecasting.

> **Paper**: "No One-Model-Fits-All: Uncovering Spatio-Temporal Forecasting Trade-offs with Graph Neural Networks and Foundation Models"

## Overview

Systematic comparison of forecasting models under varying sampling rates (5-60 min) and spatial coverage (8-25 nodes):

- **Classical**: VAR, GRU, Transformer
- **TSFMs**: Moirai, Chronos, TimesFM  
- **STGNNs**: GRUGCN, TGCN

**Key Finding**: Multivariate TSFM (Moirai) achieves best overall performance. STGNNs excel when spatial correlations are strong and data is sparse (optimal at 20-60% graph redundancy).

## Installation

```bash
git clone https://github.com/anonymousUser041603/Benchmarking-Spatiotemporal-Forecast-Models.git
cd Benchmarking-Spatiotemporal-Forecast-Models
pip install -r requirements.txt
```

**Requirements**: Python 3.8+, PyTorch 2.0+, torch-geometric, pytorch-lightning, torch-spatiotemporal

## Dataset

**IoBT Meteorological Data**: 25 sensor towers, 10km × 10km area, 9 days at 5-min sampling
- Train: 5 days | Val: 2 days | Test: 2 days
- Features: Temperature, humidity, rainfall, pressure

## Quick Start

```bash
# Train baseline models
python train_baseline.py --model gru --sampling_rate 15 --nodes 16

# Evaluate TSFMs (zero-shot)
python eval_tsfm.py --model moirai --sampling_rate 30 --nodes 25

# Train STGNNs with graph redundancy
python train_stgnn.py --model grugcn --redundancy 60 --sampling_rate 15 --nodes 16

# Run full benchmark
bash scripts/run_all_experiments.sh
```

## Experiment Setup

- **Context Window**: 8 hours (480 min)
- **Prediction Horizon**: 4 hours (240 min)
- **Sampling Rates**: 5, 15, 30, 45, 60 minutes
- **Node Counts**: 8, 16, 25 sensors
- **Graph Redundancy** (STGNNs): 0%, 20%, 60%, 100%

## Key Results

| Model | Best Scenario | MAE (°C) |
|-------|---------------|----------|
| **Moirai** | 45min/8 nodes | **0.861** |
| **TGCN** | 15min/16 nodes (20% red.) | 1.829 |
| **GRUGCN** | 30min/8 nodes (60% red.) | 2.088 |
| **Chronos** | 15min/25 nodes | 3.400 |
| **TimesFM** | 5min/8 nodes (w/ covariates) | 3.753 |

### Model Trade-offs

- **Moirai**: Best overall, native multivariate learning via attention
- **STGNNs**: Outperform when spatial correlations strong and redundancy tuned
- **Chronos**: Most robust zero-shot univariate forecasting
- **TimesFM**: Struggles at coarse sampling, improves with ensemble similarity

## Repository Structure

```
├── data/                    # IoBT dataset and preprocessing
├── models/
│   ├── baselines.py        # VAR, GRU, Transformer
│   ├── tsfm/               # Moirai, TimesFM, Chronos
│   └── stgnn/              # GRUGCN, TGCN
├── utils/
│   ├── graph_construction.py
│   └── ensemble_similarity.py
├── configs/                # Hyperparameters
├── scripts/                # Training scripts
└── results/                # Logs and outputs
```

## Reproduce Paper Results

```bash
python reproduce_table2.py  # Baseline models
python reproduce_table3.py  # TSFMs
python reproduce_table4.py  # STGNNs
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

## License

MIT License - see [LICENSE](LICENSE) for details.
