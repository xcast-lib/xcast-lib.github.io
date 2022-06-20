---
layout: page
title: Docs: Verification
permalink: /verification/ 
---

# Docs: Skill Verification
XCast implements a broad array of skill metrics, both probabilistic and deterministic. They should be used with Cross-validated prediction datasets, produced with the XCast CrossValidator class, for example. But they can also be used to verify the raw skill of GCM's and other things. Largely, they accept two positional arguments, the predicted dataarray, and the observed dataarray, and compare them. They also accept dimension name keyword arguments for both data arrays. Here is a list of the ones available: 

```
BrierScoreLoss(predicted, observed)
BrierScore(predicted, observed)
RankProbabilityScore(predicted, observed)
ContinuousRankProbabilityScore(predicted, observed)
Ignorance(predicted, observed)
PointBiserialCorrelation(predicted, observed)
HansenKuiper(predicted, observed)
MeanAbsolutePercentError(predicted, observed)
KendallsTau(predicted,observed)
BayesianInformationCriterion(predicted, observed)
AkaikeInformationCriterion(predicted, observed)
LogLikelihood(predicted, observed)
RocAuc(predicted, observed)
GeneralizedROC(predicted, observed)
F1(predicted, observed)
AveragePrecision(predicted, observed)
IndexOfAgreement(predicted, observed)
NashSutcliffeEfficiency(predicted, observed)
NormalizedNashSutcliffeEfficiency(predicted, observed)
KlingGuptaEfficiency(predicted, observed, sr=1, sa=1, sb=1)
KlingGuptaComponents(predicted, observed, sr=1, sa=1, sb=1, component='all' )
Spearman(predicted, observed)
SpearmanP(predicted, observed)
Pearson(predicted, observed)
PearsonP(predicted, observed)
```
