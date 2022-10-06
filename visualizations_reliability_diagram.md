---
layout: page
title: Visualizations: Reliability Diagram
permalink: /reliability_diagram/
---
# Visualizations: Reliability Diagram

### xc.reliability_diagram ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/core/visualization.py#L146))

This function plots the reliability diagram of a given tercile probabilistic forecast dataset. It operates on NumPy Arrays, not xarray data arrays and therefore the user needs to extract and reshape the predictions and one-hot encoded data from xarray to numpy before passing them to reliability_diagram. 
 
 
 
The reliability diagram plots the observed relative frequency of an event vs. the forecasted probability of that event, given a forecast of a certain level of confidence. Essentially, it splits all of the forecasts from the data provided up into ten bins according to how confident the probabilities are, (0-0.1, 0.1-0.2, 0.2-0.3, and so on to a highest confidence of 0.9-1). It then calculates the percentage of time the forecasted event actually occurred, given that the forecast was within each of those bins, and plots those percentages vs the forecasted probability.



The idea is that, if the forecast is well-calibrated, an event with a forecasted probability between 0.1-0.2 will only have happened between 10% and 20% of the time, but if the forecast made is 0.9-1, the event can be expected to occur between 90% and 100% of the time. It is a measure of how well the forecasted percentages can be trusted to represent the observed relative frequency of the event.



A diagonal line from bottom left to top right represents a well-calibrated forecast, where as horizontal line indicates no skill and a line reflecting climatological probability (for tercile forecasts, 33%) represents no resolution. 



This function also plots a histogram of the forecasted probabilities to give the user an idea of how often forecasts of each level of confidence are produced. 



Returns: 
- None 

Arguments: 
- ypred: an n x 1 numpy array of predicted probabilities between (0, 1) 
- ytrue: an n x 1 numpy array of binary-encoded observations 

Keyword Arguments: 
- Title: a string to use as the title of that plot. 

