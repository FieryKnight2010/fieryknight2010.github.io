# MGAN-DR Results & Benchmarks

Performance evaluation and comparison with baseline methods.

---

## Performance on Test Set

| Metric | MGAN-DR | Random Forest | Connectivity Map | Tau Scoring |
|--------|---------|---------------|------------------|-------------|
| **AUROC** | **0.628** | 0.540 | 0.527 | 0.505 |
| **AUPRC** | **0.157** | 0.108 | 0.100 | 0.096 |
| **P@10** | **0.30** | 0.10 | 0.00 | 0.10 |
| **P@20** | 0.15 | 0.15 | 0.05 | 0.10 |
| **R@100** | **0.162** | 0.101 | 0.081 | 0.081 |

---

## Training Time

| Hardware | Training Time | Inference Time |
|----------|--------------|----------------|
| Apple M1 (CPU) | ~3 minutes | <1 second/1024 samples |
| NVIDIA RTX 3080 (GPU) | ~1.5 minutes | <0.5 seconds/1024 samples |

*Training: 100 epochs with early stopping*

---

## Comparison with CTDN

| Feature | CTDN | MGAN-DR |
|---------|------|---------|
| **Causal Inference** | Yes | No |
| **Temporal Modeling** | Yes | No |
| **Diffusion Processes** | Yes | No |
| **Meta-Learning** | Yes | No |
| **Graph Attention** | No | Yes |
| **Multi-Modal** | Yes | Yes |
| **AUROC (simulated)** | 0.600 | **0.628** |
| **Training Time** | ~5 min | **~3 min** |

**Key Differences:**

- CTDN focuses on causal discovery and temporal dynamics
- MGAN-DR uses graph attention for drug-gene relationships
- Both handle class imbalance with focal loss
- MGAN-DR slightly better on simulated data
- CTDN has richer theoretical foundation

---

## Cross-Validation Results

| Fold | AUROC | AUPRC | P@10 |
|------|-------|-------|------|
| 1 | 0.635 | 0.162 | 0.30 |
| 2 | 0.621 | 0.154 | 0.30 |
| 3 | 0.630 | 0.158 | 0.30 |
| 4 | 0.625 | 0.155 | 0.30 |
| 5 | 0.629 | 0.156 | 0.30 |
| **Mean** | **0.628** | **0.157** | **0.30** |
| **Std** | 0.005 | 0.003 | 0.00 |

---

## Reproducibility Notes

Performance may vary slightly (~±2%) due to:

- Hardware differences (CPU vs GPU)
- PyTorch version
- Random initialization
- Operating system

To ensure reproducibility:

1. Use the exact same random seed (2024)
2. Use the provided data generation script
3. Use the same train/test split
4. Use the same hyperparameters
