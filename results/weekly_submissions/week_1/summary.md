# Week 1 Summary - Initial Baseline

**Week Number**: 1/13  
**Date Completed**: September 14, 2026  
**Status**: ✅ COMPLETE

---

## 📊 Executive Summary

### Overview
- **Total Queries Submitted**: 8 (1 per function)
- **Peak Discoveries**: Baseline established for all functions
- **Best Performer**: Function 5 (Chemical Yield) with output 2596.24
- **Most Challenging**: Function 1 (extremely flat: 2.45e-48)

### Key Metrics
| Metric | Value | Status |
|--------|-------|--------|
| Avg Output (all functions) | 324.365 | 📊 Baseline |
| Best Output | 2596.24 (F5) | ✅ Strong |
| Worst Output | 2.45e-48 (F1) | ⚠️ Flat |
| Model Accuracy | N/A (first week) | — |
| Exploration Rate | 100% | ✅ Full coverage |

---

## 🔍 Function-by-Function Analysis

### Function 1 (2D - Radiation Detection)

**📋 Submission**
- Query: `0.884963-0.583561`
- Technique: Gaussian Process
- Acquisition: UCB (β=3.0)
- Kernel: Matern
- Strategy: Random Exploration

**📊 Results**
- Predicted: 1.5e-50
- Actual: 2.45e-48
- Prediction Error: 1629% (way off - very noisy or flat)
- Peak to Date: 2.45e-48

**💡 Insights**
1. Function is extremely flat - outputs are near zero across the space
2. High prediction error suggests very sparse signal
3. Random exploration appropriate for week 1
4. Will need high UCB β next week to explore aggressively

**📈 Convergence Status**
- Trend: FLAT (expected for week 1)
- Next Strategy: Continue exploration with UCB β=5.0

---

### Function 2 (2D - ML Likelihood)

**📋 Submission**
- Query: `0.77761-0.937936`
- Technique: Gaussian Process
- Acquisition: UCB (β=3.0)
- Kernel: RationalQuadratic
- Strategy: Random Exploration

**📊 Results**
- Predicted: 0.25
- Actual: 0.272
- Prediction Error: 9% (reasonable for first query)
- Peak to Date: 0.272

**💡 Insights**
1. Good prediction accuracy (only 9% error)
2. Output is positive and measurable (unlike F1)
3. RQ kernel appears reasonable
4. Function shows structure we can model

**📈 Convergence Status**
- Trend: IMPROVING (small but solid start)
- Next Strategy: Continue exploration, then switch to exploitation

---

### Function 3 (3D - Drug Discovery)

**📋 Submission**
- Query: `0.910351-0.011038-0.068696`
- Technique: Gaussian Process
- Acquisition: UCB (β=3.0)
- Kernel: Matern
- Strategy: Random Exploration

**📊 Results**
- Predicted: -0.05
- Actual: -0.099
- Prediction Error: 49% (moderate)
- Peak to Date: -0.099

**💡 Insights**
1. Negative outputs - maximization goal means finding "least bad"
2. Will need to explore to find positive or less negative regions
3. Matern kernel may not be optimal for this landscape

**📈 Convergence Status**
- Trend: EXPLORING (searching for good regions)
- Next Strategy: Higher exploration with UCB β=5.0

---

### Function 4 (4D - Warehouse Placement)

**📋 Submission**
- Query: `0.440199-0.422159-0.471556-0.384654`
- Technique: Gaussian Process
- Acquisition: UCB (β=3.0)
- Kernel: Matern+White
- Strategy: Random Exploration

**📊 Results**
- Predicted: -2.5
- Actual: -0.772
- Prediction Error: 69% (large error)
- Peak to Date: -0.772

**💡 Insights**
1. Better than initial prediction (output is less negative)
2. Prediction accuracy needs work - large errors in 4D space
3. Will implement SVM filtering from week 3

**📈 Convergence Status**
- Trend: MIXED (exploring 4D space)
- Next Strategy: Continue exploration; prepare SVM filtering

---

### Function 5 (4D - Chemical Yield)

**📋 Submission**
- Query: `0.392203-0.938431-0.994313-0.88695`
- Technique: Gaussian Process
- Acquisition: UCB (β=1.5)
- Kernel: RationalQuadratic
- Strategy: Light Exploitation

**📊 Results**
- Predicted: 2400.0
- Actual: 2596.24
- Prediction Error: 8% (excellent!)
- Peak to Date: 2596.24

**💡 Insights**
1. **STAR PERFORMER**: Highest output so far
2. Excellent prediction accuracy (8% error)
3. This function has HIGH peaks - major optimization opportunity
4. RQ kernel + β=1.5 is good combination for this function
5. Switch to exploitation mode next week to refine peak

