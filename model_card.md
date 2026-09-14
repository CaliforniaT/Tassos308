# Model Card: Adaptive Bayesian Optimization Engine

## Overview

**Model Name:** Adaptive Bayesian Optimization Engine (v1.0)  
**Model Type:** Gaussian Process Regressor with Dynamic Acquisition Logic  
**Purpose:** Optimize unknown black-box functions using limited queries

This model acts as a surrogate for unknown functions, using a competitive logic loop to choose the most informative next point to sample. It combines Gaussian Process regression with principled acquisition functions (UCB and Expected Improvement) to balance exploration and exploitation.

---

## Intended Use

The approach is suitable for:

- **Optimizing expensive-to-evaluate black-box functions** where each query is costly
- **Limited sample budgets** (one query per function per week in this case)
- **Multi-dimensional regression** where the underlying function is unknown
- **Continuous optimization problems** with bounded input spaces

### Primary Use Cases

1. **Hyperparameter Optimization**: Tuning ML model parameters (Functions 7, 8)
2. **Process Optimization**: Maximizing yield or efficiency in physical/chemical processes (Function 5)
3. **Design Space Exploration**: Finding optimal configurations in complex systems (Functions 3, 4, 6)
4. **Scientific Discovery**: Guiding experiments in data-limited settings (Function 1)

### Not Recommended For

- Discrete or combinatorial optimization
- Functions with known analytical gradients
- Extremely high-dimensional problems (>20D)
- Real-time applications requiring immediate responses
- Problems with extremely noisy outputs (SNR < 0.1)

---

## Model Details

### Architecture

The optimization engine comprises three main components:

1. **Surrogate Model (Gaussian Process)**
   - Kernel types: Matern, RBF, RationalQuadratic, Composite (Matern+White)
   - Hyperparameters: length_scale, alpha (noise level), nu (for Matern)
   - Training: fit on historical input-output data using marginal likelihood maximization

2. **Acquisition Function Module**
   - Upper Confidence Bound (UCB): `μ(x) + β·σ(x)`
   - Expected Improvement (EI): `E[max(y - f_best, 0)]`
   - Candidate scoring and ranking

3. **Adaptive Logic Engine**
   - Evaluates 16 hyperparameter configurations per function per week
   - Tests combinations of:
     - Kernels: Matern, RBF, RationalQuadratic, Matern+White
     - Acquisitions: UCB, EI
     - β values: 1.0, 3.0, 5.0, 7.0 (for UCB)
     - ξ values: 0.001, 0.01, 0.1 (for EI)
   - Selects configuration with best validation performance

### Candidate Generation

- **Method**: Random sampling + optional SVM filtering
- **Scale**: 1000 × dimensionality candidates per evaluation
- **Filtering**: (Week 3+) SVM-based classification to eliminate unpromising regions
- **Selection**: Choose point with highest acquisition score

### Hyperparameter Configuration

```python
# GP Configuration
ALPHA = 1e-10              # Noise level (smaller = more fitting)
GP_FIT_N_RESTARTS = 10     # Optimization restarts for kernel tuning
NORMALIZE_Y = True         # Standardize outputs

# Acquisition Functions
UCB_BETA = 3.0             # Exploration parameter
EI_XI = 0.01               # Improvement threshold

# SVM Filtering (Weeks 3+)
SVM_C = 100                # Regularization
SVM_KERNEL = 'rbf'         # RBF kernel

# Candidate Generation
NUM_CANDIDATES = 1000 * dim
```

### Function-Specific Tuning

| Function | Primary Kernel      | Recommended β | Notes                            |
|----------|---------------------|---------------|----------------------------------|
| 1        | Matern+White, RQ    | 5.0           | High ALPHA (1e-3) for smoothing  |
| 2        | Matern, RQ          | 3.0           | Standard configuration           |
| 3        | Matern, RQ          | 5.0           | Adaptive ALPHA (1e-4)            |
| 4        | Matern+White, RQ    | 3.0           | SVM filtering critical           |
| 5        | RQ, Matern          | 1.5           | High ALPHA (0.2) for stability   |
| 6        | Matern+White, RQ    | 5.0           | Avoid noisy regions              |
| 7        | Matern+White, RQ    | 3.0           | Balanced exploration             |
| 8        | Matern+White, RQ    | 1.0           | Low β for exploitation           |

---

## Performance

### Training Metrics

The model demonstrates:
- **Low-D Performance** (Functions 1-4): RMSE < 0.15 on validation sets
- **High-D Performance** (Functions 7-8): RMSE increases with dimensionality due to sparse data
- **Stability**: Convergence achieved within 100 iterations for most kernels

