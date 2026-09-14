# Week 6 Summary - Balanced Phase

**Week Number**: 6/13  
**Phase**: Balanced  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 5
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 1.387
- **Average Prediction Error**: 29.62%
- **Technique Mix**: GP×6, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.793225, 0.773184]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.600e-80 ± 4.620e-80 → 1.320e-79 (50.00% error)
- **Interpretation**: Week 6 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Model variance is dropping even though performance is unchanged. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.871663, 0.946012]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.815 ± 0.1122 → 0.7478 (9.00% error)
- **Interpretation**: Week 6 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Repeat exploitation confirms the optimum neighbourhood. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.841092, 0.074662, 0.158492]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0499 ± 0.0269 → -0.078 (36.00% error)
- **Interpretation**: Week 6 improved the incumbent; cumulative improvement from week 1 is 0.021
- **Insight**: Noise and modality keep improvements modest. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.557800, 0.496244, 0.454924, 0.395714]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.8868 ± 0.1914 → -0.638 (39.00% error)
- **Interpretation**: Week 6 improved the incumbent; cumulative improvement from week 1 is 0.134
- **Insight**: The same hybrid configuration keeps paying off. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.348422, 0.828079, 0.794610, 0.876158]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6831.12 ± 1057.72 → 7345.29 (7.00% error)
- **Interpretation**: Week 6 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: No alternative candidate clears the incumbent. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.443225, 0.747936, 0.505336, 0.547671, 0.934342]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.299 ± 0.2307 → -0.65 (54.00% error)
- **Interpretation**: Week 6 improved the incumbent; cumulative improvement from week 1 is 0.542
- **Insight**: Noise tolerance adjustments keep paying off. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.741926, 0.558718, 0.714118, 0.590574, 0.246038, 0.550855]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.5483 ± 0.187 → 0.645 (15.00% error)
- **Interpretation**: Week 6 improved the incumbent; cumulative improvement from week 1 is 0.177
- **Insight**: Week 6 keeps nudging the best configuration upward. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.142090, 0.416063, 0.097182, 0.499344, 0.836532, 0.512204, 0.413894, 0.589107]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 4.234 ± 2.436 → 5.8 (27.00% error)
- **Interpretation**: Week 6 improved the incumbent; cumulative improvement from week 1 is 5.794
- **Insight**: Consistent gains show the search is learning the manifold. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 6 fits that pattern through a balanced-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5
- **Still actively searching**: F3, F4, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F1 | Strategy mode | Converged | Locked | Operational mode changed from Converged to Locked based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
