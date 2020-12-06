# Experiment Notes

## Feature Selection & Engineering

Checked Features:

* LotConfig (MSE: -15M, MAE: -137)
* HeatingQC (worse, XGB: 0.009494662, RF: 0.023808127498479638(top11))
* Functional (MSE: -450k, MAE: -3)
* YearBuilt (MSE: -14M, MAE: -50)
* PavedDriveEnc (worse)
* ExterCondEnc (worse, XGB: 0.006350462, RF: 0.003081121534818516)
* ExterQualEnc (better on XGB, XGB: 0.07274425 (2nd), RF: 0.08696326852520005(top3))
* FenceEnc (worse, XGB: 0.0050089965, RF: 0.004011815652303977)
* SaleTypeEnc (better on XGB, XGB: 0.007627788872184359, RF: 0.007627788872184359)
* LandContour (better on XGB)
* MSZoning (better on XGB)

Engineered Features:

* HouseAge (better on XGB, XGB: 0.007173462, RF: 0.06902209972870232 (top6))
* IsHeatingGood (worse, XGB: 0.009311837, RF: 0.0009598728451529802)
* IsFunctional (XGB: 0.0075995293, RF: 0.0017536763182931518)
* IsLandFlat (possibly better on XGB, XGB: 0.005601142, RF: 0.003685766467293613)
* FunctionalGroup (better on XGB, XGB: 0.0075995293, RF: 0.0019032972545861358)
* HasFireplace (better, XGB: 0.049419753(top4), RF: 0.03368059526732552 (top10))
* Has2ndFloor (worse, XGB: 0.0, RF: 0.005902033492007415)
* HasShed (worse, XGB: 0.0040862192, RF: 0.0005317727959454998)
* HasPool (worse, XGB: 0.006932362, RF: 0.0022129987865685654)
* TotalBathrooms (better, XGB: 0.06028449(top3), RF: 0.06470293879494333 (top4))
* IsPavedDrive (worse; XGB: 0.008439384, RF: 0.002228173854555795)
* OverallHouseQCBin (worse; XGB: 0.021698037(top9), RF: 0.04860585701454716)
* IsNeighborhoodElite (worse, XGB: 0.0063309437, RF: 0.013367967603213125)
* YearBuiltBins (worse; XGB: 0.008516163, RF: 0.046843703819147264)
* KitchenQCBin (worse; XGB: 0.00507539, RF: 0.02899681308591065)
* IsModernHouseType (worse, XGB: 0.0056375926, RF: 0.015248809163328684)
* IsNewHouseSold (XGB: 0.005251049, RF: 0.004010564395201029)
* IsExterQualGood (better on XGB, XGB: 0.038813863 (top5), RF: 0.0004267454083208078)
* IsExterCondGood (worse, XGB: 0.015417073 (top13), RF: 0.0006292433208515044)

Features with little importance:

- Neighborhood_Blueste
- MSSubClass_150
- Condition2_RRNe
- Condition2_RRAn
- Condition2_RRAe
- Condition2_PosN
- Condition2_PosA
- Condition1_RRNe

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
