# Kaggle Competition: Ames House Sale Price

<img style="height: 450px" src="https://livability.com/sites/default/files/151SUBAME031.jpg" />

This repository contains explanatory data analysis and modeling of Ames house sale prices.
<a href="http://jse.amstat.org/v19n3/decock.pdf">Ames house database</a> is sale history of almost 3000 houses that were sold in Ames, Iowa from 2008 to 2010. Each lot is represented by 80 features that describe all aspects of the house:

- Living area, floor areas, number of rooms, frontage, etc
- Neighborhood and Zoning
- Roof, masonry veneer, exterior properties
- Basement and fundament properties
- Air condition, heating, electrical properties
- Kitchen and bathroom properties
- Garage, porch, fireplace, fence, pool, wood deck properties

Competition Link: https://www.kaggle.com/c/house-prices-advanced-regression-techniques

## Content

- index.ipynb - a domain-driven explanatory data analysis with a focus on feature meaning and value
- baseline-model.ipynb - a baseline modeling of house sale price using LinearRegression
- model.ipynb - house price modeling using XGBoost applied on various engineered features

features = num_features + enc_cat_features + ['SalePrice']

frontage_corr_df = pd.DataFrame()
frontage_corr_df['feature'] = num_features + enc_cat_features
frontage_corr_df['corralation'] = [train_df[feature].corr(train_df['LotFrontage'], 'spearman') for feature in features]
frontage_corr_df.sort_values('corralation', ascending=[0], inplace=True)

plt.figure(figsize=(6, 0.25 * len(features)))
sns.barplot(data=frontage_corr_df, y='feature', x='corralation', orient='h')