# Environment Setup

Pick **one** of the options below.

---

## Option A — Conda (portable, from `environment.yml`)
Creates an env using versions/ranges declared in `environment.yml`.

```bash
conda env create -n TimesFM -f environment.yml
conda activate TimesFM
```

---

## Option B — Conda (exact, from `conda-spec.txt`)
Recreates an **exact** environment from a file exported via:
`conda list --explicit > conda-spec.txt`.

```bash
conda create -n TimesFM --file conda-spec.txt
conda activate TimesFM
```

---

## Option C — Pip + venv (from `requirements.txt`)
Lightweight alternative if you prefer pip/venv.

```bash
python -m venv .venv
# Linux/Mac:
source .venv/bin/activate
# Windows:
# .venv\Scripts\activate

pip install -r requirements.txt
```

---

## (Optional) Register the Jupyter kernel
Run **after** activating your env (Conda or venv):

```bash
python -m ipykernel install --user --name TimesFM --display-name "Python (TimesFM)"
```

> If you update packages later, you don’t need to re-register; just keep using the same kernel name.
