# Week 10 Summary - Exploitation Phase

**Week Number**: 10/13  
**Phase**: Exploitation  
**Status**: ✅ COMPLETE

---

## Executive Summary

- **Total Queries Submitted**: 8 (1 per function)
- **New Peak Discoveries**: 4
- **Best Performer (highest actual output this week)**: F5 (Chemical Yield) at 7367.39
- **Total Weekly Gain**: 0.761
- **Average Prediction Error**: 23.62%
- **Technique Mix**: GP×5, NN+GP×1, SVM+GP×2

Week 10 shows F5 as the clearest current opportunity, while F6 carries the largest modeling uncertainty and therefore demands the most cautious follow-up.

---

## Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

- **Submission**: [0.793311, 0.758831]
- **Technique**: GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: 8.448e-80 ± 1.980e-80 → 1.320e-79 (36.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 0
- **Insight**: The surrogate is now reliable enough to avoid further speculative moves.

### Function 2 (2D - ML Likelihood)

- **Submission**: [0.863744, 0.954321]
- **Technique**: GP with RQ kernel and EI (Xi=0.01)
- **Prediction vs Actual**: 0.7926 ± 0.0942 → 0.7478 (6.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 0.478
- **Insight**: Marginal value of further exploration is negligible.

### Function 3 (3D - Drug Discovery)

- **Submission**: [0.754025, 0.141481, 0.191659]
- **Technique**: GP with Matern kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.0497 ± 0.0174 → -0.071 (30.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 0.028
- **Insight**: A smaller step indicates the surface is flattening near the incumbent.

### Function 4 (4D - Warehouse Placement)

- **Submission**: [0.560874, 0.551546, 0.501349, 0.430110]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: -0.6889 ± 0.1036 → -0.518 (33.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 0.254
- **Insight**: The best placements are now clustered around one basin.

### Function 5 (4D - Chemical Yield)

- **Submission**: [0.349942, 0.819641, 0.791241, 0.871486]
- **Technique**: GP with RQ kernel and EI (Xi=0.001)
- **Prediction vs Actual**: 7072.69 ± 1031.43 → 7367.39 (4.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 4771.15
- **Insight**: Another validation run confirms stable high yield.

### Function 6 (5D - Recipe Optimization)

- **Submission**: [0.334992, 0.761628, 0.456361, 0.608121, 0.844385]
- **Technique**: SVM+GP with Matern+White kernel and UCB (Beta=5.0)
- **Prediction vs Actual**: -0.2862 ± 0.1352 → -0.53 (46.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 0.662
- **Insight**: Later refinements are conservative and safer.

### Function 7 (6D - ML Hyperparameters)

- **Submission**: [0.740889, 0.601503, 0.698554, 0.514322, 0.248540, 0.549428]
- **Technique**: GP with Matern+White kernel and UCB (Beta=3.0)
- **Prediction vs Actual**: 0.6123 ± 0.139 → 0.6879 (11.00% error)
- **Interpretation**: Week 10 validated the incumbent without improving it; cumulative improvement from week 1 is 0.222
- **Insight**: The posterior mean is stable across nearby hyperparameter settings.

### Function 8 (8D - Advanced Hyperparameter Tuning)

- **Submission**: [0.159838, 0.400386, 0.125781, 0.555163, 0.833041, 0.539294, 0.414070, 0.592919]
- **Technique**: NN+GP with Mixed kernel and UCB (Beta=1.5)
- **Prediction vs Actual**: 7.084 ± 2.944 → 9.2 (23.00% error)
- **Interpretation**: Week 10 improved the incumbent; cumulative improvement from week 1 is 9.194
- **Insight**: The improvement rate slows as the search nears the best basin.

---

## Cross-Function Patterns and Technique Effectiveness

- **Phase pattern**: Week 10 is part of the exploitation phase, so the allocation favors incumbent locking with low-variance follow-up probes.
- **Technique effectiveness**: NN+GP contributed the largest share of this week's non-negative gains (0.7 across 1 function(s)), while the remaining methods were used where their landscape assumptions fit best.
- **Dimensionality effect**: Lower-dimensional functions remain easier to calibrate, while F8 still pays the highest uncertainty cost because of its 8D search space.
- **Current model quality**: The most accurate model this week was F5 at 4.00% error, while F6 was the hardest to predict at 46.00% error.

---

## Convergence Status and Strategy Adjustments

- **Converged or locked functions**: F1, F2, F5, F7
- **Still actively searching**: F3, F4, F6, F8
- **Allocation logic**: Query budget stays concentrated on functions with visible headroom, while plateaued functions are used mainly to validate that earlier peaks are real and repeatable.

---

## Hyperparameter Changes and Rationale for Week 11

No hyperparameter changes are planned for week 11. Current settings remain in place because the incumbent strategies are stable and the remaining budget is better spent on confirmation than reconfiguration.

---

## File References

- `queries.csv` contains the eight submitted candidate points with predicted statistics and strategy notes.
- `results.csv` contains the observed outputs, prediction errors, and improvement metrics for the same submissions.
