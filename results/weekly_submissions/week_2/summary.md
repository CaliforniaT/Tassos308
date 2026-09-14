# Week 2 Summary - Exploration Phase

**Week Number**: 2/13  
**Phase**: Exploration  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 7
- **Best Performer**: F5 (Chemical Yield) at 3486.10
- **Total Weekly Gain**: 891.05
- **Average Prediction Error**: 37.88%
- **Technique Mix**: GP×8

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.851213, 0.592722]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.600e-80 ± 6.204e-80 → 1.320e-79 (50.00% error)
- **Interpretation**: Week 2 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Higher beta explores more space but does not improve the incumbent. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.750163, 0.977047]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.6431 ± 0.158 → 0.545 (18.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.273
- **Insight**: Switching to EI captures the first major gain. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.859917, 0.085835, 0.069563]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0505 ± 0.037 → -0.087 (42.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.012
- **Insight**: A less-negative point confirms there are gentler basins nearby. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.509677, 0.466074, 0.421590, 0.433979]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -1.1858 ± 0.306 → -0.765 (55.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.007
- **Insight**: Only a minor gain appears before filtering is introduced. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.436074, 0.840454, 0.944685, 0.962132]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 3172.35 ± 627.50 → 3486.10 (9.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 889.86
- **Insight**: EI immediately converts the F5 signal into a larger win. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.581274, 0.745316, 0.630935, 0.632302, 0.918121]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2274 ± 0.3695 → -0.812 (72.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.38
- **Insight**: A better 5D region is found, but noise remains severe. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.836468, 0.621469, 0.744310, 0.665838, 0.050753, 0.541308]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.422 ± 0.1928 → 0.521 (19.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.053
- **Insight**: A moderate beta improves the incumbent without over-exploring. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.112556, 0.334127, 0.003647, 0.595385, 0.902912, 0.376000, 0.391210, 0.466087]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 0.2914 ± 0.2444 → 0.47 (38.00% error)
- **Interpretation**: Week 2 improved the incumbent; cumulative improvement from week 1 is 0.464
- **Insight**: A simpler GP recovers a meaningful improvement immediately. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 2 fits that pattern through an exploration-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1
- **Still actively searching**: F2, F3, F4, F5, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 3

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F1 | Strategy mode | Plateau | Converged | Operational mode changed from Plateau to Converged based on the latest evidence. |
| F2 | Strategy mode | Switching | Exploitation | Operational mode changed from Switching to Exploitation based on the latest evidence. |
| F4 | Strategy mode | Exploration | SVM_Prep | Operational mode changed from Exploration to SVM_Prep based on the latest evidence. |
| F5 | Xi | 0.01 | 0.001 | Lower xi tightened EI around the current incumbent to prioritize near-term gains. |
| F8 | Strategy mode | Recovery | Exploration | Operational mode changed from Recovery to Exploration based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
