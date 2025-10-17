# MOIRAI_Analysis.ipynb — Zero-Shot Multivariate Forecasting

Short, self-contained notebook to evaluate **Moirai** (time-series foundation model) on the IoBT temperature dataset under different **sampling rates** (5–60 min) and **node counts** (8/16/25). It prepares data, runs zero-shot forecasts, and saves metrics/plots.

**Notebook:** [MOIRAI_Analysis.ipynb](MOIRAI_Analysis.ipynb)

---

## What this notebook does
- Loads CSVs from `Dataset_perSampling_pernodeConfig/temperature_data_{SAMP}min_{NODES}.csv`.
- Builds fixed windows (context) and horizons.
- Runs **Moirai** zero-shot forecasts.
- Computes **MAE / RMSE / MAPE** and exports tidy CSV.
