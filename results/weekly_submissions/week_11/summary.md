# Week 11 Summary - Exploitation Phase

**Week Number**: 11/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.361
- **Average Prediction Error**: 22.38%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.796848, 0.759388]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.712e-80 ± 1.716e-80 → 1.320e-79 (34.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Only incumbent verification remains worthwhile. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.865764, 0.961414]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7851 ± 0.0912 → 0.7478 (5.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: The posterior mean and reality are now tightly aligned. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.728810, 0.172682, 0.228529]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0504 ± 0.0158 → -0.07 (28.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 0.029
- **Insight**: The model is finally calibrated enough to make conservative refinements. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.584833, 0.556393, 0.523242, 0.435510]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.6442 ± 0.0878 → -0.488 (32.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 0.284
- **Insight**: Late-stage runs mostly validate the filtered basin. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.349666, 0.819743, 0.792373, 0.872022]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7051.48 ± 1028.34 → 7345.29 (4.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: The best F5 settings remain untouched. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.314199, 0.741374, 0.449952, 0.603488, 0.834681]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.28 ± 0.1175 → -0.5 (44.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 0.692
- **Insight**: The best recipe is improving by fractions now. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.742610, 0.603390, 0.690088, 0.512750, 0.245374, 0.549943]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6191 ± 0.1335 → 0.6879 (10.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: No late-stage challenger outperforms the incumbent. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.196079, 0.415522, 0.138260, 0.591276, 0.841118, 0.544823, 0.444649, 0.605435]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.41 ± 2.964 → 9.5 (22.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 9.494
- **Insight**: Only small gains remain available. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 11 fits that pattern through a exploitation-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F4, F5, F7
- **Still actively searching**: F3, F6, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F6 | Strategy mode | Refinement | Locked | Operational mode changed from Refinement to Locked based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
