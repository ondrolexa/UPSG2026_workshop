# Modern Workflow in Geology — Process Structural and Petrological Data Efficiently

One-day hands-on workshop

- **When:** 8 October 2026
- **Where:** Institute of Petrology and Structural Geology, Faculty of Science, Charles University, Albertov 6, Prague
- **Lecturer:** Ondrej Lexa

**Goal:** you leave with ready-made Jupyter notebooks into which you can simply "pour"
your own Excel tables with structural measurements or microprobe data and get
stereograms, recalculations and charts.

**Prerequisites:** a basic understanding of Python, the Jupyter Lab environment and how
the pandas library works. Bring a laptop (Linux, macOS or Windows) — and, for the last
block, your own data.

## Plan

| Time | Block | Slides | Notebook |
|---|---|---|---|
| 09:00–09:30 | **Introduction** — scientific Python, installing `apsg` and `petropandas`, philosophy of both packages | `00_intro.pdf` | — |
| 09:30–11:00 | **Block 1: Structural geology with `apsg`** — features, stereonets, contours, orientation statistics, fold axes. *Exercise:* field data → stereogram → vector graphics | `01_apsg_basics.pdf` | `01_apsg_basics.ipynb` |
| 11:00–11:15 | *Coffee break* | | |
| 11:15–12:30 | **Block 2: Advanced structural and tensor analysis** — faults and right dihedra, finite strain, strain markers, stress inversion. *Exercise:* superposition of deformations, brittle structures | `02_apsg_advanced.pdf` | `02_apsg_advanced.ipynb` |
| 12:30–13:30 | *Lunch break* | | |
| 13:30–15:00 | **Block 3: Petrological data with `petropandas`** — EPMA from Excel, formulas and end-members, filtering bad analyses. *Exercise:* wt% oxides → apfu → valid analyses → charts | `03_petropandas.pdf` | `03_petropandas.ipynb` |
| 15:00–15:15 | *Coffee break* | | |
| 15:15–16:30 | **Block 4: Bring your own data** — your own thesis data, consultations and debugging | `04_byod.pdf` | `04a_byod_structural.ipynb`<br>`04b_byod_epma.ipynb` |

Slides are in [`slides/`](slides/), notebooks in [`notebooks/`](notebooks/).

The teaching notebooks (01–03) each end with a hands-on exercise followed by a worked
solution. The BYOD notebooks (04a, 04b) are **templates**: edit only the `CONFIG` cell at
the top (file name, column names, ...), then *Run → Run All Cells*.

## Installation

The workshop uses one Python project managed by [uv](https://docs.astral.sh/uv/), a fast
Python package and project manager. uv also installs Python itself, so you don't need an
existing Python installation.

### 1. Install uv

**Linux and macOS**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

(if `curl` is not available: `wget -qO- https://astral.sh/uv/install.sh | sh`;
on macOS with Homebrew you can also use `brew install uv`)

**Windows** (PowerShell)

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

(or `winget install --id=astral-sh.uv -e`)

Close and reopen the terminal afterwards, then check:

```bash
uv --version
```

### 2. Get the workshop materials

**Option A — download a ZIP (no git needed)**

1. Download <https://github.com/ondrolexa/UPSG2026_workshop/archive/refs/heads/main.zip>
   (or on the [repository page](https://github.com/ondrolexa/UPSG2026_workshop) click
   **Code → Download ZIP**).
2. Unzip it and open a terminal in the unzipped folder:

```bash
cd UPSG2026_workshop-main
```

**Option B — clone with git**

```bash
git clone https://github.com/ondrolexa/UPSG2026_workshop.git
cd UPSG2026_workshop
```

With git you can later fetch updates with `git pull`.

### 3. Install the dependencies

In the workshop folder run:

```bash
uv sync
```

This creates a local virtual environment in `.venv/` with Python 3.14 and the exact
package versions the notebooks were tested with (pinned in `uv.lock`): `apsg`,
`petropandas`, Jupyter Lab and their dependencies.

### 4. Launch the notebooks

```bash
uv run jupyter lab
```

Jupyter Lab opens in your browser; open the `notebooks/` folder and start with
`01_apsg_basics.ipynb`. Stop the server with `Ctrl+C` in the terminal.

### 5. Check the installation

In a new notebook run:

```python
import apsg, petropandas
print(apsg.__version__, petropandas.__version__)

from apsg import *
quicknet(fol(120, 40), lin(210, 30))          # a stereonet should appear

from petropandas import pd, Grt
from petropandas.data import minerals
minerals.oxides.select("Garnet", on="Mineral").mineral.end_members(Grt).head()
```

### Using apsg and petropandas in your own project

```bash
uv init --bare --python 3.14 myproject
cd myproject
uv add "apsg[lab]" "petropandas[lab]"
uv run jupyter lab
```

More details, including upgrading packages, are in [install.md](install.md).

## Repository layout

```
slides/            lecture slides (PDF) and their LaTeX sources
notebooks/         Jupyter notebooks for each block
notebooks/data/    example data used in the notebooks
notebooks/output/  figures and tables written by the notebooks (created when you run them)
```

### Example data (`notebooks/data/`)

| File | Content |
|---|---|
| `structures.csv`, `structures_wide.csv` | field structural data (long and wide table layout), from the apsg documentation |
| `mele.csv` | 94 fault-slip measurements, from the apsg documentation |
| `field_measurements.csv` | synthetic survey of a folded sequence: bedding S0, cleavage S1, lineation L1 |
| `epma_export.xlsx` | synthetic microprobe export: garnet, plagioclase, biotite and muscovite spots (including a few bad analyses) and a garnet profile |

## Resources

- apsg: <https://github.com/ondrolexa/apsg>
- petropandas: <https://github.com/ondrolexa/petropandas>
- uv: <https://docs.astral.sh/uv/>

## License

The workshop materials are released under the [MIT License](LICENSE).
