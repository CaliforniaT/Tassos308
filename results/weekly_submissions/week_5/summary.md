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

Week 5 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.806578, 0.709155]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 6.072e-80 ± 5.412e-80 → 1.320e-79 (54.00% error)
- **Interpretation**: Week 5 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: The flat prior is stable enough to stop spending exploratory budget.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.872606, 0.951575]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.825 ± 0.1275 → 0.75 (10.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.478
- **Insight**: A local peak near 0.75 appears to be established.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.840671, 0.058900, 0.122437]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0504 ± 0.0292 → -0.08 (37.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.019
- **Insight**: Another tiny gain suggests exploration is still worthwhile.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.462546, 0.456895, 0.466260, 0.373764]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.9419 ± 0.2138 → -0.668 (41.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.104
- **Insight**: Filtered candidates continue producing steady gains.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.352453, 0.827757, 0.804209, 0.868736]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6778.00 ± 1060.90 → 7367.39 (8.00% error)
- **Interpretation**: Week 5 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: The search is effectively locked around the best-yield composition.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.456709, 0.762115, 0.528274, 0.613825, 0.950449]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2992 ± 0.255 → -0.68 (56.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.512
- **Insight**: The hybrid pipeline produces steadier improvements than raw GP.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.791704, 0.611952, 0.768246, 0.605814, 0.196659, 0.615919]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.5208 ± 0.1922 → 0.62 (16.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 0.152
- **Insight**: The incumbent is now clearly inside a productive basin.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.121502, 0.422634, 0.092003, 0.529597, 0.863298, 0.504913, 0.320011, 0.520898]
- **Technique**: GP with Matern kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 3.24 ± 2.07 → 4.5 (28.00% error)
- **Interpretation**: Week 5 improved the incumbent; cumulative improvement from week 1 is 4.494
- **Insight**: F8 is still far from converged, but the trend is finally positive.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 5 is part of the balanced phase, so the allocation favors a mix of refinement and selective filtering.
- **Technique effectiveness**: GP contributed the largest share of this week's non-negative gains (1.384 across 6 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 8.00% error, while F6 was the hardest to predict at 56.00% error.

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
