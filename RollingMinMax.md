---
layout: page
title: RollingMinMax
permalink: /RollingMinMax/
---

# RollingMinMax

The RollingMinMax class applies min-max scaling to sub-seasonal data based on a "rolling window" of user-specified width. One should not use the standard MinMax class on data with multiple samples per year from a given season because, for example, when scaling two-week aggregated data from the NDJFM season, February and March values could follow entirely different distributions than November and December values. The minimum and maximum could be purely determined by the intra-seasonal variability, making the scalings somewhat nonsensical. The Rolling MinMax class accounts for this by doing the scaling separately at each week-in-year, plus/minus the window size. So rather than scaling all the February values as the highest, it will scale those separately from the other periods within the NDJFM season, based on the minimum and maximum of the February values only. The specific time period used to determine the min/max is defined by the window size in days specified by the user, centered at each sample. Each sample is encoded separately based on this window centered around it. For this reason, xarray.DataArrays passed to RollingMinMax must have sample-dimension coordinates convertible to pandas.Timestamp. 
The difference between this class and the standard MinMax class is that this class will separately scale each sample along the sample dimension. It will take any samples which, for any calendar year, fall into the day-in-year range defined by ( the coordinate of the given sample (say, initialization of June 1) plus `lead_low` (by default this is -7 to reflect one-week-prior to that sample in the year), and the coordinate of the given sample (say, initialization of June 1) plus `lead_high` (by default this is 7 to reflect one-week-post that sample in the year)

```
rmm = xc.RollingMinMax(
  lead_low=-7,  # defines the number of days prior to an initialization date to include in the min-max window 
  lead_high=7,  # defines the number of days post- an initialization date to include in the minmax window
  base_year=1999, # first year to search - make sure all your data falls between 1/1/base_year and 12/31/(base_year+n_years_to_search) 
  n_years_to_search=30
)
rmm.fit(X) 
Xmm = rmm.transform(X) # this could be X1, a dataset from a different year of the same format as X. T will have three features - one representing 'Below Normal (~1-33rd percentiles, one for 'Near Normal' (~34-66 percentiles), and one for 'Above Normal' (~67-99th percentiles) 
```

Note that RollingMinMax cannot inverse-transform in the way that the standard MinMax class can, for the foreseeable future.






