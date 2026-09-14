# Black-Box Optimization (BBO) Capstone Project

## 📌 Section 1: Project Overview

The Black-Box Optimization (BBO) Capstone Project is a machine learning challenge focused on optimizing unknown functions using limited queries. Each function is treated as a black box — its internal logic, gradients, and analytical form are completely hidden.

The overall goal is to develop strategies that intelligently select input queries to maximize the output of these functions. This involves balancing **exploration** (trying new regions) and **exploitation** (refining known good regions).

### Key Learning Objectives

This project has provided hands-on experience in:
- **Bayesian Optimization**: Using Gaussian Processes and acquisition functions to guide exploration
- **Surrogate Modeling**: Building efficient approximations of expensive black-box functions
- **Hyperparameter Tuning**: Optimizing acquisition functions and kernel parameters for different function landscapes
- **Data-Driven Decision Making**: Making smart choices with limited feedback
- **Scientific Documentation**: Explaining methodology, justifying choices, and reflecting on results

### Functions in Scope

| **Function**   | **Input Dimensionality** | **Output Type** | **Optimization Goal** | **Application**                                          |
|----------------|--------------------------|------------------|----------------------|----------------------------------------------------------|
| **Function 1** | 2D                       | Scalar           | Maximize             | Contamination source detection in radiation fields      |
| **Function 2** | 2D                       | Scalar           | Maximize             | Maximize noisy ML model scores                           |
| **Function 3** | 3D                       | Scalar           | Maximize             | Drug discovery compound optimization                     |
| **Function 4** | 4D                       | Scalar           | Maximize             | Warehouse placement optimization                         |
| **Function 5** | 4D                       | Scalar           | Maximize             | Chemical process yield maximization                      |
| **Function 6** | 5D                       | Scalar           | Maximize             | Recipe optimization (cake ingredient tuning)             |
| **Function 7** | 6D                       | Scalar           | Maximize             | ML hyperparameter tuning (6 parameters)                  |
| **Function 8** | 8D                       | Scalar           | Maximize             | ML hyperparameter tuning (8 parameters, high-dimensional)|

---

## 📥 Section 2: Inputs and Outputs

Each week, the model receives past input–output data for each function and must submit one new query per function. The goal is to select queries that improve performance based on limited feedback.

### Input Specifications

- **Format**: Normalized vectors with values between 0 and 1
- **Dimensionality**: Varies by function (2D to 8D)
- **Constraints**:
  - Each component must be in the range [0, 1]
  - Only one query submission per function per week
  - All values are continuous (no discrete constraints)

### Output Specifications

- **Format**: Scalar float value (single output per query)
- **Type**: 1D array or single float
- **Meaning**: Performance/reward signal from the black-box function
- **Range**: Unbounded (can be negative or very large)

### Example Query-Output Pairs

**Function 1 (2D)**
```
Query: [0.793745, 0.763745]
Output: 1.322677e-79
```

**Function 5 (4D)**
```
Query: [0.352536, 0.820938, 0.794749, 0.871774]
Output: 1074.7568746609543
```

**Function 8 (8D)**
```
Query: [0.036105, 0.349529, 0.029123, 0.509092, 0.904733, 0.455832, 0.319773, 0.505309]
Output: 9.836
```

---

## 🎯 Section 3: Challenge Objectives

The primary objective is to **maximize** the output of eight unknown black-box functions. Each function represents a different real-world scenario with varying characteristics.

### Optimization Constraints

- **Limited Queries**: Only one query per function per week
- **Unknown Function Structure**: No access to gradients, analytical form, or internal logic
- **Noisy Outputs**: Some functions return unstable or noisy outputs
- **High Dimensionality**: Input spaces range from 2D to 8D, increasing complexity
- **Delayed Feedback**: Results received after submission, requiring careful planning

### Success Metrics

- Maximize the output value for each function
- Efficiently use limited queries (one per week)
- Adapt strategy based on historical feedback
- Document reasoning and justify methodological choices

---

## 🧪 Section 4: Technical Approach

### Core Strategy: Gaussian Process + Bayesian Optimization

**Phase 1: GP-Based Exploration**
- Train Gaussian Process regression with multiple kernels (Matern, RBF, RationalQuadratic)
- Use acquisition functions (UCB, Expected Improvement) to balance exploration/exploitation
- Generate candidate points uniformly across the input space
- Select query with highest acquisition score

**Phase 2: SVM-Guided Filtering**
- Train Support Vector Machine to classify regions as promising vs. unpromising
- Combine SVM confidence scores with GP predictions
- Improve query selection efficiency by filtering low-probability regions

**Phase 3: Adaptive Hyperparameter Tuning**
- Monitor model performance (training/validation error)
- Adjust kernel parameters and acquisition function settings
- Apply function-specific configurations based on historical patterns

### Function-Specific Strategies

| Function | Strategy                          | Key Insight                              |
|----------|-----------------------------------|------------------------------------------|
| 1        | GP + SVM filtering                | Flat surface → cautious exploration      |
| 2        | GP with UCB                       | Gradual slope → moderate exploitation    |
| 3        | GP + kernel SVM                   | Noisy → adaptive modeling                |
| 4        | GP + SVM filtering                | Low output → filtered search             |
| 5        | GP + SVM exploitation             | High output peaks → targeted sampling    |
| 6        | GP + SVM filtering                | Sparse signal → avoid noisy regions      |
| 7        | GP + alternating acquisition      | Mixed behavior → adaptive switching      |
| 8        | GP + kernel SVM                   | High-D → complex interactions            |

