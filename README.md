# House Prices Advanced Regression Techniques
Vlad Tsiperko

**The objective of this repository was to conduct an analysis for Kaggle's competition: https://www.kaggle.com/c/house-prices-advanced-regression-techniques**

## Description

**Exploratory Data Analysis and Data Cleaning:**

1. Eliminated columns with 100% identical values ["Street", "Utilities"]
2. Removed outliers: GrLivArea exceeding 4500
3. Corrected values exceeding 2017 for "Year"
4. Handled missing numerical values:
 + Imputed LotFrontage based on median value in the specific neighborhood
 + Set constant = 0 for: ['BsmtFinSF1', 'BsmtFinSF2', 'BsmtFullBath', 'BsmtHalfBath', "MasVnrArea"]
 + Imputed remaining numerical columns (excluding the above) with the median
5. Transformed some numerical features treated as categorical: ['MSSubClass', 'OverallCond’]
6. Managed missing categorical values (specific to each feature)
7. Addressed skewness in features:
 + Log transformation for SalePrice
 + BoxCox transformation for other features with skewness > 0.5
10. Transformed specific categorical features with a defined order into numerical values

**Feature Engineering:**

1. Created feature Isgarage based on GarageArea (1 – if GarageArea > 0)
2. Created feature Isfireplace based on Fireplaces (1 – if Fireplaces > 0)
3. Created feature Ispool based on PoolArea (1 – if PoolArea > 0)
4. Created feature Issecondfloor based on 2ndFlrSF (1 – if 2ndFlrSF > 0)
5. Created feature IsOpenPorch based on OpenPorchSF (1 – if OpenPorchSF > 0)
6. Created feature IsWoodDeck based on WoodDeckSF (1 – if WoodDeckSF > 0)
7. Created feature TotalSqrtFeet as the sum of GrLivArea and TotalBsmtSF
8. Created feature TotalBaths as BsmtFullBath + FullBath + BsmtHalfBath/2 + HalfBath/2.
9. Transformed Neighborhood into 0, 1, 2 based on statistical data to represent the neighborhood's affluence level.
10. Applied One-Hot Encoding for categorical data

**Modeling:**

1. Used RobustScaler for scaling
2. Implemented various regression models:
 + Linear Regression
 + LASSO model selection
 + GradientBoostingRegressor
 + XGBRegressor
 + ElasticNet
 + LGBMRegressor
3. Trained models using StackingCVRegressor with models: [ElasticNet, XGB, LGBM]
4. Combined predictions with weights: 0.3 ElasticNet, 0.25 LGBM, 0.45 StackedModels