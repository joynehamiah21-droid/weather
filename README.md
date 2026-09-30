# AIML-Recruitment-2026-Joy

Coding Ninjas 10X — AI/ML Recruitment Task (Second Years)
Task 1: Air Quality Forecasting

---

## Table of Contents
- [Candidate Details](#candidate-details)
- [Tasks Completed](#tasks-completed)
- [Problem Statement](#problem-statement)
- [Dataset](#dataset)
- [Approach](#approach)
- [Technologies Used](#technologies-used)
- [Repository Structure](#repository-structure)
- [How to Run](#how-to-run)
- [Results](#results)
- [Key Learnings](#key-learnings)
- [Challenges](#challenges)

---

## Candidate Details
- **Name:** Joy
- **Institute:** SRM Institute of Science and Technology, Ramapuram
- **Year:** Second year

## Tasks Completed
- [x] Task 1: Air Quality Forecasting

## Problem Statement
Air pollution monitoring stations generate a continuous stream of hourly sensor and pollutant readings. This project uses the UCI Air Quality dataset to analyse historical trends in urban air quality and to build a model that predicts the **CO concentration one hour ahead**, based on recent pollutant, sensor, and weather readings.

## Dataset
- **Source:** [UCI Air Quality Dataset](https://archive.ics.uci.edu/dataset/360/air+quality)
- **Period:** March 2004 – April 2005, hourly readings
- **Fields:** CO, NOx, NO2, C6H6 (ground truth), five metal-oxide sensor responses (PT08.S1–S5), temperature, relative humidity, absolute humidity
- **Notes:** missing values are encoded as `-200`; `NMHC(GT)` is missing for ~90% of rows

## Approach
1. **Data Cleaning**
   - Parsed `Date` + `Time` into a proper datetime index and reindexed to a complete hourly frequency
   - Replaced `-200` with `NaN`; dropped `NMHC` (too sparse to be useful)
   - Forward-filled short gaps (≤ 3 hours); left longer gaps as missing
2. **Exploratory Data Analysis**
   - Distribution and skewness of CO, NOx, NO2, C6H6
   - Correlation matrix / heatmap across pollutants and sensors
   - Daily, weekly, and monthly patterns (rush-hour peaks, weekday vs weekend)
   - Outlier detection via z-score
3. **Feature Engineering**
   - Lagged CO values (1, 2, 3, 6, 24 hours)
   - Rolling mean/std of CO (3, 6, 24-hour windows)
   - Cyclical hour encoding (sin/cos), day of week, weekend flag, month
4. **Modelling**
   - Chronological 80/20 train-test split (no shuffling, to respect time order)
   - Baseline: persistence model (`CO(t+1) = CO(t)`)
   - Compared Ridge Regression, Random Forest, and Histogram Gradient Boosting
5. **Evaluation & Analysis**
   - MAE, MSE, RMSE, R² on train and test sets
   - Actual-vs-predicted plots, error breakdown by hour/season/pollution level
   - Permutation feature importance
   - Discussion of data leakage risks in time-series prediction and how they were avoided

## Technologies Used
- Python 3
- pandas, NumPy
- scikit-learn
- matplotlib, seaborn
- Google Colab / Jupyter Notebook

## Repository Structure
```
AIML-Recruitment-2026-Joy/
├── Air_Quality_Forecasting.ipynb   # Main notebook (Task 1)
├── README.md
└── data/                           # (optional) local copy of AirQualityUCI.csv
```

## How to Run
1. Open `Air_Quality_Forecasting.ipynb` in Google Colab or Jupyter
2. Run all cells top to bottom (`Runtime → Run all` in Colab)
3. The notebook auto-downloads the dataset; if that fails, download `AirQualityUCI.csv` from the [UCI link](https://archive.ics.uci.edu/dataset/360/air+quality) and place it in the working directory

## Results

| Model | MAE | MSE | RMSE | R² |
|---|---|---|---|---|
| Persistence baseline | — | — | — | — |
| Ridge Regression | — | — | — | — |
| Random Forest | — | — | — | — |
| Hist Gradient Boosting | — | — | — | — |

*(Fill in with the actual values printed by the notebook after running it.)*

**Best model:** *fill in*
**Top predictive features:** *fill in from permutation importance output*

## Key Learnings
1. *e.g. Always compare a model against a simple baseline (here, persistence) to know whether it's actually adding value*
2. *e.g. How data leakage can silently creep into time-series models through shuffled splits or centered rolling windows*
3. *e.g. Why chronological train-test splitting is essential for time-dependent data*

## Challenges
- *e.g. Handling the `-200` missing-value encoding and the near-total absence of `NMHC` without discarding too much data*
