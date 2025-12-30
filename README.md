# Basel Velo/Fuss Counts + MeteoSwiss Weather (Data Wrangling)

Reproducible data wrangling project that merges Basel-Stadt bicycle/pedestrian counting station data (Velo/Fuss) with MeteoSwiss weather data (station BAS: Basel/Binningen). The pipeline produces a clean daily dataset (`data/merged_dataset.csv`) and an exploratory analysis notebook.

## Repository contents
- `01_build_merged_dataset.ipynb`: load → clean → daily aggregation → merge → quality assurance → write output
- `02_analysis_plots.ipynb`: exploratory analysis and plots
- `data/merged_dataset.csv`: final merged daily dataset
- `requirements.txt`: Python dependencies

## Data sources
- Basel-Stadt Velo/Fuss counts: https://data.bs.ch/explore/dataset/100013/
- Meteo Swiss Data: https://www.meteoswiss.admin.ch/services-and-publications/applications/ext/download-data-without-coding-skills.html#lang=en&mdt=normal&pgid=&sid=BAS&col=ch.meteoschweiz.ogd-smn&di=hourly&tr=historical&hdr=2020-2029
    - MeteoSwiss BAS hourly data: https://data.geo.admin.ch/ch.meteoschweiz.ogd-smn/bas/ogd-smn_bas_h_historical_2020-2029.csv
    - MeteoSwiss parameter metadata: https://data.geo.admin.ch/ch.meteoschweiz.ogd-smn/ogd-smn_meta_parameters.csv

Notes:
- MeteoSwiss CSV uses `;` as separator and is read with `latin1` encoding.

## Git LFS (required)
This repository uses **Git LFS** to store large CSV files under `data/`. Without Git LFS you will download pointer files and the notebooks will fail.

```bash
git lfs install
git clone https://github.com/Markusspb/DAW_daily_temperatur_and_pedestrians.git
cd DAW_daily_temperatur_and_pedestrians
git lfs pull
```

## Reproducibility (clean environment)

Requirement: **Python >= 3.10 and < 3.13**. Run commands from the repository root (notebooks use relative `data/...` paths).

Create a virtual environment:

```bash
python -m venv .venv
```

Activate:

* Windows (PowerShell): `.venv\Scripts\Activate.ps1`
* macOS / Linux: `source .venv/bin/activate`

Install dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Run notebooks in order:

```bash
jupyter lab
```

1. `01_build_merged_dataset.ipynb` (writes `data/merged_dataset.csv`)
2. `02_analysis_plots.ipynb` (plots + summaries)

## Output dataset

`data/merged_dataset.csv` columns:

* `SiteCode`, `SiteName`, `date`, `daily_total`
* `temp_mean_C`, `precip_mm`, `wind_mean_ms`
* `weekday`, `is_weekend`

## Data quality note (stable panel)

Some stations have partial coverage within the year. Aggregated analyses in Notebook 02 use a stable subset of stations with full daily coverage to avoid panel bias in time-series totals.

## Submission note (ZIP)

Do not rely on GitHub “Download ZIP” for LFS data. Before creating a ZIP locally, run:

```bash
git lfs pull
```

## Authors

* Pablo Munoz Ceroni
* Markus Barten
