# Week 12 Summary - Exploitation Phase

**Week Number**: 12/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.2605
- **Average Prediction Error**: 21.12%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.790429, 0.765503]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.976e-80 ± 1.558e-80 → 1.320e-79 (32.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Confidence intervals are narrow and unchanged. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.859688, 0.956236]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7851 ± 0.0882 → 0.7478 (5.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Only tiny confirmation steps remain justified. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.733459, 0.169942, 0.239201]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0514 ± 0.0142 → -0.0695 (26.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 0.0295
- **Insight**: Week 12 suggests near-convergence without a full lock. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.601191, 0.565466, 0.532177, 0.437682]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.6 ± 0.0788 → -0.458 (31.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 0.314
- **Insight**: The hybrid model is close to fully converged. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.350215, 0.821925, 0.793550, 0.869913]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7124.93 ± 1028.34 → 7345.29 (3.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: All evidence supports a strict exploitation lock. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.304535, 0.746054, 0.459572, 0.616949, 0.812093]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2726 ± 0.1067 → -0.47 (42.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 0.722
- **Insight**: The function is nearly converged but still benefits from one more lock step. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.745500, 0.606615, 0.691131, 0.512706, 0.252877, 0.553638]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.626 ± 0.128 → 0.6879 (9.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: Convergence lock remains justified. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.191746, 0.439032, 0.170945, 0.580106, 0.837120, 0.543082, 0.419268, 0.605935]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.663 ± 2.9488 → 9.7 (21.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 9.694
- **Insight**: Week 12 indicates near-convergence in 8D. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 12 fits that pattern through a exploitation-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F4, F5, F6, F7
- **Still actively searching**: F3, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F1 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence. |
| F2 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence. |
| F3 | Strategy mode | Refinement | Final | Operational mode changed from Refinement to Final based on the latest evidence. |
| F4 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence. |
| F5 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence. |
| F6 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence. |
| F7 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence. |
| F8 | Strategy mode | Ensemble | Final | Operational mode changed from Ensemble to Final based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