### Query Results Summary

| Function | Peak Output | Strategy              | Status      |
|----------|-------------|----------------------|-------------|
| 1        | 1.32e-79    | Cautious exploration  | Flat        |
| 2        | 0.75        | Moderate exploitation | Improving   |
| 3        | -0.09       | Adaptive modeling     | Improving   |
| 4        | -3.59       | Filtered search       | Low signal  |
| 5        | 7367.39     | Targeted exploitation | **Peak**    |
| 6        | -0.41       | Sparse signal         | Low signal  |
| 7        | 0.69        | Adaptive switching    | Moderate    |
| 8        | 9.84        | High-D exploration    | Constrained |

### Limitations

1. **Data Sparsity**: With only 1 query per week, coverage is extremely limited
2. **Curse of Dimensionality**: Functions 7-8 are severely under-sampled
3. **Cold Start**: First few weeks rely on random exploration
4. **Function Mismatch**: Some functions don't follow GP assumptions (e.g., highly multimodal)

---

## Assumptions and Limitations

### Key Assumptions

1. **Stationarity**: Function behavior is consistent across the search space
2. **Smoothness**: Functions are continuous (ideally differentiable)
3. **No Discontinuities**: No sudden jumps or singularities
4. **Bounded Inputs**: All inputs remain in [0, 1]
5. **Limited Noise**: Outputs have low-to-moderate noise

### Limitations

1. **Computational Trade-off**: Balancing number of kernel restarts vs. wall-clock time
2. **Kernel Selection**: Different functions may require different kernels, no universal choice
3. **Scalability**: Beyond 8D, candidate generation becomes computationally expensive
4. **Small Sample Regime**: Results are dominated by initial random queries
5. **No Adaptive Gradient**: Cannot use gradients even if they were available
6. **Multimodality**: May get stuck in local optima with small sample budget

### Robustness Considerations

- **Noise Handling**: Increased ALPHA for high-noise functions
- **Stability**: Multiple kernel restarts reduce sensitivity to initialization
- **Fallback**: Random sampling if GP fitting fails

---

## Interpretability

### Decision Transparency

All queries are logged with:
- Input vector
- Predicted mean and variance from GP
- Acquisition scores for all candidates
- Kernel/acquisition function used
- Hyperparameter values

### Inspection Example

```
Query #5 (Week 5):
Function 5
Selected Point: [0.352536, 0.820938, 0.794749, 0.871774]
GP Prediction: mean=1200, std=150
Acquisition Score (UCB): 2200
Kernel: RationalQuadratic
Beta: 1.5
Reasoning: Known high-output region, exploit locally
```

---

## Ethical Considerations

### Transparency & Reproducibility

- All hyperparameter justifications are documented
- Acquisition scores are computed transparently
- Code is open-source and available for inspection
- Decision-making process is not a "black box"

### Fairness & Bias

- No inherent bias in candidate sampling (uniform random generation)
- All functions treated equally in framework (function-specific tuning is explicit)
- No sensitive personal data involved

### Limitations Disclosure

- Clearly stated assumptions and limitations
- Known issues (e.g., high-D scaling, sparse data regime)
- Honest assessment of performance vs. baselines

---

## Deployment & Usage

### System Requirements

- Python 3.8+
- scikit-learn >= 1.0
- numpy >= 1.20
- pandas >= 1.3
- scipy >= 1.7

### Running the Model

```python
from sklearn.gaussian_process import GaussianProcessRegressor
from sklearn.gaussian_process.kernels import Matern

# Initialize
gp = GaussianProcessRegressor(kernel=Matern(nu=2.5), alpha=1e-10)

# Train on historical data
gp.fit(X_train, y_train)

# Predict and score candidates
predictions = gp.predict(X_candidates, return_std=True)
scores = predictions.mean + beta * predictions.std  # UCB

# Select best candidate
best_idx = np.argmax(scores)
next_query = X_candidates[best_idx]
```

### Integration with Optimization Loop

See `Function1-Final.ipynb` for complete working example with:
- Data loading and preprocessing
- Cross-validation setup
- Kernel comparison
- Acquisition function evaluation
- Query logging and result tracking

---

## Maintenance & Updates

- **Version**: 1.0 (active development)
- **Last Updated**: Week 13, 2026
- **Maintenance**: Weekly during optimization phase
- **Future Work**: 
  - Ensemble surrogates (combine GP + Neural Network)
  - Adaptive dimension reduction for high-D problems
  - Multi-objective optimization support

---

**Author**: CaliforniaT  
**License**: MIT  
**Repository**: [GitHub](https://github.com/CaliforniaT/Tassos308)