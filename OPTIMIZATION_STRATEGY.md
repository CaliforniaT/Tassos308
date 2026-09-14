# Black-Box Optimization Strategy & Methodology

## 📋 Overview

This document outlines the systematic approach to maximizing eight synthetic black-box functions using Bayesian Optimization and related techniques. The strategy evolves over 13 weeks based on empirical results and iterative learning.

---

## 🎯 Core Philosophy

**Principle**: Balance exploration (discovering new regions) with exploitation (refining known peaks).

**Constraint**: Only 1 query per function per week = 13 queries per function total.

**Objective**: Maximize output, not queries. Every submission must count.

---

## 📊 Weeks 1-2: Foundation & Random Exploration

### Goal
Establish baseline performance and learn function characteristics.

### Strategy
- **Technique**: Gaussian Process (GP) regression with random candidate generation
- **Acquisition**: UCB with moderate β (3.0)
- **Rationale**: 
  - Not enough data to trust complex models
  - Random sampling provides broad coverage
  - GP gives uncertainty estimates for next week

### Actions by Function

| Function | Dimensionality | Initial Data | Approach |
|----------|-----------------|--------------|----------|
| F1-F2 | 2D | 10 points | Wide exploration |
| F3-F4 | 3D-4D | 10 points | Stratified random |
| F5 | 4D | 10 points | Random + peak observation |
| F6-F7 | 5D-6D | 10 points | Latin hypercube sampling |
| F8 | 8D | 10 points | Uniform random (high-D curse) |

### Key Metrics to Collect
- Maximum output per function
- Output variance (is it noisy?)
- Dimensionality impact (does performance drop with D?)

### Deliverables
- `results/weekly_submissions/week_1/summary.md`
- `results/weekly_submissions/week_2/summary.md`
- Initial observations document

---

## 📊 Weeks 3-5: Pattern Recognition & Hybrid Approaches

### Goal
Identify function landscapes and switch to targeted strategies.

### Strategy
- **Technique**: GP + SVM filtering + acquisition function selection
- **Acquisition**: Adaptive choice between UCB and EI based on data
- **Rationale**:
  - Enough data to fit reliable GP models
  - SVM identifies "good" vs "bad" regions
  - Different functions need different β/ξ values

### Function-Specific Strategies

#### **Flat Functions (F1, F2, F6)**
- Problem: Outputs don't vary much
- Solution: High UCB β (5.0-7.0) to explore aggressively
- Kernel: Matern+White (noise = signal)

#### **Steep Functions (F5, F7)**
- Problem: High outputs concentrated in small regions
- Solution: Low UCB β (1.0-1.5) to exploit identified peaks
- Kernel: RationalQuadratic (multi-scale)

#### **Complex Functions (F3, F4, F8)**
- Problem: Multimodal or noisy
- Solution: Balanced UCB (3.0) + SVM filtering
- Kernel: Hybrid (Matern + RBF)

### SVM Filtering Logic

```
For each function:
  1. Compute median output from historical data
  2. Classify: "Good" (output > median), "Bad" (output < median)
  3. Train SVM on features vs. labels
  4. Score all 1000 GP-generated candidates with SVM
  5. Keep only top 500 candidates by SVM confidence
  6. Select best by GP acquisition score from filtered set
```

### Deliverables
- `results/weekly_submissions/week_3/summary.md` through `week_5/`
- SVM effectiveness analysis

---

## 📊 Weeks 6-10: Refinement & Technique Comparison

### Goal
Double down on what works; discontinue what doesn't.

### Strategy
- **Technique**: Per-function method selection
- **Adaptive**: Switch acquisition β/ξ if not improving
- **Ensemble**: Average predictions from multiple models for high-D functions

### Monitoring Metrics

**For each function, track:**

| Metric | Formula | Interpretation |
|--------|---------|-----------------|
| **Peak Output** | max(outputs) | Best found |
| **Weekly Gain** | Peak(week N) - Peak(week N-1) | Progress rate |
| **Predicted vs. Actual** | Predicted(x) vs. Actual(x) for best query | Model accuracy |
| **Exploration Rate** | % queries in new regions | Exploration% |
| **Convergence** | (Latest 5 outputs - best) / best | Convergence speed |

