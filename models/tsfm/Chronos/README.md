# Chronos Zero-Shot Forecasting (Colab)

> Runs the **Chronos / Chronos-Bolt** pipeline on IoBT temperature data across
> sampling rates and node counts. Produces per-run metrics CSVs and (optionally) plot CSVs.

---

## 1) Setup (Colab)
1. Create a Hugging Face token and add it in **Colab → Secrets** as **`HF_TOKEN`**.
2. In the first cell of the notebook run:
   ```python
   from huggingface_hub import login
   import os
   from google.colab import userdata
   login(token=userdata.get('HF_TOKEN'))
