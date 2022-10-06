--- 
layout: page
title: Preprocessing: One-Hot Encoding 
permalink: /rankedterciles/
---

# Preprocessing: One-Hot Encoding 
### xc.RankedTerciles ([source code](https://github.com/kjhall01/xcast/blob/b1764eaa1bfaf17c85447f6571caf016a13b2915/src/preprocessing/onehot.py#L44)) 

This is a transformer class which “one-hot encodes” the data provided based on tercile categories defined by the 33rd and 66th percentiles of the data along the sample dimension. 

It uses all the same methods and attributes as the other transformer classes, generally. 