**📈 Convergence Status**
- Trend: STRONG START ⭐⭐⭐⭐⭐
- Next Strategy: Switch to EI with ξ=0.001 for exploitation

---

### Function 6 (5D - Recipe Optimization)

**📋 Submission**
- Query: `0.520611-0.821804-0.559784-0.568522-0.968203`
- Technique: Gaussian Process
- Acquisition: UCB (β=3.0)
- Kernel: Matern+White
- Strategy: Random Exploration

**📊 Results**
- Predicted: -0.3
- Actual: -1.192
- Prediction Error: 297% (very poor)
- Peak to Date: -1.192

**💡 Insights**
1. Large negative output - poor initial query
2. Very bad prediction accuracy suggests sparse/noisy landscape
3. High ALPHA needed to handle noise
4. Need aggressive exploration to find better regions

**📈 Convergence Status**
- Trend: CHALLENGING (5D curse + noise)
- Next Strategy: UCB β=5.0 + SVM filtering from week 3

---

### Function 7 (6D - ML Hyperparameters)

**📋 Submission**
- Query: `0.836537-0.558098-0.856597-0.621254-0.116653-0.631617`
- Technique: Gaussian Process
- Acquisition: UCB (β=1.0)
- Kernel: Matern+White
- Strategy: Balanced Approach

**📊 Results**
- Predicted: 0.4
- Actual: 0.468
- Prediction Error: 17% (good)
- Peak to Date: 0.468

**💡 Insights**
1. Reasonable output for 6D function (β=1.0 seems appropriate)
2. Good prediction accuracy (17% error)
3. Room for improvement - will explore further
4. Hyperparameter tuning shows promise

**📈 Convergence Status**
- Trend: MODERATE START (reasonable for 6D)
- Next Strategy: Continue balanced exploration/exploitation

---

### Function 8 (8D - Advanced Hyperparameter Tuning)

**📋 Submission**
- Query: `0.036105-0.349529-0.029123-0.509092-0.904733-0.455832-0.319773-0.505309`
- Technique: Ensemble (GP + NN averaging)
- Acquisition: UCB (β=1.5)
- Kernel: Mixed
- Strategy: Random Exploration

**📊 Results**
- Predicted: 6.0
- Actual: 0.006
- Prediction Error: 99.89% (terrible!)
- Peak to Date: 0.006

**💡 Insights**
1. **MOST CHALLENGING**: Extremely high-dimensional (8D)
2. Ensemble gave terrible predictions - averaging made it worse
3. Will switch to pure GP next week, simpler approach
4. Curse of dimensionality evident - very sparse data

**📈 Convergence Status**
- Trend: VERY DIFFICULT (high-D + sparse data)
- Next Strategy: Switch to single GP; aggressive exploration

---

## 📈 Cross-Function Patterns

### Technique Effectiveness This Week

| Function | Technique | Acquisition | Peak | Error % | Status |
|----------|-----------|-------------|------|---------|--------|
| F1 | GP | UCB β=3.0 | 2.45e-48 | 1629% | ⚠️ Flat |
| F2 | GP | UCB β=3.0 | 0.272 | 9% | ✅ Good |
| F3 | GP | UCB β=3.0 | -0.099 | 49% | ⚠️ Negative |
| F4 | GP | UCB β=3.0 | -0.772 | 69% | ⚠️ Negative |
| F5 | GP | UCB β=1.5 | 2596.24 | 8% | ⭐⭐⭐⭐⭐ |
| F6 | GP | UCB β=3.0 | -1.192 | 297% | ⚠️ Poor |
| F7 | GP | UCB β=1.0 | 0.468 | 17% | ✅ Good |
| F8 | Ensemble | UCB β=1.5 | 0.006 | 99.89% | ⚠️ Terrible |

### Best Performer
- **Function 5** with output 2596.24 and 8% prediction error
- RationalQuadratic kernel + UCB β=1.5 works well
- Clear opportunity for high efficiency score

### Most Challenging
- **Function 1** with extremely flat landscape (2.45e-48)
- Will require aggressive exploration (high β) and patience

### Dimensionality Impact
- 2D functions (F1, F2): 9%-1629% error (wide range)
- 3D-4D functions (F3, F4, F5, F6): Negative or low outputs
- 6D-8D functions (F7, F8): Very low outputs (curse of dimensionality)

---

## 🎓 Key Learnings from Week 1

### What Worked Well
1. **Function 5 RQ Kernel**: Excellent prediction accuracy (8%)
2. **Random Exploration Strategy**: Good for initial baseline
3. **GP Fundamental Approach**: Works reasonably on 2D-6D functions

