# Week 2 Summary - Exploration Phase

**Week Number**: 2/13  
**Phase**: Exploration  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 7
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 3486.10
- **Total Weekly Gain**: 891.05
- **Average Prediction Error**: 37.88%
- **Technique Mix**: GP×8

Week 2 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.851213, 0.592722]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.600e-80 ± 6.204e-80 → 1.320e-79 (50.00% error)
- **Interpretation**: Week 2 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Higher beta explores more space but does not improve the incumbent.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.750163, 0.977047]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.6431 ± 0.158 → 0.545 (18.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.273
- **Insight**: Switching to EI captures the first major gain.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.859917, 0.085835, 0.069563]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0505 ± 0.037 → -0.087 (42.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.012
- **Insight**: A less-negative point confirms there are gentler basins nearby.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.509677, 0.466074, 0.421590, 0.433979]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -1.1858 ± 0.306 → -0.765 (55.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.007
- **Insight**: Only a minor gain appears before filtering is introduced.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.436074, 0.840454, 0.944685, 0.962132]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 3172.35 ± 627.50 → 3486.10 (9.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 889.86
- **Insight**: EI immediately converts the F5 signal into a larger win.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.581274, 0.745316, 0.630935, 0.632302, 0.918121]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2274 ± 0.3695 → -0.812 (72.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.38
- **Insight**: A better 5D region is found, but noise remains severe.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.836468, 0.621469, 0.744310, 0.665838, 0.050753, 0.541308]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.422 ± 0.1928 → 0.521 (19.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.053
- **Insight**: A moderate beta improves the incumbent without over-exploring.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.112556, 0.334127, 0.003647, 0.595385, 0.902912, 0.376000, 0.391210, 0.466087]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 0.2914 ± 0.2444 → 0.47 (38.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.464
- **Insight**: A simpler GP recovers a meaningful improvement immediately.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 2 is part of the exploration phase, so the allocation favors information-gathering and wider spacing.
- **Technique effectiveness**: GP contributed the largest share of this week's non-negative gains (891.05 across 8 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 9.00% error, while F6 was the hardest to predict at 72.00% error.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1
- **Still actively searching**: F2, F3, F4, F5, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 3

Function | Change | Old | New | Rationale
-------- | ------ | --- | --- | ---------
F1 | Strategy mode | Plateau | Converged | Week 3 plan: operational mode changed from Plateau to Converged based on the latest evidence.
F2 | Strategy mode | Switching | Exploitation | Week 3 plan: operational mode changed from Switching to Exploitation based on the latest evidence.
F4 | Strategy mode | Exploration | SVM_Prep | Week 3 plan: operational mode changed from Exploration to SVM_Prep based on the latest evidence.
F5 | Xi | Xi=0.01 | Xi=0.001 | Week 3 plan: lower xi tightened EI around the current incumbent to prioritize near-term gains.
F8 | Strategy mode | Recovery | Exploration | Week 3 plan: operational mode changed from Recovery to Exploration based on the latest evidence.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
