# Method Comparison

Detailed comparison between CTDN, MGAN-DR, and baseline methods.

---

## Performance Summary

| Metric | CTDN | MGAN-DR | Random Forest | Connectivity Map | Tau Scoring |
|--------|------|---------|---------------|------------------|-------------|
| **AUROC** | 0.600 | **0.628** | 0.540 | 0.527 | 0.505 |
| **AUPRC** | 0.153 | **0.157** | 0.108 | 0.100 | 0.096 |
| **P@10** | 0.20 | **0.30** | 0.10 | 0.00 | 0.10 |
| **P@20** | 0.15 | 0.15 | 0.15 | 0.05 | 0.10 |
| **R@100** | 0.112 | **0.162** | 0.101 | 0.081 | 0.081 |

---

## Feature Comparison

| Feature | CTDN | MGAN-DR | RF | CMap | Tau |
|---------|:----:|:-------:|:--:|:----:|:---:|
| Deep Learning | Yes | Yes | No | No | No |
| Causal Inference | Yes | No | No | No | No |
| Temporal Modeling | Yes | No | No | No | No |
| Diffusion Processes | Yes | No | No | No | No |
| Meta-Learning | Yes | No | No | No | No |
| Graph Attention | No | Yes | No | No | No |
| Multi-Modal | Yes | Yes | No | No | No |
| Focal Loss | Yes | Yes | No | N/A | N/A |
| Class Weighting | Yes | Yes | Yes | No | No |

---

## Training Characteristics

| Method | Training Time | Inference Time | GPU Required |
|--------|--------------|----------------|:------------:|
| CTDN | ~5 min | <2s / 1024 | Optional |
| MGAN-DR | ~3 min | <1s / 1024 | Optional |
| Random Forest | ~30s | <0.5s / 1024 | No |
| Connectivity Map | N/A | ~1s / 1024 | No |
| Tau Scoring | N/A | <0.5s / 1024 | No |

---

## Strengths and Weaknesses

### CTDN

=== "Strengths"
    - **Causal discovery**: Identifies true causal drug-gene relationships
    - **Temporal modeling**: Captures time-dependent drug effects
    - **Theoretical foundation**: Based on causal inference and diffusion theory
    - **Uncertainty quantification**: Provides confidence estimates
    - **Few-shot learning**: Handles limited positive samples

=== "Weaknesses"
    - More complex architecture
    - Longer training time
    - Requires more hyperparameter tuning
    - Lower empirical performance on simulated data

### MGAN-DR

=== "Strengths"
    - **Best empirical performance**: Highest AUROC and AUPRC
    - **Interpretable attention**: Graph attention weights show important genes
    - **Simpler architecture**: Easier to train and deploy
    - **Faster training**: ~3 minutes to convergence

=== "Weaknesses"
    - No causal inference capability
    - No temporal modeling
    - May overfit to spurious correlations
    - Less theoretical foundation

### Traditional Methods

=== "Random Forest"
    - Simple and interpretable
    - No deep learning required
    - Limited representation learning
    - Moderate performance

=== "Connectivity Map"
    - Widely used baseline
    - No training required
    - Poor performance on this dataset
    - Not designed for classification

=== "Tau Scoring"
    - Simple correlation-based approach
    - Fast computation
    - Lowest performance
    - No learning capability

---

## When to Use Each Method

### Use CTDN when:

- You need to understand **causal** drug-gene relationships
- **Temporal dynamics** of drug effects are important
- You want **uncertainty quantification** for predictions
- You have **very few** positive examples (few-shot scenario)
- **Interpretability** of causal graphs is valuable

### Use MGAN-DR when:

- You prioritize **predictive performance**
- You want **faster training** and inference
- **Gene importance** through attention weights is sufficient
- You have a simpler deployment environment
- **Graph structure** of drug-gene relationships is important

### Use Traditional Methods when:

- You need a **quick baseline**
- **Interpretability** is more important than performance
- **Computational resources** are limited
- You're doing **exploratory analysis**

---

## Recommendations

!!! tip "Best Overall Performance"
    **MGAN-DR** achieves the best performance on our benchmark dataset with AUROC of 0.628.

!!! tip "Most Interpretable"
    **CTDN** provides the most interpretable results through its causal discovery module and temporal dynamics.

!!! tip "Fastest Prototyping"
    **Random Forest** is the fastest to set up for initial experiments and provides a reasonable baseline.

---

## Code Comparison

=== "CTDN"
    ```python
    from src.model import CTDN

    model = CTDN(
        n_genes=978,
        hidden_dim=256,
        n_heads=8,
        n_timesteps=10
    )
    ```

=== "MGAN-DR"
    ```python
    from src.model import MGANDR

    model = MGANDR(
        input_dim=978,
        hidden_dims=[512, 256, 128],
        dropout_rates=[0.4, 0.3, 0.2]
    )
    ```

=== "Random Forest"
    ```python
    from sklearn.ensemble import RandomForestClassifier

    model = RandomForestClassifier(
        n_estimators=100,
        class_weight='balanced'
    )
    ```
