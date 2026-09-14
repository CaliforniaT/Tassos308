# Week 5 Summary - Balanced Phase

**Week Number**: 5/13  
**Phase**: Balanced  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 6
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 1.444
- **Average Prediction Error**: 31.25%
- **Technique Mix**: GP×6, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.806578, 0.709155]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.072e-80 ± 5.412e-80 → 1.320e-79 (54.00% error)
- **Interpretation**: Week 5 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: The flat prior is stable enough to stop spending exploratory budget. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.872606, 0.951575]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.825 ± 0.1275 → 0.75 (10.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.478
- **Insight**: A local peak near 0.75 appears to be established. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.840671, 0.058900, 0.122437]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0504 ± 0.0292 → -0.08 (37.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.019
- **Insight**: Another tiny gain suggests exploration is still worthwhile. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.462546, 0.456895, 0.466260, 0.373764]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.9419 ± 0.2138 → -0.668 (41.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.104
- **Insight**: Filtered candidates continue producing steady gains. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.352453, 0.827757, 0.804209, 0.868736]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6778.00 ± 1060.90 → 7367.39 (8.00% error)
- **Interpretation**: Week 5 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: The search is effectively locked around the best-yield composition. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.456709, 0.762115, 0.528274, 0.613825, 0.950449]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2992 ± 0.255 → -0.68 (56.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.512
- **Insight**: The hybrid pipeline produces steadier improvements than raw GP. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.791704, 0.611952, 0.768246, 0.605814, 0.196659, 0.615919]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.5208 ± 0.1922 → 0.62 (16.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.152
- **Insight**: The incumbent is now clearly inside a productive basin. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.121502, 0.422634, 0.092003, 0.529597, 0.863298, 0.504913, 0.320011, 0.520898]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 3.24 ± 2.07 → 4.5 (28.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 4.494
- **Insight**: F8 is still far from converged, but the trend is finally positive. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 5 fits that pattern through a balanced-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5
- **Still actively searching**: F3, F4, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 6

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F2 | Strategy mode | Plateau | Locked | Operational mode changed from Plateau to Locked based on the latest evidence. |
| F3 | Strategy mode | Exploration | Slow | Operational mode changed from Exploration to Slow based on the latest evidence. |
| F8 | Strategy mode | Exploration | Steady | Operational mode changed from Exploration to Steady based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
