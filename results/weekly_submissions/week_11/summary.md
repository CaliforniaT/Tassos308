# Week 11 Summary - Exploitation Phase

**Week Number**: 11/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.361
- **Average Prediction Error**: 22.38%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

Week 11 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.796848, 0.759388]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.712e-80 ± 1.716e-80 → 1.320e-79 (34.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: Only incumbent verification remains worthwhile.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.865764, 0.961414]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7851 ± 0.0912 → 0.7478 (5.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: The posterior mean and reality are now tightly aligned.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.728810, 0.172682, 0.228529]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0504 ± 0.0158 → -0.07 (28.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 0.029
- **Insight**: The model is finally calibrated enough to make conservative refinements.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.589234, 0.561994, 0.524691, 0.432212]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.6442 ± 0.0878 → -0.488 (32.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 0.284
- **Insight**: Late-stage runs mostly validate the filtered basin.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.349666, 0.819743, 0.792373, 0.872022]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7072.69 ± 1031.43 → 7367.39 (4.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: The best F5 settings remain untouched.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.314199, 0.741374, 0.449952, 0.603488, 0.834681]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.28 ± 0.1175 → -0.5 (44.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 0.692
- **Insight**: The best recipe is improving by fractions now.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.742610, 0.603390, 0.690088, 0.512750, 0.245374, 0.549943]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6191 ± 0.1335 → 0.6879 (10.00% error)
- **Interpretation**: Week 11 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: No late-stage challenger outperforms the incumbent.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.196079, 0.415522, 0.138260, 0.591276, 0.841118, 0.544823, 0.444649, 0.605435]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.41 ± 2.964 → 9.5 (22.00% error)
- **Interpretation**: Week 11 improved the incumbent; cumulative improvement from week 1 is 9.494
- **Insight**: Only small gains remain available.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 11 is part of the exploitation phase, so the allocation favors incumbent locking with low-variance follow-up probes.
- **Technique effectiveness**: NN+GP contributed the largest share of this week's non-negative gains (0.3 across 1 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 4.00% error, while F6 was the hardest to predict at 44.00% error.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5, F7
- **Still actively searching**: F3, F4, F6, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 12

No hyperparameter changes are planned for week 12. Current settings remain in place because the incumbent strategies are stable and the remaining budget is better spent on confirmation than reconfiguration.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
