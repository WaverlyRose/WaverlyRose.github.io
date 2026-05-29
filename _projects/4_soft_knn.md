---
layout: page
title: Soft-kNN ICU Mortality
description: Subgroup-fair calibration for ICU mortality prediction on MIMIC-IV
img: assets/img/projects/soft-knn.jpg
importance: 4
category: current
---

{% include figure.liquid loading="eager" path="assets/img/projects/soft-knn.jpg" title="ICU physiological monitoring" class="img-fluid rounded z-depth-1" %}

ICU mortality prediction models on MIMIC-IV routinely exhibit calibration gaps across demographic subgroups; race in particular shows a recurring worst-group AUROC floor that standard imputation methods don't help close. This project tests whether soft-kNN imputation combined with propensity-weighted training can raise that floor without sacrificing aggregate performance.

Approach. Combines soft-kNN imputation with propensity-weighted training, then evaluates whether this raises the worst-group AUROC floor without degrading aggregate performance. 

**Status.** Manuscript in preparation. Target venue: AAAI 2027 (full paper deadline late July). CHIL 2027 as backup.
