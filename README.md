# CO₂ emissions EDA

Exploratory data analysis of global CO₂ emissions using the
[Our World in Data CO₂ dataset](https://github.com/owid/co2-data).

## Structure

```
co2-eda/
├── data/raw/            owid-co2-data.csv, owid-co2-codebook.csv (as downloaded, never edited)
├── data/clean/          co2_clean.csv (written by 01_cleaning.ipynb)
├── notebooks/           01_cleaning.ipynb, 02_analysis.ipynb
├── figures/             PNG charts exported by the notebooks, ready for slides
└── README.md
```

## Data

- `data/raw/owid-co2-data.csv` — one row per location per year, 1750 to 2025.
  Source: https://raw.githubusercontent.com/owid/co2-data/master/owid-co2-data.csv
- `data/raw/owid-co2-codebook.csv` — description, unit and source of every column.
- `data/clean/co2_clean.csv` — the subset of columns used in the analysis, plus
  `gdp_per_capita` and an `is_aggregate` flag that separates real countries from
  regions and income groups such as *World* or *Asia*.

## How to run

Requires Python 3.11 or later with pandas, matplotlib, seaborn and Jupyter. For example, with conda:

```bash
git clone https://github.com/Mohamed-Arbi-Ghanmi/co2-eda.git
cd co2-eda
conda create -n co2-eda -c conda-forge python=3.13 pandas matplotlib seaborn jupyterlab nbconvert
conda activate co2-eda
jupyter lab notebooks/
```

Or with pip in any virtual environment:

```bash
pip install pandas matplotlib seaborn jupyterlab nbconvert
```

Run the notebooks in order:

1. `01_cleaning.ipynb` — loads the raw file, keeps the needed columns, splits
   countries from aggregates, checks missingness and writes `data/clean/co2_clean.csv`.
2. `02_analysis.ipynb` — reads the clean file and produces the analysis
   (distribution, global trend, rankings, regions, wealth, decoupling, trade, country profile).

Every chart is saved to `figures/` as a PNG when its cell runs.

The notebooks resolve paths relative to the project root, so they work whether
the kernel starts in `co2-eda/` or in `co2-eda/notebooks/`.

To run both notebooks from the command line without opening Jupyter:

```bash
jupyter nbconvert --to notebook --execute --inplace notebooks/01_cleaning.ipynb
jupyter nbconvert --to notebook --execute --inplace notebooks/02_analysis.ipynb
```
