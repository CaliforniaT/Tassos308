# Week 2 Summary - Early Strategy Shift

**Week Number**: 2/13  
**Date Completed**: September 14, 2026  
**Status**: ✅ COMPLETE  
**Source**: Reconstructed from `results/performance_analysis/week_by_week_metrics.csv` and repository summary documents

---

## Executive Summary

- **Tracked Functions This Week**: 8
- **Best Function to Date**: F5 with peak `3486.1`
- **Largest Weekly Gain**: F5 with `+889.86`
- **Average Model Accuracy**: 62.1%
- **Average Exploration Rate**: 61.2%

### Status Breakdown

- **Balanced**: 1
- **Exploitation**: 1
- **Exploration**: 3
- **Plateau**: 1
- **Recovery**: 1
- **Switching**: 1

---

## Function Snapshot

| Function | Technique | Acquisition | Parameter | Peak After Week | Weekly Improvement | Status |
|----------|-----------|-------------|-----------|-----------------|--------------------|--------|
| F1 | GP | UCB | Beta=5.0 | 1.32e-79 | 0.0 | Plateau |
| F2 | GP | EI | Xi=0.01 | 0.545 | 0.273 | Switching |
| F3 | GP | UCB | Beta=5.0 | -0.087 | 0.012 | Exploration |
| F4 | GP | UCB | Beta=3.0 | -0.765 | 0.007 | Exploration |
| F5 | GP | UCB | Beta=1.0 | 3486.1 | 889.86 | Exploitation |
| F6 | GP | UCB | Beta=5.0 | -0.812 | 0.38 | Exploration |
| F7 | GP | UCB | Beta=3.0 | 0.521 | 0.053 | Balanced |
| F8 | GP | UCB | Beta=1.5 | 0.47 | 0.464 | Recovery |

---

## Weekly Insights

- **F1**: Increased exploration doesn't help flat function
- **F2**: SWITCH to EI - exploitation begins; +100% improvement
- **F3**: Marginal improvement; multimodal confirmed
- **F4**: Slight improvement; 4D still challenging
- **F5**: Light exploitation pays off; +34% weekly gain
- **F6**: Improved from -1.192 to -0.812; noisy but progressing
- **F7**: Steady improvement; balanced strategy working
- **F8**: Switched to simple GP; stabilized after week 1 failure

---

## Submission Files

- `queries.csv` records the weekly submission metadata available in this repository snapshot.
- `results.csv` records the week-level performance metrics and outcomes captured in the project analysis.

## Next Focus

- Double down on the strongest week 2 improvements while keeping difficult functions exploratory.

---

**Document Status**: ✅ COMPLETE  
**Week**: 2/13  
**Author**: CaliforniaT  
**Date**: September 14, 2026
