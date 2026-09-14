# Week 3 Summary - Exploration Phase

**Week Number**: 3/13  
**Phase**: Exploration  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 7
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 3883.06
- **Average Prediction Error**: 33.88%
- **Technique Mix**: GP×8

Week 3 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.872699, 0.566571]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.336e-80 ± 5.940e-80 → 1.320e-79 (52.00% error)
- **Interpretation**: Week 3 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Three weeks of evidence suggest the ceiling is already known.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.799533, 0.966298]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.719 ± 0.1477 → 0.642 (12.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.37
- **Insight**: The EI policy keeps climbing the same smooth basin.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.922525, 0.094332, 0.045085]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0521 ± 0.034 → -0.084 (38.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.015
- **Insight**: The surrogate is finding small improvements but no breakthrough.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.442320, 0.455209, 0.460455, 0.362047]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -1.0774 ± 0.2766 → -0.728 (48.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.044
- **Insight**: Week 3 data is sufficient to activate SVM screening.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.420720, 0.771945, 0.777954, 0.958550]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6925.35 ± 1178.78 → 7367.39 (6.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 4771.15
- **Insight**: Week 3 discovers the global project peak.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.459688, 0.742674, 0.451417, 0.555038, 1.000000]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2632 ± 0.3271 → -0.752 (65.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.44
- **Insight**: Small progress suggests the signal is recoverable with more data.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.761954, 0.572561, 0.889852, 0.522332, 0.084248, 0.677069]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.46 ± 0.1963 → 0.561 (18.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.093
- **Insight**: The same policy keeps extracting reliable gains.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.096569, 0.417061, 0.000000, 0.563884, 0.934832, 0.434540, 0.419746, 0.543713]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 1.36 ± 1 → 2 (32.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 1.994
- **Insight**: High-dimensional exploration begins to uncover structure.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 3 is part of the exploration phase, so the allocation favors information-gathering and wider spacing.
- **Technique effectiveness**: GP contributed the largest share of this week's non-negative gains (3883.06 across 8 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 6.00% error, while F6 was the hardest to predict at 65.00% error.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1
- **Still actively searching**: F2, F3, F4, F5, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 4

Function | Change | Old | New | Rationale
-------- | ------ | --- | --- | ---------
F4 | Technique | GP + Matern+White | SVM+GP + Matern+White | Week 4 plan: shifted to SVM+GP to better match the observed landscape.
F5 | Strategy mode | Peak | Plateau | Week 4 plan: operational mode changed from Peak to Plateau based on the latest evidence.
F6 | Technique | GP + Matern+White | SVM+GP + Matern+White | Week 4 plan: shifted to SVM+GP to better match the observed landscape.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