### Adaptive Decision Rules

**If Peak Output plateaus for 2+ weeks:**
- Increase exploration: β → β + 1.0 (or ξ → ξ × 2)
- Switch kernel: Try RationalQuadratic if using Matern

**If Predicted ≠ Actual by >30%:**
- Increase ALPHA (noise level): 1e-10 → 1e-6
- Try NN surrogate for next week

**If Best Query is in explored region:**
- Set flag: Function converged
- Maintain current strategy until week 13

### Deliverables
- `results/weekly_submissions/week_6/ through week_10/`
- Technique effectiveness table
- Per-function convergence plots

---

## 📊 Weeks 11-13: Consolidation & Final Push

### Goal
Lock in discoveries; make final strategic bets.

### Strategy

#### **For Converged Functions** (F1, F2, F5, F7)
- Strategy: Minimal exploration, light exploitation
- Action: Maintain peak, prepare final report

#### **For Non-Converged Functions** (F3, F4, F6, F8)
- Strategy: Aggressive exploration
- Action: Try new regions or ensemble methods
- Rationale: Last chance to find new peaks

### Final Week (Week 13) Special Actions

1. **Analyze all query-output pairs** for patterns
2. **Generate "best possible guess"** for unexplored regions
3. **Allocate week 13 queries** to highest-uncertainty regions
4. **Document learned landscape** for each function

### Deliverables
- `results/weekly_submissions/week_11/ through week_13/`
- Final efficiency scorecard
- Convergence analysis

---

## 🔧 Technical Details

### Gaussian Process Configuration

```python
# Default Configuration
GP_ALPHA = 1e-10  # Initial noise level (very tight fit)
GP_N_RESTARTS = 10  # Multiple initializations to escape local optima
NORMALIZE_Y = True  # Standardize outputs

# Function-Specific Overrides
FUNCTION_ALPHA = {
    1: 1e-3,      # Noisy (F1 is flat)
    2: 1e-6,      # Medium
    5: 0.2,       # Very noisy (high peaks = unstable)
    8: 1e-5,      # Complex high-D
}
```

### Kernel Selection by Function

| Function | Primary Kernel | Backup | Rationale |
|----------|-----------------|--------|-----------|
| F1 | Matern+White | RQ | Handle flat landscape noise |
| F2 | Matern | RQ | Smooth noisy slope |
| F3 | RationalQuadratic | Matern | Multi-modal |
| F4 | Matern+White | RQ | Complex + noisy |
| F5 | RationalQuadratic | Matern | Sharp peaks, multi-scale |
| F6 | Matern+White | Matern | Sparse signal + noise |
| F7 | Matern+White | RQ | High-D stability |
| F8 | Ensemble (all 3) | N/A | Extreme high-D uncertainty |

### Acquisition Function Parameters

```python
# UCB: μ(x) + β·σ(x)
UCB_BETA_EXPLORE = 5.0  # High uncertainty weight
UCB_BETA_EXPLOIT = 1.0  # Low uncertainty weight

# EI: E[max(y - y_best, 0)]
EI_XI_EXPLORE = 0.1     # Improvement threshold (low tolerance)
EI_XI_EXPLOIT = 0.001   # Improvement threshold (high tolerance)

# Adaptive selection logic:
# If (peak_output - mean_output) > 0.5 * std(output):
#     Use EI with low ξ (we know good regions exist)
# Else:
#     Use UCB with high β (explore everything)
```

---

## 📈 Performance Evaluation Framework

### Efficiency Score (ES)

$$ES = \frac{\text{Peak Output Gained}}{\text{Queries Used}} = \frac{\Delta y}{13}$$

**Interpretation:**
- ES > 500: Excellent (F5 with GP-EI)
- ES 100-500: Good (F7 with GP-UCB)
- ES 10-100: Moderate (F4 with SVM+GP)
- ES < 10: Poor (F1 on flat landscape)

### Convergence Speed (CS)

$$CS = \frac{\text{Peak Output Achieved}}{\text{Week of Achievement}}$$

**Example:**
- F5 achieved 7367.39 by week 3: CS = 7367.39 / 3 = 2455.8
- F1 achieved 1.32e-79 by week 13: CS = 1.32e-79 / 13 = negligible

