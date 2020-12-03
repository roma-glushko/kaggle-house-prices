# Experiment Notes

## Feature Selection & Engineering

Checked Features:

* LotConfig (MSE: -15M, MAE: -137)
* ExterCond (MSE: -1.3M, MAE: -10)
* ExterQualEnc (MSE: -5.5M, MAE: -15)
* HeatingQC (MSE: -2.2M, MAE: -24)
* Functional (MSE: -450k, MAE: -3)
* YearBuilt (MSE: -14M, MAE: -50)
* PavedDriveEnc (worse)

Engineered Features:

* TotalBathrooms (better)
* IsPavedDrive (worse)
* OverallHouseQCBin (worse)
* IsNeighborhoodElite (worse)

## Hyperparm Tuning

### XGBoost Model

#### XGB (max_depth=7, n_estimators=800, learning_rate=0.03, booster='gbtree') {CV=2, 0.14148}

- [CV] MSE: 1067244005.9819 (6786543.5300)
- [CV] MAE: 18585.0924 (529.1012)
- [CV] R^2: 0.8299 (0.0117)
- [CV] RMSLE: 0.146894

#### XGB (max_depth=8, n_estimators=300, learning_rate=0.06, min_child_weight=3, booster='gbtree') {CV=2, 0.13913}

- [CV] MSE: 864066837.6111 (54223012.6496)
- [CV] MAE: 18005.2899 (967.4594)
- [CV] R^2: 0.8629 (0.0000)
- [CV] RMSLE: 0.140989

## XGB (max_depth=8, n_estimators=200, learning_rate=0.06, min_child_weight=3, booster='gbtree', subsample=0.7, gamma=0) {CV=2, 0.13494}

- [CV] MSE: 782138754.8110 (37985553.8400)
- [CV] MAE: 16999.5631 (458.6830)
- [CV] R^2: 0.8758 (0.0017)
- [CV] RMSLE: 0.133976

## XGB (max_depth=3, n_estimators=500, learning_rate=0.07, min_child_weight=3, objective='reg:gamma', booster='gbtree', subsample=0.7, gamma=0.02) {CV=2, 0.13542}

Model starts to overfit. It seems to relate to reducing max_depth param.

- [CV] MSE: 737521183.3120 (60451371.5640)
- [CV] MAE: 16499.2829 (795.1411)
- [CV] R^2: 0.8831 (0.0023)
- [CV] RMSLE: 0.129336

## XGB (max_depth=2, n_estimators=800, learning_rate=0.07, min_child_weight=1, objective='reg:gamma', booster='gbtree', subsample=0.8, gamma=0.02) {CV=2, 0.13620}

The same overfitting effect can be seen for this set of params.

- [CV] MSE: 672593417.6297 (69417924.6645)
- [CV] MAE: 16345.5821 (856.6857)
- [CV] R^2: 0.8935 (0.0044)
- [CV] RMSLE: 0.127799

## XGB (max_depth=5, n_estimators=2000, learning_rate=0.04, min_child_weight=2, subsample=0.7, gamma=0.03, objective='reg:gamma', booster='gbtree') {CV=2, 0.13543}

- [CV] MSE: 720217763.9437 (76727068.2702)
- [CV] MAE: 16300.2146 (788.1942)
- [CV] R^2: 0.8860 (0.0051)
- [CV] RMSLE: -0.129308

# Best Model: XGB (max_depth=4, n_estimators=7000, learning_rate=0.01, min_child_weight=1.5, subsample=0.2, gamma=0, reg_alpha=1, reg_lambda=0.1, booster='gbtree') {CV=2, 0.13105}

- [CV] MSE: 782885721.1446 (6743520.5426)
- [CV] MAE: 16302.8672 (471.5882)
- [CV] R^2: 0.8754 (0.0067)
- [CV] RMSLE: -0.130275 (0.0048)
