# Week 1 Summary - Exploration Phase

**Week Number**: 1/13  
**Phase**: Exploration  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 0
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 2596.24
- **Total Weekly Gain**: 0
- **Average Prediction Error**: 55.25%
- **Technique Mix**: GP×7, NN+GP×1

Week 1 shows F5 as the clearest current opportunity, while F8 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.961701, 0.530632]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 5.940e-80 ± 5.940e-80 → 1.320e-79 (55.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: Baseline confirms the response is essentially flat.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.805998, 0.976911]
- **Technique**: GP with RQ kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.4026 ± 0.1387 → 0.272 (48.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: A usable low-dimensional ridge appears immediately.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.958413, 0.000000, 0.155798]
- **Technique**: GP with Matern kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.0505 ± 0.052 → -0.099 (49.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: Negative outputs indicate the search is still in poor regions.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.441123, 0.411738, 0.494631, 0.342777]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -1.3047 ± 0.4169 → -0.772 (69.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: The initial 4D fit is underpowered and noisy.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.463189, 0.894624, 1.000000, 0.847079]
- **Technique**: GP with RQ kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 2388.54 ± 1401.97 → 2596.24 (8.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: The project’s strongest signal appears in week 1.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.534805, 0.797728, 0.583763, 0.631959, 0.956318]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.0358 ± 0.6616 → -1.192 (97.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: The first recipe query lands in a noisy low-value region.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.902056, 0.647237, 0.772125, 0.611816, 0.143151, 0.652780]
- **Technique**: GP with Matern+White kernel and UCB (Beta=1.0)
- **Prediction vs Actual**: 0.3884 ± 0.2668 → 0.468 (17.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: Balanced GP-UCB works surprisingly well for 6D.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.038035, 0.409881, 0.055322, 0.560541, 0.868601, 0.450918, 0.304014, 0.440225]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 6.000e-5 ± 0.0036 → 0.006 (99.00% error)
- **Interpretation**: Week 1 established the baseline; cumulative improvement from week 1 is 0
- **Insight**: The opening ensemble badly overestimates this 8D landscape.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 1 is part of the exploration phase, so the allocation favors information-gathering and wider spacing.
- **Technique effectiveness**: No method recorded an incumbent gain in week 1 because all eight runs were baseline-establishment queries; the main takeaway is that the standard GP configurations calibrated faster than the opening ensemble on F8.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 8.00% error, while F8 was the hardest to predict at 99.00% error.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: None yet
- **Still actively searching**: F1, F2, F3, F4, F5, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 2

Function | Change | Old | New | Rationale
-------- | ------ | --- | --- | ---------
F1 | Beta | Beta=3.0 | Beta=5.0 | Raised beta to search more broadly after the latest evidence showed the current model was still too uncertain.
F2 | Acquisition / parameter | UCB Beta=3.0 | EI Xi=0.01 | Acquisition changed from UCB to EI to better match the latest search objective.
F3 | Beta | Beta=3.0 | Beta=5.0 | Raised beta to search more broadly after the latest evidence showed the current model was still too uncertain.
F5 | Acquisition / parameter | UCB Beta=1.5 | EI Xi=0.01 | Acquisition changed from UCB to EI to better match the latest search objective.
F6 | Beta | Beta=3.0 | Beta=5.0 | Raised beta to search more broadly after the latest evidence showed the current model was still too uncertain.
F7 | Beta | Beta=1.0 | Beta=3.0 | Raised beta to search more broadly after the latest evidence showed the current model was still too uncertain.
F8 | Technique | NN+GP + Mixed | GP + Matern | Shifted to GP to better match the observed landscape.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
