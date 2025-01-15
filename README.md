# [CMI-PIU: Actigraphy data EDA](https://www.kaggle.com/code/antoninadolgorukova/cmi-piu-actigraphy-data-eda)

This notebook explores working with ___actigraphy time series___ recordings to get an idea of the data at hand.
* Investigate ___data quality___ (e.g., time gaps, non-wear periods, battery issues)
* Calculate main statistics for all participants
* Derive meaningful ___insights___ for feature engineering (circadian rhythms, time-based activity trends, activity levels, etc.)

# [CMI | Features EDA](https://www.kaggle.com/code/antoninadolgorukova/cmi-piu-features-eda)

## Understanding the task

The aim of this competition is to ___predict___ the ___Severity Impairment Index___ __(sii)__, which measures the level of problematic internet use among children and adolescents, based on __physical activity data__ and __other features__.
__sii__ is derived from __PCIAT-PCIAT_Total__, the sum of scores from the ___Parent-Child Internet Addiction Test (PCIAT: 20 questions, scored 0-5).___

__Target Variable (sii)__ is defined as:

* 0: None (PCIAT-PCIAT_Total from 0 to 30)
* 1: Mild (PCIAT-PCIAT_Total from 31 to 49)
* 1：轻度（PCIAT-PCIAT_Total 从 31 到 49）
* 2: Moderate (PCIAT-PCIAT_Total from 50 to 79)
* 3: Severe (PCIAT-PCIAT_Total 80 and more)

This makes sii an ordinal categorical variable with four levels, where the order of categories is meaningful.

Type of Machine Learning Problem we can use with sii as a target:

* Ordinal classification (ordinal logistic regression, models with custom ordinal loss functions)
* [__Multiclass classification__](https://www.kaggle.com/code/tubotubo/starter-notebook-multi-target-prediction/notebook) treat sii as a nominal categorical variable without considering the order)
* Regression (ignore the discrete nature of categories and treat sii as a continuous variable, then round prediction)
* Custom (e.g. loss functions that penalize errors based on the distance between categories)

We can also use PCIAT-PCIAT_Total as a continuous target variable, and implement regression on PCIAT-PCIAT_Total and then map predictions to sii categories.

Finally, another strategy involves predicting responses to each question of the Parent-Child Internet Addiction Test: i.e. pedict individual question scores as separate targets, sum the predicted scores to get the PCIAT-PCIAT_Total and map predictions to the corresponding sii category.

# [CMI | EDA which makes sense](https://www.kaggle.com/code/ambrosm/piu-eda-which-makes-sense#A-look-at-selected-other-features)

* a first analysis of the data

* how to ___cross-validate___ a model

* that ___regression___ models are better than ___classification___ models in this competition, and

* how to ___tune the thresholds for rounding the regression output___.

* The notebook uses ___polars___ DataFrames. If you are more fluent with pandas than with polars, this is an opportunity to get to know polars, which is often more ___efficient than pandas___.

# [CMI | Best Single Model](https://www.kaggle.com/code/abdmental01/cmi-best-single-model)

# [CMI | 1st Place Solution](https://www.kaggle.com/code/lennarthaupts/1st-place-cmi-model-v4-1-1-reduced/notebook?scriptVersionId=213769368)

voted ensemble consisting of:
(improving the robustness)

* __LGBMRegressor__

* __Two__[__XGBoost__](https://www.kaggle.com/code/prashant111/a-guide-on-xgboost-hyperparameters-tuning)__Regressors__

* __CatBoostRegressor__ 

* __ExtraTreesRegressor__
