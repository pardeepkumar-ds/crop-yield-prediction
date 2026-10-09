# 🌾 Crop Yield Prediction Using Machine Learning

Predicting crop yields from historical climate and agricultural data to support smarter
agricultural planning — built as a comparison of classical regression models against a
tree-based model on real FAO/World Bank-sourced data.

![Python](https://img.shields.io/badge/Python-3.11-blue)
![scikit--learn](https://img.shields.io/badge/scikit--learn-ML-orange)
![status](https://img.shields.io/badge/status-complete-brightgreen)

---

## 📖 Overview

Crop yield is shaped by a complex mix of climate conditions, pesticide/fertilizer use, and
crop- and region-specific factors. This project trains and compares several machine learning
models that predict yield (tonnes/hectare) from:

- **Climate data** — average rainfall (mm/year), average temperature (°C)
- **Agricultural inputs** — pesticide use (tonnes)
- **Categorical context** — crop type (`Item`) and country (`Area`)
- **Time** — year (1990–2013)

The notebook walks through the full pipeline: data loading → raw data quality checks →
cleaning → exploratory data analysis → feature engineering → encoding/scaling → model
training → evaluation → conclusions.

## 📂 Project Structure

```
.
├── Crop_Yield_Prediction.ipynb   # Main notebook (fully executed, outputs included)
├── README.md
└── Data/
    ├── yield_df.csv              # Pre-merged modelling dataset (primary input)
    ├── yield.csv                 # Raw FAO yield data (hg/ha) by country, crop, year
    ├── rainfall.csv              # Raw World Bank rainfall data by country & year
    ├── temp.csv                  # Raw average temperature by country & year
    └── pesticides.csv            # Raw FAO pesticide-use data by country & year
```

## 📊 Dataset

Source: **Crop Yield Prediction Dataset** (Kaggle), compiling FAO crop-yield statistics,
World Bank rainfall data, FAO pesticide-use data, and historical temperature records.

- **101 countries** · **10 crops** · **1990–2013**
- Target variable: `hg/ha_yield` (converted to tonnes/ha in the notebook for interpretability)

> Place the five CSV files above in a `Data/` folder (or update the file paths at the top of
> the notebook) before running.

## 🔧 Pipeline Summary

1. **Data loading & quality check** — inspects all four raw sources; flags missing/non-numeric
   rainfall and temperature readings and country-naming inconsistencies across sources.
2. **Cleaning** — de-duplicates the merged dataset and adds a tonnes/ha yield column.
3. **EDA** — yield distribution, rainfall-vs-yield scatter, temperature distribution,
   yield trend over time, correlation heatmap.
4. **Feature engineering** — `years_since_start`, `rainfall_temp_interaction`,
   `pesticide_intensity`, `drought_index_proxy`; one-hot encoding of `Area` and `Item`.
5. **Modelling** — Linear Regression, Ridge, Lasso, Polynomial Regression (degree 2), and a
   Random Forest for a non-linear/tree-based comparison.
6. **Evaluation** — RMSE, MAE, R² for every model, plus feature-importance and
   predicted-vs-actual plots.

## 📈 Results

| Model | R² | RMSE (t/ha) | MAE (t/ha) |
|---|---|---|---|
| **Random Forest** | **0.978** | **1.263** | **0.570** |
| Linear Regression | 0.749 | 4.267 | 2.991 |
| Ridge Regression | 0.749 | 4.268 | 2.987 |
| Polynomial Regression | 0.748 | 4.271 | 3.004 |
| Lasso Regression | 0.727 | 4.446 | 2.972 |

**Key finding:** the linear models cluster tightly together (R² ≈ 0.73–0.75) and are all
clearly outperformed by the Random Forest — evidence that yield depends on non-linear,
interacting effects between crop, country, and climate rather than a simple additive
combination of raw features. Crop type (`Item`) is the single most important predictor.

## 🚀 Getting Started

### Requirements
```
python >= 3.9
numpy
pandas
matplotlib
seaborn
scikit-learn
```

Install with:
```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```

### Run
```bash
git clone <your-repo-url>
cd <your-repo-name>
jupyter notebook Crop_Yield_Prediction.ipynb
```
Then **Run All** cells. (The notebook as shipped already has every cell executed, so you can
also just open and read it without running anything.)

## ⚠️ Limitations & Future Work

- No soil-type or fertilizer-tonnage data was available — only pesticide totals.
- Climate data is annual, not daily, so true Growing Degree Days couldn't be computed.
- Yield is averaged at the country level, hiding regional/farm-level variation.
- Next steps: sub-national weather/soil data, gradient-boosted trees (XGBoost/LightGBM),
  hyperparameter tuning with cross-validation, and more recent data (this dataset ends 2013).

## 📜 License

This project is shared for educational/portfolio purposes. Add a license file (e.g. MIT) if
you plan to open-source it formally.

## 🙏 Acknowledgments

- Dataset: Crop Yield Prediction Dataset (Kaggle), compiled from FAO and World Bank sources.

---

*Author: [Your Name] — update this section with your details before publishing.*
