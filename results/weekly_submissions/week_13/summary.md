# Week 13 Summary - Exploitation Phase

**Week Number**: 13/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.2305
- **Average Prediction Error**: 19.88%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.791120, 0.768550]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 9.240e-80 ± 1.452e-80 → 1.320e-79 (30.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Final check confirms F1 never meaningfully improves from baseline. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.867574, 0.959468]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7777 ± 0.0823 → 0.7478 (4.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Final week preserves the 0.75 solution without regression. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.698685, 0.184532, 0.241608]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0524 ± 0.0128 → -0.069 (24.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 0.03
- **Insight**: Final output is still negative, but materially better than week 1. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.616764, 0.580597, 0.534020, 0.446072]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.5564 ± 0.0685 → -0.428 (30.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 0.344
- **Insight**: Final week keeps the slow SVM+GP climb intact. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.355135, 0.820919, 0.797716, 0.867342]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7124.93 ± 1028.34 → 7345.29 (3.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Final week preserves the week-3 peak without degradation. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.287271, 0.736489, 0.448052, 0.620415, 0.802186]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.246 ± 0.0881 → -0.41 (40.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 0.782
- **Insight**: Final week posts the best F6 value of the project. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.739395, 0.603511, 0.693016, 0.509855, 0.249339, 0.554076]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6329 ± 0.1169 → 0.6879 (8.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: Final week confirms a stable 0.69 best value. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.207046, 0.429096, 0.161496, 0.583470, 0.814591, 0.559000, 0.450814, 0.608814]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.872 ± 2.952 → 9.84 (20.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 9.834
- **Insight**: Final week records the project-best F8 output at 9.84. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 13 fits that pattern through a exploitation-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F3, F4, F5, F6, F7, F8
- **Still actively searching**: None
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale

No further hyperparameter changes are planned. Final week analysis confirmed that the incumbent settings already match the best available strategy for each function.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
