# Week 7 Summary - Balanced Phase

**Week Number**: 7/13  
**Phase**: Balanced  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 5
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7351.04
- **Total Weekly Gain**: 1.185
- **Average Prediction Error**: 27.88%
- **Technique Mix**: GP×6, SVM+GP×2

Week 7 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.797551, 0.776111]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 7.260e-80 ± 3.300e-80 → 1.320e-79 (45.00% error)
- **Interpretation**: Week 7 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Lock mode begins: queries are now confirmation-only.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.856252, 0.945352]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.8057 ± 0.1059 → 0.746 (8.00% error)
- **Interpretation**: Week 7 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: No nearby candidate beats the incumbent.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.778956, 0.092896, 0.164180]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0494 ± 0.0247 → -0.076 (35.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.023
- **Insight**: The incumbent keeps improving, but only by hundredths.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.565419, 0.502263, 0.470825, 0.378847]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.833 ± 0.1702 → -0.608 (37.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.164
- **Insight**: Balanced filtering still improves the incumbent each week.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.352350, 0.824579, 0.790645, 0.868203]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6909.98 ± 1058.55 → 7351.04 (6.00% error)
- **Interpretation**: Week 7 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Maintaining the incumbent is now the optimal decision.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.413451, 0.792240, 0.529235, 0.556427, 0.915735]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2976 ± 0.2077 → -0.62 (52.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.572
- **Insight**: Filtered exploration still finds small gains.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.726066, 0.615195, 0.726128, 0.572416, 0.277814, 0.517318]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.5745 ± 0.1804 → 0.668 (14.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 0.2
- **Insight**: By week 7 the function is close to its practical ceiling.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.077215, 0.434831, 0.063742, 0.528031, 0.827113, 0.554011, 0.406003, 0.516859]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 5.106 ± 2.76 → 6.9 (26.00% error)
- **Interpretation**: Week 7 improved the incumbent; cumulative improvement from week 1 is 6.894
- **Insight**: Week 7 still improves, although more slowly.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 7 is part of the balanced phase, so the allocation favors a mix of refinement and selective filtering.
- **Technique effectiveness**: GP contributed the largest share of this week's non-negative gains (1.125 across 6 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 6.00% error, while F6 was the hardest to predict at 52.00% error.

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
