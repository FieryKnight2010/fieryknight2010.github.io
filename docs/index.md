# Epilepsy Drug Repurposing

Deep Learning Approaches for Identifying Novel Anti-Epileptic Drugs using LINCS L1000 Gene Expression Data

---

## Overview

This project presents two novel deep learning approaches for computational drug repurposing in epilepsy:

<div class="grid cards" markdown>

-   :material-brain:{ .lg .middle } **CTDN**

    ---

    Causal Temporal Diffusion Networks combining causal discovery, diffusion processes, and temporal dynamics for drug effect modeling.

    [:octicons-arrow-right-24: Learn more](ctdn/index.md)

-   :material-graph:{ .lg .middle } **MGAN-DR**

    ---

    Multi-Modal Graph Attention Networks integrating gene expression, molecular structure, and biological pathways.

    [:octicons-arrow-right-24: Learn more](mgan-dr/index.md)

</div>

---

## Performance Summary

| Metric | CTDN | MGAN-DR | Random Forest | Connectivity Map |
|--------|------|---------|---------------|------------------|
| **AUROC** | 0.600 | **0.628** | 0.540 | 0.527 |
| **AUPRC** | 0.153 | **0.157** | 0.108 | 0.100 |
| **P@10** | 0.20 | **0.30** | 0.10 | 0.00 |
| **P@20** | 0.15 | 0.15 | 0.15 | 0.05 |

**Dataset**: 3,000 drug profiles, 978 genes, 29 unique AEDs (11:1 class imbalance)

---

## Key Features

=== "CTDN"

    - **Causal Discovery**: Neural causal inference for true drug-gene relationships
    - **Diffusion Processes**: Models biological effect propagation
    - **Temporal Dynamics**: Captures time-dependent drug effects
    - **Few-Shot Meta-Learning**: Handles limited positive samples
    - **Uncertainty Quantification**: Confidence estimates via neural processes

=== "MGAN-DR"

    - **Multi-Modal Integration**: Combines diverse data types
    - **Graph Attention Networks**: 4-head attention for drug-gene relationships
    - **Cross-Modal Attention**: 8-head attention across modalities
    - **Hierarchical Learning**: Multi-level feature extraction
    - **Focal Loss**: Handles extreme class imbalance

---

## Quick Links

- [CTDN Quick Start](ctdn/quickstart.md)
- [MGAN-DR Quick Start](mgan-dr/quickstart.md)
- [Method Comparison](comparison.md)
- [GitHub Repository](https://github.com/fieryknight2010)

---

## Citation

If you use this work in your research, please cite:

```bibtex
@article{kondadadi2025ctdn,
  title={CTDN: Causal Temporal Diffusion Networks for Drug Repurposing in Epilepsy},
  author={Kondadadi, Rishik},
  journal={ISCB-ASCS},
  year={2025}
}

@article{kondadadi2025mgandr,
  title={MGAN-DR: Multi-Modal Graph Attention Networks for Drug Repurposing in Epilepsy},
  author={Kondadadi, Rishik},
  journal={AMIA Annual Symposium},
  year={2025}
}
```

---

## License

Both projects are licensed under the MIT License.
