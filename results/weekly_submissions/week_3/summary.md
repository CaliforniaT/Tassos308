# Week 3 Summary - Exploration Phase

**Week Number**: 3/13  
**Phase**: Exploration  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 7
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 3883.06
- **Average Prediction Error**: 33.88%
- **Technique Mix**: GP×8

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.872699, 0.566571]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.336e-80 ± 5.940e-80 → 1.320e-79 (52.00% error)
- **Interpretation**: Week 3 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Three weeks of evidence suggest the ceiling is already known. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.799533, 0.966298]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.719 ± 0.1477 → 0.642 (12.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.37
- **Insight**: The EI policy keeps climbing the same smooth basin. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.922525, 0.094332, 0.045085]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0521 ± 0.034 → -0.084 (38.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.015
- **Insight**: The surrogate is finding small improvements but no breakthrough. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.442320, 0.455209, 0.460455, 0.362047]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -1.0774 ± 0.2766 → -0.728 (48.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.044
- **Insight**: Week 3 data is sufficient to activate SVM screening. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.420720, 0.771945, 0.777954, 0.958550]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6925.35 ± 1178.78 → 7367.39 (6.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 4771.15
- **Insight**: Week 3 discovers the global project peak. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.459688, 0.742674, 0.451417, 0.555038, 1.000000]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2632 ± 0.3271 → -0.752 (65.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.44
- **Insight**: Small progress suggests the signal is recoverable with more data. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.761954, 0.572561, 0.889852, 0.522332, 0.084248, 0.677069]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.46 ± 0.1963 → 0.561 (18.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 0.093
- **Insight**: The same policy keeps extracting reliable gains. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.096569, 0.417061, 0.000000, 0.563884, 0.934832, 0.434540, 0.419746, 0.543713]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 1.36 ± 1 → 2 (32.00% error)
- **Interpretation**: Week 3 improved the incumbent; cumulative improvement from week 1 is 1.994
- **Insight**: High-dimensional exploration begins to uncover structure. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 3 fits that pattern through a exploration-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1
- **Still actively searching**: F2, F3, F4, F5, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F4 | Technique | GP | SVM+GP | Shifted to SVM+GP to better match the observed landscape. |
| F5 | Strategy mode | Peak | Plateau | Operational mode changed from Peak to Plateau based on the latest evidence. |
| F6 | Technique | GP | SVM+GP | Shifted to SVM+GP to better match the observed landscape. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
