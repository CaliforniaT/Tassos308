# Week 9 Summary - Exploitation Phase

**Week Number**: 9/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.762
- **Average Prediction Error**: 25.00%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

Week 9 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.793600, 0.762194]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.052e-80 ± 2.244e-80 → 1.320e-79 (39.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: No hidden ridge emerges despite wider spacing from previous queries.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.862960, 0.955355]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7926 ± 0.0972 → 0.7478 (6.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Late exploitation supports a stable convergence claim.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.769726, 0.139686, 0.191522]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.049 ± 0.0191 → -0.072 (32.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 0.027
- **Insight**: Refined candidates keep trimming the loss.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.564185, 0.508290, 0.512953, 0.416097]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.7343 ± 0.1206 → -0.548 (34.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 0.224
- **Insight**: The weekly gain persists even in lower-uncertainty regions.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.354057, 0.823519, 0.794210, 0.874750]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6999.02 ± 1031.43 → 7367.39 (5.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Exploration would only add risk at this point.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.378262, 0.756279, 0.503823, 0.607961, 0.846561]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2912 ± 0.154 → -0.56 (48.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 0.632
- **Insight**: The incumbent is still moving, but only gradually.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.740001, 0.602306, 0.692659, 0.513179, 0.247388, 0.553344]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6054 ± 0.1445 → 0.6879 (12.00% error)
- **Interpretation**: Week 9 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: Repeated confirmation suggests the plateau is real.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.169018, 0.418711, 0.114834, 0.569631, 0.851195, 0.517822, 0.399628, 0.594791]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 6.46 ± 2.89 → 8.5 (24.00% error)
- **Interpretation**: Week 9 improved the incumbent; cumulative improvement from week 1 is 8.494
- **Insight**: Late-stage ensemble refinement keeps adding value.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 9 is part of the exploitation phase, so the allocation favors incumbent locking with low-variance follow-up probes.
- **Technique effectiveness**: NN+GP contributed the largest share of this week's non-negative gains (0.7 across 1 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 5.00% error, while F6 was the hardest to predict at 48.00% error.

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
| F4 | Strategy mode | Balanced | Refinement | Operational mode changed from Balanced to Refinement based on the latest evidence. |
| F6 | Strategy mode | Balanced | Refinement | Operational mode changed from Balanced to Refinement based on the latest evidence. |

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
