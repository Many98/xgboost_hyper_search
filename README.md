# XGboost hyperparameter search in R
## Design & Analysis framework

(Optimally open notebook in Google Colab)

Protocol is written in Slovak language


## Introduction

In this protocol, our goal is to find the optimal hyperparameter setting for the XGBoost algorithm using 2^(8-2) experimental design instead of the classical grid-search approach.
Specifically, we try to predict the price of apartments in CZK based on tabular data. The prepared dataset contains a total of 8191 samples, while 85% (6962) of the data were used for training and the remaining 15% (1229) for testing the predictive properties of the model.
The evaluated metric is the mean absolute error (MAE) over the test dataset (in CZK units).


## Highlights
![main_effects](https://github.com/Many98/xgboost_hyper_search/assets/65658910/26f1b7aa-5920-4d08-b049-c26ebba80ce2)
![surface_a](https://github.com/Many98/xgboost_hyper_search/assets/65658910/46f9d3f5-63a5-415f-b8d6-e707ad5a376a)

![surface_3d](https://github.com/Many98/xgboost_hyper_search/assets/65658910/6462121c-cb1c-4c69-99d5-397e8d6e33bc)


## Conclusions

In the protocol, we set ourselves the goal of optimizing the hyperparameter values of the XGBoost algorithm in such a way as to obtain the lowest possible value of the MAE test metric.
For the design of the experiment, we chose a 2^(8-2) design and thus a total of 64 observations were measured. Due to the additional requirements of the model, we performed 5 replicate measurements 
at the central point as well as 16 unreplicated measurements using the central composite design.

Through qualitative and quantitative analysis, we found that MAE significantly depended on the factors colsample_bytree, colsample_bynode, subsample, max_depth, n_estimators and also their interactions.
Using measurements at the central points, we found that the dependence is even quadratic in the colsample_bynode and max_depth factors.

In the end, the quadratic model turned out to be an adequate but not sufficient approximation of the real process, while with its help we were able to 
discover a kind of optimal setting of the hyperparameters, with which we arrived at a MAE equal to 88,499. On the other hand, using the randomized search approach,
a much better setting of the hyperparameters was discovered, which gave the MAE value is equal to 67,747. But this corresponds to the expectations that the dependence
of the MAE metric on the hyperparameters of the XGBoost algorithm will be at least complex, and thus the use of a quadratic surface for its approximation will not bring significant success.

We would therefore recommend the use of factorial design for finding hyperparameters of the XGBoost algorithm only in the case of extremely limited resources, especially in terms of computing power.
