# crop-yield-prediction

Predicting crop yield (tonnes/hectare) for 101 countries and 10 crops using World Bank climate data and FAO statistics, comparing regression models including Random Forest

Overview
Predicted crop yield (tonnes/hectare) for 101 countries and 10 crops using World Bank climate data and FAO statistics, comparing multiple regression models to find the best fit.

What I Did
•  ⁠Collected and merged climate and agricultural data from World Bank and FAO sources
•  ⁠Engineered 116 features including temperature, rainfall, and crop-specific variables
•  ⁠Compared Linear, Ridge, Lasso, Polynomial, and Random Forest regression models
•  ⁠Evaluated models using R² score and RMSE

Tools Used
•  ⁠Python, pandas, NumPy
•  ⁠scikit-learn
•  ⁠Matplotlib, Seaborn
•  ⁠Jupyter Notebook

How to Run
1.  ⁠Clone this repository
2.  ⁠Install dependencies: pip install numpy pandas matplotlib seaborn scikit-learn
3.  ⁠Download the dataset from the sources mentioned in the notebook
4.  ⁠Open the notebook and run all cells

Key Findings
•  ⁠Random Forest achieved the best performance with an R² of 0.978 and RMSE of 1.26 tonnes/hectare
•  ⁠Feature engineering significantly improved model accuracy
•  ⁠Climate variables like temperature and rainfall were the strongest predictors of yield
