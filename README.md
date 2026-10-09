# Crop yield prediction

Forecasting crop yield in tonnes per hectare for 101 countries and 10 crops, 1990–2013, from FAO yield and pesticide tables and World Bank rainfall and temperature.

The saved run uses the reconciled modelling table, not the raw climate files. 2,310 duplicate rows were removed. 25,932 country–crop–year records remain. 116 features after encoding.

## Result

Random Forest is the model to use when accuracy matters. The linear models stay in the comparison because their coefficients are easier to explain.

| Model | R² | RMSE (t/ha) | MAE (t/ha) |
|---|---:|---:|---:|
| Random Forest | 0.9780 | 1.263 | 0.570 |
| Linear regression | 0.7488 | 4.267 | 2.991 |
| Ridge | 0.7486 | 4.268 | 2.987 |
| Polynomial | 0.7483 | 4.271 | 3.004 |
| Lasso | 0.7273 | 4.446 | 2.972 |

![R² and RMSE by model](assets/model_comparison.png)

## What actually drives yield

Crop identity is the strongest single feature, potatoes in particular. Country and climate matter most once the crop is fixed. Rainfall on its own has almost no linear correlation with yield (about 0). That is why the model uses crop, country, temperature, pesticides, and interactions together, not rainfall alone.

![Top 15 Random Forest importances](assets/feature_importance.png)

![Rainfall versus yield](assets/rainfall_vs_yield.png)

## Fit

![Predicted versus actual](assets/predicted_vs_actual.png)

![Mean yield, 1990–2013](assets/yield_over_time.png)

![Numeric correlation](assets/correlation.png)

## Data

| File | Role |
|---|---|
| `yield.csv` | FAO crop yield (hg/ha) |
| `pesticides.csv` | FAO pesticide use (tonnes) |
| `rainfall.csv` | World Bank average annual rainfall |
| `temp.csv` | Average temperature by country and year |
| `yield_df.csv` | Reconciled modelling table |

Raw climate files are messy on purpose in this check: 780 rainfall readings and 2,547 temperature readings are missing or non-numeric, and country names do not match across agencies. Modelling uses `yield_df.csv`, then this project's own cleaning.

## How to run

From the folder that contains `data/`:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
jupyter notebook Pardeep_kumar_cropyieldproduction.ipynb
```

The notebook looks for each CSV in the current folder and in `data/`.

## Stack

Python, pandas, NumPy, scikit-learn, Matplotlib, Seaborn, Jupyter.
