# Week 3 Summary - Breakthrough Week

**Week Number**: 3/13  
**Date Completed**: September 14, 2026  
**Status**: ✅ COMPLETE  
**Source**: Reconstructed from `results/performance_analysis/week_by_week_metrics.csv` and repository summary documents

---

## Executive Summary

- **Tracked Functions This Week**: 8
- **Best Function to Date**: F5 with peak `7367.39`
- **Largest Weekly Gain**: F5 with `+3881.29`
- **Average Model Accuracy**: 66.1%
- **Average Exploration Rate**: 55.0%

### Status Breakdown

- **Balanced**: 1
- **Converged**: 1
- **Exploitation**: 1
- **Exploration**: 3
- **SVM_Prep**: 1
- **🎯PEAK**: 1

---

## Function Snapshot

| Function | Technique | Acquisition | Parameter | Peak After Week | Weekly Improvement | Status |
|----------|-----------|-------------|-----------|-----------------|--------------------|--------|
| F1 | GP | UCB | Beta=5.0 | 1.32e-79 | 0.0 | Converged |
| F2 | GP | EI | Xi=0.01 | 0.642 | 0.097 | Exploitation |
| F3 | GP | UCB | Beta=5.0 | -0.084 | 0.003 | Exploration |
| F4 | GP | UCB | Beta=3.0 | -0.728 | 0.037 | SVM_Prep |
| F5 | GP | EI | Xi=0.001 | 7367.39 | 3881.29 | 🎯PEAK |
| F6 | GP | UCB | Beta=5.0 | -0.752 | 0.06 | Exploration |
| F7 | GP | UCB | Beta=3.0 | 0.561 | 0.04 | Balanced |
| F8 | GP | UCB | Beta=1.5 | 2.0 | 1.53 | Exploration |

---

## Weekly Insights

- **F1**: Flat function confirmed converged; accept ceiling
- **F2**: Continued EI exploitation; +18% weekly gain
- **F3**: Minor gains; function very difficult
- **F4**: SVM filtering activated this week; preparing for week 4+
- **F5**: ⭐⭐⭐ BREAKTHROUGH - Found major peak (+111% improvement!)
- **F6**: Steady progress; noise handling improving
- **F7**: Consistent balanced exploration; on track
- **F8**: Still low output; high-D challenge confirmed

---

## Submission Files

- `queries.csv` records the weekly submission metadata available in this repository snapshot.
- `results.csv` records the week-level performance metrics and outcomes captured in the project analysis.

## Next Focus

- Protect the F5 breakthrough and activate more selective filtering where data is now sufficient.

---

**Document Status**: ✅ COMPLETE  
**Week**: 3/13  
**Author**: CaliforniaT  
**Date**: September 14, 2026