### Key Hyperparameters

```python
# Gaussian Process Configuration
GP_ALPHA = 1e-10              # Noise level (lower = more fitting)
GP_FIT_N_RESTARTS = 10        # Optimization restarts
NORMALIZE_Y = True            # Standardize outputs

# Acquisition Functions
UCB_BETA = 3.0                # Exploration parameter (higher = more exploration)
EI_XI = 0.01                  # Improvement threshold

# SVM Configuration
SVM_C = 100                   # Regularization parameter
SVM_KERNEL = 'rbf'            # RBF kernel for nonlinear boundaries

# Candidate Generation
NUM_CANDIDATES = 1000 * dim   # Scale with dimensionality
```

---

## 📊 Section 5: Technical Justification

### Gaussian Processes for Black-Box Optimization

**Why GPs?**
- Non-parametric model that captures uncertainty
- Provides both predictions (mean) and uncertainty (variance)
- Foundation for principled acquisition functions
- Scales reasonably to 8D with efficient kernels

**Kernel Selection**
- **Matern**: For physically-motivated processes with smoothness control (ν parameter)
- **RBF**: For very smooth functions (infinitely differentiable)
- **RationalQuadratic**: For multi-scale features (good in high dimensions)
- **Composite (Matern+White)**: For noisy data with explicit noise modeling

### Acquisition Functions

**Upper Confidence Bound (UCB)**
```
UCB(x) = μ(x) + β·σ(x)
```
- Balances mean (exploitation) and uncertainty (exploration)
- β parameter controls exploration level
- Simple, interpretable, efficient

**Expected Improvement (EI)**
```
EI(x) = E[max(y - f_best, 0)]
```
- Quantifies probability of improving current best
- More conservative than UCB
- Better for exploitation-focused tasks

### Support Vector Machines for Region Classification

**Why SVM Filtering?**
- Separates high-output regions from low-output regions
- Reduces wasted queries in unpromising areas
- Combines with GP for hybrid decision-making
- Robust to high dimensionality

---

## 📖 Section 6: Files & Structure

- **`Function1-Final.ipynb`**: Main analysis and optimization notebook
- **`initial_inputs.npy`**: Initial input training data
- **`initial_outputs.npy`**: Corresponding outputs
- **`README.md`**: This file - project overview and methodology
- **`References.md`**: Comprehensive list of learning resources
- **`data_sheet.md`**: Dataset documentation and analysis
- **`model_card.md`**: Model specifications and performance tracking

---

## 🚀 Getting Started

### Requirements

```
numpy>=1.20
pandas>=1.3
scikit-learn>=1.0
matplotlib>=3.4
seaborn>=0.11
scipy>=1.7
jupyter>=1.0
```

### Running the Analysis

1. Clone the repository
2. Install requirements: `pip install -r requirements.txt`
3. Open the main notebook: `jupyter notebook Function1-Final.ipynb`
4. Execute cells sequentially to:
   - Load initial training data
   - Train surrogate models
   - Generate optimized queries
   - Visualize results

### Key Workflow

```
1. Load Data (initial + historical weekly submissions)
   ↓
2. Train Surrogate Model (GP with best kernel)
   ↓
3. Generate Candidates (1000×dim random points)
   ↓
4. Evaluate Acquisition Function (UCB or EI)
   ↓
5. Apply SVM Filter (optional)
   ↓
6. Select Best Point
   ↓
7. Submit Query & Record Output
```

---

## 📈 Results & Learning Outcomes

### Key Discoveries

- **Function 5**: Achieved high outputs (>7000) by focusing on exploitation near known peaks
- **Function 1**: Required cautious exploration due to flat landscape and very small outputs (e-79 scale)
- **High-D Functions (7,8)**: Benefited from RationalQuadratic kernel for multi-scale feature capture
- **Noisy Functions**: Adaptive ALPHA tuning crucial for stability

### Lessons Learned

1. **Kernel Selection Matters**: Different functions require different kernel assumptions
2. **ALPHA Tuning is Critical**: Balancing fitting vs. smoothing is essential for stability
3. **Adaptive Strategies Work**: Function-specific hyperparameters outperform one-size-fits-all
4. **SVM Filtering Helps**: Combining probabilistic and geometric approaches improves efficiency
5. **Documentation is Key**: Clear reasoning enables reproducibility and future improvements

---

## 📚 Learning Resources

For detailed technical references, see [References.md](References.md)

Key concepts covered:
- Bayesian Optimization fundamentals
- Gaussian Process theory and practice
- Kernel design and selection
- Acquisition function design
- High-dimensional optimization
- Ensemble methods

---

## 🔗 Links & References

- **Main Notebook**: `Function1-Final.ipynb`
- **Data Sheet**: See `data_sheet.md` for dataset analysis
- **Model Card**: See `model_card.md` for model specifications
- **References**: See `References.md` for full reference list

---

**Author**: CaliforniaT  
**Project**: Black-Box Optimization Capstone  
**Last Updated**: 2026
