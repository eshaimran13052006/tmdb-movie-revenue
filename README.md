# Predicting Box-Office Revenue from TMDB Movie Data

**Programming for AI · Team: 25L-3001, 25L-0004 · SEED = 4**

Can we predict how much a movie will earn at the box office, using only what's known **before** it's released?
We collected 1,100 movies (100 per year, 2016–2026) from the [TMDB](https://www.themoviedb.org/) API, cleaned them, and trained regression models on the 899 movies with a known revenue.

## Results at a glance
| | |
|---|---|
| Final model | Gradient Boosting (tuned) |
| Test R² (log revenue) | 0.441 |
| Cross-validated R² | 0.496 |
| Most important features | budget, part of a franchise, budget unknown |
| Advanced technique #1 | KNN / Iterative imputation (Iterative cut the error by about 36% compared with the median) |
| Advanced technique #2 | Target encoding of director and studio (test R² 0.428 → 0.484) |

## What's in this repository
| Path | What it is |
|---|---|
| `01_Data_Collection_Preparation.ipynb` | collecting the data from TMDB, cleaning, missing values, imputation |
| `02_EDA_Modelling.ipynb` | charts, skewness, outliers, features, models, evaluation |
| `Project_Report.pdf` | the project report |
| `data/` | raw data (`tmdb_movies_raw.csv`), cleaned versions, collection log, fingerprints |
| `figures/` | all charts |
| `outputs/` | result tables, training log and saved models |

## How to run it
```
pip install -r requirements.txt
jupyter notebook
```
1. Open `01_Data_Collection_Preparation.ipynb` → Run All → paste your TMDB **API Read Access Token** when asked. This downloads fresh data (about 15 minutes), so the numbers and the fingerprint will change slightly, because TMDB updates every day.
2. Open `02_EDA_Modelling.ipynb` → Run All (about 5 minutes). It only needs the files in `data/`; no internet or token required.

To check the raw data hasn't been changed, compare its SHA-256 with `data/collection_log.json`:
```
python -c "import hashlib;print(hashlib.sha256(open('data/tmdb_movies_raw.csv','rb').read()).hexdigest())"
```

*This product uses the TMDB API but is not endorsed or certified by TMDB.*
