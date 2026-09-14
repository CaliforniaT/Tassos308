# Week 8 Summary - Late-Stage Tuning

**Week Number**: 8/13  
**Date Completed**: September 14, 2026  
**Status**: ✅ COMPLETE  
**Source**: Reconstructed from `results/performance_analysis/week_by_week_metrics.csv` and repository summary documents

---

## Executive Summary

- **Tracked Functions This Week**: 7
- **Best Function to Date**: F5 with peak `7367.39`
- **Largest Weekly Gain**: F8 with `+0.9`
- **Average Model Accuracy**: 73.7%
- **Average Exploration Rate**: 26.9%

### Status Breakdown

- **Ensemble**: 1
- **Locked**: 1
- **Plateau**: 2
- **SVM_Stable**: 2
- **Slow**: 1

---

## Function Snapshot

| Function | Technique | Acquisition | Parameter | Peak After Week | Weekly Improvement | Status |
|----------|-----------|-------------|-----------|-----------------|--------------------|--------|
| F2 | GP | EI | Xi=0.01 | 0.75 | 0.0 | Plateau |
| F3 | GP | UCB | Beta=5.0 | -0.074 | 0.002 | Slow |
| F4 | SVM+GP | UCB | Beta=3.0 | -0.578 | 0.03 | SVM_Stable |
| F5 | GP | EI | Xi=0.001 | 7367.39 | 0.0 | Locked |
| F6 | SVM+GP | UCB | Beta=5.0 | -0.59 | 0.03 | SVM_Stable |
| F7 | GP | UCB | Beta=3.0 | 0.69 | 0.022 | Plateau |
| F8 | NN+GP | UCB | Beta=1.5 | 7.8 | 0.9 | Ensemble |

---

## Weekly Insights

- **F2**: Confirmed plateau
- **F3**: Minimal gain; function near ceiling
- **F4**: Stable refinement
- **F5**: Peak maintained
- **F6**: Stable; consistent refinement
- **F7**: Reaching plateau; strategy effective
- **F8**: Added NN; ensemble beginning to help

---

## Submission Files

- `queries.csv` records the weekly submission metadata available in this repository snapshot.
- `results.csv` records the week-level performance metrics and outcomes captured in the project analysis.

## Next Focus

- Concentrate the remaining budget on the unresolved high-dimensional and negative-output functions.

---

**Document Status**: ✅ COMPLETE  
**Week**: 8/13  
**Author**: CaliforniaT  
**Date**: September 14, 2026
