# FAERS Dual ICI (Nivolumab + Ipilimumab) Cardiotoxicity Signal Pipeline

This repository contains a reproducible analysis pipeline for evaluating **cardiotoxicity safety signals** associated with immune checkpoint inhibitors (ICI) using **FAERS** reports, with a focus on:

- Nivolumab monotherapy
- Ipilimumab monotherapy
- Dual therapy (nivolumab + ipilimumab)

Curated **submission-ready outputs** (tables/figures) used in the manuscript are included under `outputs/`.

## What is included

- `scripts/` one-command runners
- `src/` analysis modules (cohorting, disproportionality, interaction metrics, modeling, plots)
- `outputs/` curated CSV tables and PNG figures (as generated on Kaggle)
- `manuscript/` the submission-ready DOCX

## What is NOT included

- Raw FAERS data files are **not** committed.

## Data requirements

Place FAERS-derived flat files under:

```
data/raw/
  DRUG.csv
  DEMOGRAPHIC.csv
  REACTION.csv
```

These are expected to be **tab-separated** (\t) and to contain standard FAERS-style identifiers (e.g., `primaryid`/`caseid`) and drug/event fields.
See `schema/` for expected columns.

## Quickstart

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements_min.txt
# (Optional) For exact Kaggle environment, see requirements.txt

# Copy and edit config
cp config.example.yaml config.yaml

# Run the full pipeline
python scripts/run_pipeline.py --config config.yaml
```

Outputs are written to `outputs/tmp/` (intermediate) and `outputs/` (curated).

## GitHub "single-shot" push

After unzipping this repository:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## Interpretation note

FAERS is a spontaneous reporting system; analyses here estimate **reporting disproportionality** (e.g., ROR) and interaction **signals**. These results are not incidence rates.

## Folder map

- `outputs/tables/`: curated CSV tables (ROR, interaction metrics, adjusted OR, sensitivity analyses)
- `outputs/figures/`: curated PNG figures (forest plot, time trends, central illustration)

