# Week 8 Summary - Exploitation Phase

**Week Number**: 8/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 5
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7345.29
- **Total Weekly Gain**: 0.984
- **Average Prediction Error**: 26.50%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

Week 8 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.790543, 0.760911]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 7.656e-80 ± 2.772e-80 → 1.320e-79 (42.00% error)
- **Interpretation**: Week 8 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Late-stage probes continue to support an early convergence call.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.868995, 0.960661]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.8001 ± 0.1002 → 0.7478 (7.00% error)
- **Interpretation**: Week 8 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: The ridge is fully mapped and now effectively locked.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.776018, 0.098023, 0.159099]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0488 ± 0.0226 → -0.074 (34.00% error)
- **Interpretation**: Week 8 improved the incumbent; cumulative improvement from week 1 is 0.025
- **Insight**: Slow progress continues as the search narrows onto a viable pocket.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.530990, 0.513226, 0.492547, 0.401697]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.7861 ± 0.1387 → -0.578 (36.00% error)
- **Interpretation**: Week 8 improved the incumbent; cumulative improvement from week 1 is 0.194
- **Insight**: Exploration budget is reduced as the feasible region tightens.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.355372, 0.821144, 0.793298, 0.871241]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 6978.03 ± 1028.34 → 7345.29 (5.00% error)
- **Interpretation**: Week 8 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: The posterior variance is near zero around the winning recipe.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.384703, 0.752078, 0.501628, 0.591821, 0.878413]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.295 ± 0.1741 → -0.59 (50.00% error)
- **Interpretation**: Week 8 improved the incumbent; cumulative improvement from week 1 is 0.602
- **Insight**: Progress becomes more exploitative as candidate quality improves.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.737251, 0.602393, 0.694290, 0.511884, 0.243172, 0.555332]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6003 ± 0.1587 → 0.69 (13.00% error)
- **Interpretation**: Week 8 improved the incumbent; cumulative improvement from week 1 is 0.222
- **Insight**: Week 8 likely reaches the long-run optimum.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.125691, 0.409281, 0.097937, 0.541796, 0.860598, 0.523350, 0.391064, 0.561496]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 5.85 ± 2.808 → 7.8 (25.00% error)
- **Interpretation**: Week 8 improved the incumbent; cumulative improvement from week 1 is 7.794
- **Insight**: A lightweight NN+GP ensemble helps capture nonlinear interactions.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 8 is part of the exploitation phase, so the allocation favors incumbent locking with low-variance follow-up probes.
- **Technique effectiveness**: NN+GP contributed the largest share of this week's non-negative gains (0.9 across 1 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 5.00% error, while F6 was the hardest to predict at 50.00% error.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5, F7
- **Still actively searching**: F3, F4, F6, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 9

Function | Change | Old | New | Rationale
-------- | ------ | --- | --- | ---------
F7 | Strategy mode | Plateau | Locked | Operational mode changed from Plateau to Locked based on the latest evidence.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
