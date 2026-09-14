# Week 12 Summary - Exploitation Phase

**Week Number**: 12/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7362.87
- **Total Weekly Gain**: 0.2605
- **Average Prediction Error**: 21.12%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

Week 12 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.790429, 0.765503]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.976e-80 ± 1.558e-80 → 1.320e-79 (32.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Confidence intervals are narrow and unchanged.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.859688, 0.956236]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7866 ± 0.0884 → 0.7491 (5.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Only tiny confirmation steps remain justified.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.733459, 0.169942, 0.239201]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0514 ± 0.0142 → -0.0695 (26.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 0.0295
- **Insight**: Week 12 suggests near-convergence without a full lock.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.611713, 0.558576, 0.545069, 0.425313]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.6 ± 0.0788 → -0.458 (31.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 0.314
- **Insight**: The hybrid model is close to fully converged.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.350215, 0.821925, 0.793550, 0.869913]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7141.98 ± 1030.80 → 7362.87 (3.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: All evidence supports a strict exploitation lock.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.306986, 0.754766, 0.466340, 0.609664, 0.803570]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2726 ± 0.1067 → -0.47 (42.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 0.722
- **Insight**: The function is nearly converged but still benefits from one more lock step.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.745500, 0.606615, 0.691131, 0.512706, 0.252877, 0.553638]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6271 ± 0.1282 → 0.6891 (9.00% error)
- **Interpretation**: Week 12 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: Convergence lock remains justified.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.191746, 0.439032, 0.170945, 0.580106, 0.837120, 0.543082, 0.419268, 0.605935]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.663 ± 2.9488 → 9.7 (21.00% error)
- **Interpretation**: Week 12 improved the incumbent; cumulative improvement from week 1 is 9.694
- **Insight**: Week 12 indicates near-convergence in 8D.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 12 is part of the exploitation phase, so the allocation favors incumbent locking with low-variance follow-up probes.
- **Technique effectiveness**: NN+GP contributed the largest share of this week's non-negative gains (0.2 across 1 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 3.00% error, while F6 was the hardest to predict at 42.00% error.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5, F7
- **Still actively searching**: F3, F4, F6, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 13

Function | Change | Old | New | Rationale
-------- | ------ | --- | --- | ---------
F1 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence.
F2 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence.
F3 | Strategy mode | Refinement | Final | Operational mode changed from Refinement to Final based on the latest evidence.
F4 | Strategy mode | Refinement | Final | Operational mode changed from Refinement to Final based on the latest evidence.
F5 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence.
F6 | Strategy mode | Refinement | Final | Operational mode changed from Refinement to Final based on the latest evidence.
F7 | Strategy mode | Locked | Final | Operational mode changed from Locked to Final based on the latest evidence.
F8 | Strategy mode | Ensemble | Final | Operational mode changed from Ensemble to Final based on the latest evidence.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