### Exploration Effectiveness (EE)

$$EE = \frac{\text{# Queries in New Regions}}{\text{Total Queries}} \times 100\%$$

**Target:**
- Weeks 1-3: 80%+ (broad exploration)
- Weeks 4-7: 50% (balanced)
- Weeks 8-13: <20% (exploitation focus)

---

## 📊 Expected Outcomes by Week

### Week 1-2: Baseline
- F1-F4: 0-10% improvement
- F5-F6: 0-20% improvement
- F7-F8: 0-5% improvement

### Week 3: Inflection Point
- Some functions show 50%+ improvement (SVM filtering + GP kicks in)
- Others plateau (flat functions hard to optimize)

### Week 5: Mid-way Evaluation
- Functions split into "converged" (< 1% weekly improvement) vs. "active" (> 5% weekly improvement)

### Week 10: Consolidation Check
- Most improvements locked in
- Diminishing returns on exploration

### Week 13: Final State
- Peak outputs stable
- Efficiency metrics finalized
- Lessons learned documented

---

## 🚀 When to Switch Strategies

### Switch to NN Surrogate If:
```
- Predicted values deviate >40% from actual
- Function is 6D+ and convergence is slow
- GP fitting takes >5 seconds per iteration
```

### Switch to Ensemble If:
```
- Multiple kernels have similar likelihood
- High-D function (F7, F8) with sparse data
- Need to average uncertainty across models
```

### Increase Exploration (β ↑) If:
```
- No improvement for 2+ consecutive weeks
- Exploration rate < 10% but peak < 50th percentile
```

### Increase Exploitation (β ↓) If:
```
- Found a clear peak and want to refine it
- Exploration rate > 80% but no new peaks found
```

---

## 📝 Weekly Reflection Template

**Each week, document:**

### 1. Method Selection
```markdown
- **Function**: F5
- **Technique**: Gaussian Process
- **Acquisition**: Expected Improvement
- **Kernel**: RationalQuadratic
- **Beta/Xi**: ξ = 0.001 (exploitation mode)
- **Why**: Previous week found peak at 3486.10. 
  Now exploiting locally near that peak.
```

### 2. Results
```markdown
- **Query Submitted**: [0.352536, 0.820938, 0.794749, 0.871774]
- **Predicted Output**: 6200.0 (std: 450)
- **Actual Output**: 7367.39
- **Improvement**: +3881.29 from previous peak
- **Exploration?**: No (query near previous peaks)
```

### 3. Efficiency Analysis
```markdown
- **Weeks to Peak**: 3 weeks
- **Peak Output**: 7367.39
- **Efficiency Score**: 7367.39 / 3 = 2455.8 per query
- **Comparison**: GP-EI is 25x better than random for F5
```

### 4. Next Week Plan
```markdown
- **Observed**: Function has clear peak; diminishing returns from further queries
- **Decision**: Switch to light exploitation (β = 0.5)
- **Rationale**: Lock in gains; minimize wasted queries
```

---

## 🎯 Success Criteria

**By Week 13, evaluate success on:**

1. ✅ **Improvement from Initial**: Each function shows some improvement from week 0 to week 13
2. ✅ **Technique Diversity**: Multiple optimization methods compared
3. ✅ **Documentation**: Weekly reflections + efficiency metrics
4. ✅ **Reproducibility**: Code + results are fully documented
5. ✅ **Insights**: Key learnings extracted and communicated

---

## 🔗 Integration with Results Directory

All strategies execute within this structure:

```
results/
├── weekly_submissions/
│   ├── week_1/
│   │   ├── summary.md          # ← Document reflection from above
│   │   ├── queries.csv         # ← Store submitted query
│   │   └── results.csv         # ← Record actual output
│   └── ... week_13/
│
└── performance_analysis/
    ├── efficiency_metrics.csv  # ← Aggregate ES, CS, EE
    └── technique_comparison.md # ← Narrative analysis
```

---

## 📚 References

See **References.md** for learning resources on:
- Gaussian Processes
- Bayesian Optimization
- Acquisition Functions
- Neural Network Surrogates

