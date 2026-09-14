# Week 1 Summary - Exploration Phase

**Week Number**: 1/13  
**Phase**: Exploration  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 7
- **Best Performer**: F5 (Chemical Yield) at 2596.24
- **Total Weekly Gain**: 2596.99
- **Average Prediction Error**: 55.25%
- **Technique Mix**: GP×7, NN+GP×1

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.961701, 0.530632]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 5.940e-80 ± 5.940e-80 → 1.320e-79 (55.00% error)
- **Interpretation**: Week 1 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Baseline confirms the response is essentially flat. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.805998, 0.976911]
- **Technique**: GP with RQ kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.4026 ± 0.1387 → 0.272 (48.00% error)
- **Interpretation**: Week 1 improved the incumbent; cumulative improvement from week 1 is 0
- **Insight**: A usable low-dimensional ridge appears immediately. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.958413, 0.000000, 0.155798]
- **Technique**: GP with Matern kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.0505 ± 0.052 → -0.099 (49.00% error)
- **Interpretation**: Week 1 improved the incumbent; cumulative improvement from week 1 is 0
- **Insight**: Negative outputs indicate the search is still in poor regions. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.441123, 0.411738, 0.494631, 0.342777]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -1.3047 ± 0.4169 → -0.772 (69.00% error)
- **Interpretation**: Week 1 improved the incumbent; cumulative improvement from week 1 is 0
- **Insight**: The initial 4D fit is underpowered and noisy. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.463189, 0.894624, 1.000000, 0.847079]
- **Technique**: GP with RQ kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 2388.54 ± 1401.97 → 2596.24 (8.00% error)
- **Interpretation**: Week 1 improved the incumbent; cumulative improvement from week 1 is 0
- **Insight**: The project’s strongest signal appears in week 1. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.534805, 0.797728, 0.583763, 0.631959, 0.956318]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.0358 ± 0.6616 → -1.192 (97.00% error)
- **Interpretation**: Week 1 improved the incumbent; cumulative improvement from week 1 is 0
- **Insight**: The first recipe query lands in a noisy low-value region. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.902056, 0.647237, 0.772125, 0.611816, 0.143151, 0.652780]
- **Technique**: GP with Matern+White kernel and UCB (Beta=1.0)
- **Prediction vs Actual**: 0.3884 ± 0.2668 → 0.468 (17.00% error)
- **Interpretation**: Week 1 improved the incumbent; cumulative improvement from week 1 is 0
- **Insight**: Balanced GP-UCB works surprisingly well for 6D. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.038035, 0.409881, 0.055322, 0.560541, 0.868601, 0.450918, 0.304014, 0.440225]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 6.000e-5 ± 0.0036 → 0.006 (99.00% error)
- **Interpretation**: Week 1 improved the incumbent; cumulative improvement from week 1 is 0
- **Insight**: The opening ensemble badly overestimates this 8D landscape. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 1 fits that pattern through a exploration-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: None yet
- **Still actively searching**: F1, F2, F3, F4, F5, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F1 | Beta | 3.0 | 5.0 | Raised beta to increase exploration pressure after weak early gains. |
| F2 | Acquisition | UCB | EI | Acquisition changed from UCB to EI to match the phase transition. |
| F3 | Beta | 3.0 | 5.0 | Raised beta to increase exploration pressure after weak early gains. |
| F5 | Acquisition | UCB | EI | Acquisition changed from UCB to EI to match the phase transition. |
| F6 | Beta | 3.0 | 5.0 | Raised beta to increase exploration pressure after weak early gains. |
| F7 | Beta | 1.0 | 3.0 | Raised beta to increase exploration pressure after weak early gains. |
| F8 | Technique | NN+GP | GP | Shifted to GP to better match the observed landscape. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
