# Week 4 Summary - Balanced Phase

**Week Number**: 4/13  
**Phase**: Balanced  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 6
- **Best Performer**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 1.359
- **Average Prediction Error**: 32.12%
- **Technique Mix**: GP×6, SVM+GP×2

This week continues the project-wide trajectory where low-dimensional functions stabilize early, F5 dominates once exploitation begins, and the highest-dimensional functions require the longest learning curve.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.834479, 0.666681]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.204e-80 ± 5.676e-80 → 1.320e-79 (53.00% error)
- **Interpretation**: Week 4 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Validation repeats confirm no useful gradient is present. High-ucb exploration confirmed the function is effectively flat, so the strategy transitions into lock mode early.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.800959, 0.915778]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7726 ± 0.1322 → 0.696 (11.00% error)
- **Interpretation**: Week 4 improved the incumbent; cumulative improvement from week 1 is 0.424
- **Insight**: Refinement continues with smaller but reliable gains. After baseline mapping, ei consistently refines the same promising ridge.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.895918, 0.023007, 0.092809]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.05 ± 0.0316 → -0.082 (39.00% error)
- **Interpretation**: Week 4 improved the incumbent; cumulative improvement from week 1 is 0.017
- **Insight**: Progress remains incremental on this multimodal surface. Continued exploration is necessary because every gain comes from shaving away negative loss rather than finding a strong positive basin.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.450549, 0.501381, 0.495876, 0.350376]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.9912 ± 0.2373 → -0.698 (42.00% error)
- **Interpretation**: Week 4 improved the incumbent; cumulative improvement from week 1 is 0.074
- **Insight**: SVM filtering removes clearly bad regions and boosts consistency. The main improvement comes from using svm filtering to avoid obviously poor placements while still preserving a modest exploration budget.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.342910, 0.814210, 0.786345, 0.878717]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6851.67 ± 1090.37 → 7367.39 (7.00% error)
- **Interpretation**: Week 4 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Follow-up probes show the peak is real and repeatable. A week-2 switch into ei pays off immediately and the week-3 peak becomes the global anchor for the rest of the project.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.421573, 0.818649, 0.577151, 0.538321, 0.896567]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2982 ± 0.2804 → -0.71 (58.00% error)
- **Interpretation**: Week 4 improved the incumbent; cumulative improvement from week 1 is 0.482
- **Insight**: SVM filtering removes obviously poor recipes and sharpens results. The model needs both higher noise tolerance and candidate filtering to keep making small but reliable gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.830884, 0.595201, 0.812425, 0.538037, 0.142212, 0.554496]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.4914 ± 0.1954 → 0.592 (17.00% error)
- **Interpretation**: Week 4 improved the incumbent; cumulative improvement from week 1 is 0.124
- **Insight**: Improvement remains steady even as dimensionality bites. Moderate ucb keeps improving the incumbent until the landscape stabilizes around week 8.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.038749, 0.350806, 0.059299, 0.536794, 0.886281, 0.477618, 0.397483, 0.500607]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 2.24 ± 1.536 → 3.2 (30.00% error)
- **Interpretation**: Week 4 improved the incumbent; cumulative improvement from week 1 is 3.194
- **Insight**: The incumbent keeps increasing as the model gains data. Pure gp stabilizes the search after the weak week-1 ensemble, then a lightweight nn+gp blend helps squeeze out late-stage gains.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Weeks 1-3 emphasize exploration, weeks 4-7 use a more balanced policy, and weeks 8-13 increasingly lock onto incumbents. Week 4 fits that pattern through a balanced-oriented allocation.
- **Technique effectiveness**: GP-EI remains the strongest exploitation tool whenever a credible incumbent exists (especially F5, then F2). GP-UCB is still the best general-purpose explorer, and SVM+GP produces slower but steadier gains on F4/F6 once enough data exists to filter candidates.
- **Dimensionality effect**: 2D problems calibrate quickly, 4D-6D problems benefit from hybrid filtering, and the 8D search still pays a high uncertainty tax even after model improvements.
- **Model quality trend**: Prediction intervals shrink over time, with the sharpest improvements on F2, F5, and F7 after exploitation begins.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F5
- **Still actively searching**: F2, F3, F4, F6, F7, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 5

| Function | Change | Old | New | Rationale |
|----------|--------|-----|-----|-----------|
| F2 | Strategy mode | Exploitation | Plateau | Operational mode changed from Exploitation to Plateau based on the latest evidence. |
| F4 | Strategy mode | SVM_Active | SVM_Stable | Operational mode changed from SVM_Active to SVM_Stable based on the latest evidence. |
| F5 | Strategy mode | Plateau | Locked | Operational mode changed from Plateau to Locked based on the latest evidence. |
| F6 | Strategy mode | SVM_Active | SVM_Stable | Operational mode changed from SVM_Active to SVM_Stable based on the latest evidence. |
| F7 | Strategy mode | Balanced | Improving | Operational mode changed from Balanced to Improving based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
