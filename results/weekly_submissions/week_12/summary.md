# Week 12 Summary - Pre-Final Lock-In

**Week Number**: 12/13  
**Date Completed**: September 14, 2026  
**Status**: ✅ COMPLETE  
**Source**: Reconstructed from `results/performance_analysis/week_by_week_metrics.csv` and repository summary documents

---

## Executive Summary

- **Tracked Functions This Week**: 4
- **Best Function to Date**: F5 with peak `7367.39`
- **Largest Weekly Gain**: F8 with `+0.2`
- **Average Model Accuracy**: 70.0%
- **Average Exploration Rate**: 15.0%

### Status Breakdown

- **Ensemble**: 1
- **Locked**: 1
- **SVM_Stable**: 2

---

## Function Snapshot

| Function | Technique | Acquisition | Parameter | Peak After Week | Weekly Improvement | Status |
|----------|-----------|-------------|-----------|-----------------|--------------------|--------|
| F4 | SVM+GP | UCB | Beta=3.0 | -0.458 | 0.03 | SVM_Stable |
| F5 | GP | EI | Xi=0.001 | 7367.39 | 0.0 | Locked |
| F6 | SVM+GP | UCB | Beta=5.0 | -0.47 | 0.03 | SVM_Stable |
| F8 | NN+GP | UCB | Beta=1.5 | 9.7 | 0.2 | Ensemble |

---

## Weekly Insights

- **F4**: Stable refinement
- **F5**: Peak maintained
- **F6**: Stable; marginal gain
- **F8**: Ensemble plateauing; minimal gain

---

## Submission Files

- `queries.csv` records the weekly submission metadata available in this repository snapshot.
- `results.csv` records the week-level performance metrics and outcomes captured in the project analysis.

## Next Focus

- Enter the last week with stable settings and use the final submissions as confirmation or last-chance probes.

---

**Document Status**: ✅ COMPLETE  
**Week**: 12/13  
**Author**: CaliforniaT  
**Date**: September 14, 2026
