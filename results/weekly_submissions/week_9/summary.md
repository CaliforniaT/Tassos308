# Week 9 Summary - Exploitation Phase

**Week Number**: 9/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer**: F5 (Chemical Yield) at 7345.29
- **Total Weekly Gain**: 0.762
- **Average Prediction Error**: 25.00%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.793600, 0.762194]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.052e-80 ± 2.244e-80 → 1.320e-79 (39.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: No hidden ridge emerges despite wider spacing from previous queries. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.862960, 0.955355]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7926 ± 0.0972 → 0.7478 (6.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Late exploitation supports a stable convergence claim. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.769726, 0.139686, 0.191522]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.049 ± 0.0191 → -0.072 (32.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 0.027
- **Insight**: Refined candidates keep trimming the loss. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.564185, 0.508290, 0.512953, 0.416097]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.7343 ± 0.1206 → -0.548 (34.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 0.224
- **Insight**: The weekly gain persists even in lower-uncertainty regions. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.354057, 0.823519, 0.794210, 0.874750]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6978.02 ± 1028.34 → 7345.29 (5.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Exploration would only add risk at this point. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.378262, 0.756279, 0.503823, 0.607961, 0.846561]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2912 ± 0.154 → -0.56 (48.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 0.632
- **Insight**: The incumbent is still moving, but only gradually. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.740001, 0.602306, 0.692659, 0.513179, 0.247388, 0.553344]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6054 ± 0.1445 → 0.6879 (12.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: Repeated confirmation suggests the plateau is real. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.169018, 0.418711, 0.114834, 0.569631, 0.851195, 0.517822, 0.399628, 0.594791]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 6.46 ± 2.89 → 8.5 (24.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 8.494
- **Insight**: Late-stage ensemble refinement keeps adding value. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 9 fits that pattern through a exploitation-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5, F7
- **Still actively searching**: F3, F4, F6, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 10

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F3 | Strategy mode | Slow | Refinement | Operational mode changed from Slow to Refinement based on the latest evidence. |
| F4 | Strategy mode | Balanced | Locked | Operational mode changed from Balanced to Locked based on the latest evidence. |
| F6 | Strategy mode | Balanced | Refinement | Operational mode changed from Balanced to Refinement based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
