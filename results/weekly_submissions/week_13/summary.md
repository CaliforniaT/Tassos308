# Week 13 Summary - Exploitation Phase

**Week Number**: 13/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.2305
- **Average Prediction Error**: 19.88%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

Week 13 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.791120, 0.768550]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 9.240e-80 ± 1.452e-80 → 1.320e-79 (30.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Final check confirms F1 never meaningfully improves from baseline.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.867574, 0.959468]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7777 ± 0.0823 → 0.7478 (4.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Final week preserves the 0.75 solution without regression.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.698685, 0.184532, 0.241608]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0524 ± 0.0128 → -0.069 (24.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 0.03
- **Insight**: Final output is still negative, but materially better than week 1.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.616764, 0.580597, 0.534020, 0.446072]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.5564 ± 0.0685 → -0.428 (30.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 0.344
- **Insight**: Final week keeps the slow SVM+GP climb intact.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.355135, 0.820919, 0.797716, 0.867342]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7146.37 ± 1031.43 → 7367.39 (3.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Final week preserves the week-3 peak without degradation.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.287271, 0.736489, 0.448052, 0.620415, 0.802186]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.246 ± 0.0881 → -0.41 (40.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 0.782
- **Insight**: Final week posts the best F6 value of the project.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.739395, 0.603511, 0.693016, 0.509855, 0.249339, 0.554076]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6329 ± 0.1169 → 0.6879 (8.00% error)
- **Interpretation**: Week 13 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: Final week confirms a stable 0.69 best value.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.207046, 0.429096, 0.161496, 0.583470, 0.814591, 0.559000, 0.450814, 0.608814]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.872 ± 2.952 → 9.84 (20.00% error)
- **Interpretation**: Week 13 improved the incumbent; cumulative improvement from week 1 is 9.834
- **Insight**: Final week records the project-best F8 output at 9.84.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 13 is part of the exploitation phase, so the allocation favors incumbent locking with low-variance follow-up probes.
- **Technique effectiveness**: NN+GP contributed the largest share of this week's non-negative gains (0.14 across 1 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 3.00% error, while F6 was the hardest to predict at 40.00% error.

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