### What Didn't Work
1. **Ensemble for High-D**: Averaging gave terrible predictions (99.89% error)
2. **Flat Landscapes (F1)**: Need special handling with high ALPHA
3. **Negative Outputs (F3, F4, F6)**: Hard to model and optimize

### Surprising Discoveries
1. **F5 Peak is HUGE**: 2596.24 is orders of magnitude higher than other functions
   - High optimization efficiency opportunity
   - Switch to exploitation immediately

2. **8D Curse is Real**: F8 output is near zero (0.006) despite ensemble approach
   - Single models might work better than averaging
   - Will need dense sampling and NN surrogate

3. **Prediction Accuracy Varies Wildly**: 
   - Best: F5 (8% error)
   - Worst: F8 (99.89% error)
   - Suggests different kernels needed per function

---

## 🛠️ Hyperparameter Adjustments for Week 2

| Function | Parameter | Old | New | Rationale |
|----------|-----------|-----|-----|-----------|
| F1 | UCB β | 3.0 | 5.0 | Need aggressive exploration for flat landscape |
| F1 | ALPHA | 1e-10 | 1e-3 | Increase to handle noise better |
| F2 | UCB β | 3.0 | 3.0 | Keep - good performance |
| F3 | UCB β | 3.0 | 5.0 | Increase exploration for negative outputs |
| F4 | UCB β | 3.0 | 3.0 | Keep balanced approach |
| F5 | Acquisition | UCB | EI | SWITCH to EI for exploitation |
| F5 | EI ξ | N/A | 0.001 | Low threshold - exploit known peak |
| F6 | UCB β | 3.0 | 5.0 | Increase exploration for noisy function |
| F6 | ALPHA | 1e-10 | 1e-5 | Increase noise tolerance |
| F7 | UCB β | 1.0 | 3.0 | Increase to explore 6D space better |
| F8 | Technique | Ensemble | GP | SWITCH from ensemble to single GP |
| F8 | Kernel | Mixed | Matern | Use simple Matern kernel |

---

## 📈 Strategy for Week 2

### Overall Approach
- **Exploitation on F5**: Switch to EI with low ξ to refine the 2596.24 peak
- **Aggressive Exploration**: Increase β to 5.0 for flat/noisy functions (F1, F3, F6)
- **Simplify High-D**: Remove ensemble, use single GP for F8
- **Prepare SVM Filtering**: Will activate in week 3 for functions with enough data

### Function-Specific Plans

| Function | Week 2 Strategy | Expected Outcome |
|----------|-----------------|------------------|
| F1 | UCB β=5.0, ALPHA=1e-3 | Explore flat landscape aggressively |
| F2 | Continue UCB β=3.0 | Find local peaks around 0.272 |
| F3 | UCB β=5.0, explore new regions | Discover positive outputs |
| F4 | SVM prep + UCB β=3.0 | Map promising regions |
| F5 | EI ξ=0.001 exploitation | Refine peak around 2596 |
| F6 | UCB β=5.0, ALPHA=1e-5 | Escape poor regions |
| F7 | UCB β=3.0 exploration | Discover better 6D configurations |
| F8 | Switch to simple GP | Stabilize predictions |

### Budget Allocation
```
Week 2 Query Budget:
├─ Exploration (50%): F1, F3, F6, F8 (4 functions)
└─ Exploitation (50%): F2, F4, F5, F7 (4 functions)
```

---

## 📎 Appendices

### A. Complete Query Log Week 1
[See queries.csv]

### B. Cumulative Performance

| Function | Week 1 Peak | Efficiency Score | Convergence Speed |
|----------|-------------|------------------|-------------------|
| F1 | 2.45e-48 | 1.88e-79 | 1 |
| F2 | 0.272 | 0.021 | 1 |
| F3 | -0.099 | -0.0076 | 1 |
| F4 | -0.772 | -0.059 | 1 |
| F5 | 2596.24 | 199.7 | 1 |
| F6 | -1.192 | -0.092 | 1 |
| F7 | 0.468 | 0.036 | 1 |
| F8 | 0.006 | 0.00046 | 1 |

### C. Notes for Future Self
- F5 is the star - prioritize this function for gains
- F1 landscape is extremely flat - may hit convergence ceiling early
- High-D functions (F7, F8) need special attention
- Prediction accuracy varies - consider function-specific kernels
- Week 2 will focus on: stabilizing predictions + first exploitation moves on F5

---

**Document Status**: ✅ COMPLETE  
**Week**: 1/13  
**Next Review**: Week 2  
**Author**: CaliforniaT  
**Date**: September 14, 2026

