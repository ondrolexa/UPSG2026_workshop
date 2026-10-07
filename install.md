# Installation

The workshop uses one Python project managed by [uv](https://docs.astral.sh/uv/)
containing `apsg`, `petropandas` and Jupyter Lab.

## 1. Install uv (one-time)

```bash
# Linux / macOS
curl -LsSf https://astral.sh/uv/install.sh | sh
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## 2a. Use the workshop materials (recommended)

The materials ship `pyproject.toml` and `uv.lock` with the exact versions the notebooks
were tested with (apsg 2.0.5, petropandas 0.2.3, Python 3.14):

```bash
cd UPSG2026_workshop      # or UPSG2026_workshop-main (from the ZIP)
uv sync
```

## 2b. Or start your own project from scratch

```bash
uv init --bare --python 3.14 myproject
cd myproject
uv add "apsg[lab]" "petropandas[lab]"
```

## 3. Start Jupyter Lab

```bash
uv run jupyter lab
```

## 4. Check the installation

In a new notebook:

```python
import apsg, petropandas
print(apsg.__version__, petropandas.__version__)

from apsg import *
quicknet(fol(120, 40), lin(210, 30))          # a stereonet should appear

from petropandas import pd, Grt
from petropandas.data import minerals
minerals.oxides.select("Garnet", on="Mineral").mineral.end_members(Grt).head()
```

## Upgrading later

```bash
uv lock --upgrade-package apsg --upgrade-package petropandas
uv sync
```
