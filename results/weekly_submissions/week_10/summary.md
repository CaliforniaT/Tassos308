# Week 10 Summary - Exploitation Phase

**Week Number**: 10/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.761
- **Average Prediction Error**: 23.62%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.793311, 0.758831]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.448e-80 ± 1.980e-80 → 1.320e-79 (36.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: The surrogate is now reliable enough to avoid further speculative moves. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.863744, 0.954321]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7926 ± 0.0942 → 0.7478 (6.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Marginal value of further exploration is negligible. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.754025, 0.141481, 0.191659]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0497 ± 0.0174 → -0.071 (30.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 0.028
- **Insight**: A smaller step indicates the surface is flattening near the incumbent. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.567006, 0.543854, 0.513567, 0.431088]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.6889 ± 0.1036 → -0.518 (33.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 0.254
- **Insight**: The best placements are now clustered around one basin. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.349942, 0.819641, 0.791241, 0.871486]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7051.48 ± 1028.34 → 7345.29 (4.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Another validation run confirms stable high yield. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.334992, 0.761628, 0.456361, 0.608121, 0.844385]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2862 ± 0.1352 → -0.53 (46.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 0.662
- **Insight**: Later refinements are conservative and safer. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.740889, 0.601503, 0.698554, 0.514322, 0.248540, 0.549428]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6123 ± 0.139 → 0.6879 (11.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: The posterior mean is stable across nearby hyperparameter settings. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.159838, 0.400386, 0.125781, 0.555163, 0.833041, 0.539294, 0.414070, 0.592919]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.084 ± 2.944 → 9.2 (23.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 9.194
- **Insight**: The improvement rate slows as the search nears the best basin. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 10 fits that pattern through a exploitation-oriented allocation.
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

No further hyperparameter changes are planned. Final week analysis confirmed that the incumbent settings already match the best available strategy for each function.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
