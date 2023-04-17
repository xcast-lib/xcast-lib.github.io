---
layout: page
title: ACPAC
permalink: /ACPAC/
---

# ACPAC 

ACPAC is an XCast estimator which implements the Anomaly Correlation and Probability Anomaly Correlation methods used by the CPC. It can produce deterministic forecasts and tercile probabilistic forecasts. It is best used with the individual members of a given climate model, rather than as a multi-model ensemble method. For more information, check [here](https://www.cpc.ncep.noaa.gov/products/people/wd51hd/vddoolpubs/AMS_JWAF_2017_199-206_PACprobanomcorr.pdf)  

ACPAC is not implemented as a subclass of BaseEstimator, but rather directly with Xarray operations. There are no hyperparameters to be tuned, as in EPO-ELM or other methods. It uses Anomaly Correlation to produce calibrated ensemble mean predictions (its `.predict` method), and Probability Anomaly Correlation to produce calibrated Member-Count based tercile probability forecasts (its `.predict_proba` method). It cannot be used for probabilty of non-exceedance predictions. 
