# Week 4 Summary

**Week Number**: 4/13  
**Status**: ✅ COMPLETE

## Overview
- Functions Evaluated: 8
- Total Queries Recorded: 8
- Best Peak This Week: 7367.39 (F5)
- Total Weekly Improvement: 1.359
- Average Model Accuracy: 67.88%

## Function Results

| Function | Technique | Acquisition | Peak Output | Weekly Improvement | Status |
|---|---|---|---:|---:|---|
| F1 | GP | UCB Beta=5.0 | 1.32e-79 | 0 | Converged |
| F2 | GP | EI Xi=0.01 | 0.696 | 0.054 | Exploitation |
| F3 | GP | UCB Beta=5.0 | -0.082 | 0.002 | Exploration |
| F4 | SVM+GP | UCB Beta=3.0 | -0.698 | 0.03 | SVM_Active |
| F5 | GP | EI Xi=0.001 | 7367.39 | 0 | Plateau |
| F6 | SVM+GP | UCB Beta=5.0 | -0.71 | 0.042 | SVM_Active |
| F7 | GP | UCB Beta=3.0 | 0.592 | 0.031 | Balanced |
| F8 | GP | UCB Beta=1.5 | 3.2 | 1.2 | Exploration |

## Notes
- Query configuration details are in `queries.csv`.
- Actual outputs and performance metrics are in `results.csv`.
