---
layout: page
title: reliability_diagram
permalink: /reliability_diagram/
---

reliability_diagram calculates and plots the reliability diagram between two NumPy arrays, one of which represnets a probabilty forecast and one of which represents one-hot encoded observations for reference. 

```
reliability_diagram(
  ypred,  # probability predictions for one category. Nx1 column vector please
  t,      # one-hot encoded observations for one category. Nx1 column vector
  title=None,  # plot title 
  tercile_skill_area=True,   # plot gray polygons over skillful area for tercile forecasts
  perfect_reliability_line=True,    # plots a line representing theoretical perfect reliability
  plot_hist=True,                # plot histogram of predicted probabilities 
  fig=None,          # use existing fig?
  ax=None,           # use existing ax? 
  bin_minimum_pct=0.01,  # minimum percent of predicted values falling into a given bin in order to calculate reliability for that bin
  scores=True        # plot BSS, REL, RES as numeric values on plot 
)
```
