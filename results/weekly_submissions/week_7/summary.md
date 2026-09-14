# Week 7 Summary - Balanced Phase

**Week Number**: 7/13  
**Phase**: Balanced  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 5
- **Best Performer**: F5 (Chemical Yield) at 7345.29
- **Total Weekly Gain**: 1.185
- **Average Prediction Error**: 27.88%
- **Technique Mix**: GP×6, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.797551, 0.776111]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 7.260e-80 ± 3.300e-80 → 1.320e-79 (45.00% error)
- **Interpretation**: Week 7 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Lock mode begins: queries are now confirmation-only. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.856252, 0.945352]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.8076 ± 0.1062 → 0.7478 (8.00% error)
- **Interpretation**: Week 7 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: No nearby candidate beats the incumbent. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.778956, 0.092896, 0.164180]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0494 ± 0.0247 → -0.076 (35.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.023
- **Insight**: The incumbent keeps improving, but only by hundredths. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.565419, 0.502263, 0.470825, 0.378847]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.833 ± 0.1702 → -0.608 (37.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.164
- **Insight**: Balanced filtering still improves the incumbent each week. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.352350, 0.824579, 0.790645, 0.868203]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6904.57 ± 1057.72 → 7345.29 (6.00% error)
- **Interpretation**: Week 7 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Maintaining the incumbent is now the optimal decision. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.413451, 0.792240, 0.529235, 0.556427, 0.915735]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2976 ± 0.2077 → -0.62 (52.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.572
- **Insight**: Filtered exploration still finds small gains. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.726066, 0.615195, 0.726128, 0.572416, 0.277814, 0.517318]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.5745 ± 0.1804 → 0.668 (14.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.2
- **Insight**: By week 7 the function is close to its practical ceiling. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.077215, 0.434831, 0.063742, 0.528031, 0.827113, 0.554011, 0.406003, 0.516859]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 5.106 ± 2.76 → 6.9 (26.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 6.894
- **Insight**: Week 7 still improves, although more slowly. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 7 fits that pattern through a balanced-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5
- **Still actively searching**: F3, F4, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 8

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F4 | Strategy mode | SVM_Stable | Balanced | Operational mode changed from SVM_Stable to Balanced based on the latest evidence. |
| F6 | Strategy mode | SVM_Stable | Balanced | Operational mode changed from SVM_Stable to Balanced based on the latest evidence. |
| F7 | Strategy mode | Improving | Plateau | Operational mode changed from Improving to Plateau based on the latest evidence. |
| F8 | Technique | GP | NN+GP | Shifted to NN+GP to better match the observed landscape. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
