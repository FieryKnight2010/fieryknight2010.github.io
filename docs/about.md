# About

## Project Overview

This project presents deep learning approaches for computational drug repurposing in epilepsy, using LINCS L1000 gene expression data to identify potential anti-epileptic drugs (AEDs) from existing compounds.

---

## Background

### The Problem

- **Epilepsy** affects ~50 million people worldwide
- **Drug development** is expensive (~$2.6B) and slow (~10-15 years)
- **Drug repurposing** can accelerate discovery of new treatments
- **LINCS L1000** provides gene expression signatures for ~20,000 compounds

### Our Approach

We developed two complementary deep learning methods:

1. **CTDN**: Focuses on causal inference and temporal dynamics
2. **MGAN-DR**: Focuses on graph attention and multi-modal learning

Both methods significantly outperform traditional approaches.

---

## Publications

```bibtex
@article{kondadadi2025ctdn,
  title={CTDN: Causal Temporal Diffusion Networks for Drug Repurposing in Epilepsy},
  author={Kondadadi, Ravi},
  journal={ISCB-ASCS},
  year={2025}
}

@article{kondadadi2025mgandr,
  title={MGAN-DR: Multi-Modal Graph Attention Networks for Drug Repurposing in Epilepsy},
  author={Kondadadi, Ravi},
  journal={AMIA Annual Symposium},
  year={2025}
}
```

---

## Data Sources

### LINCS L1000

The **Library of Integrated Network-Based Cellular Signatures (LINCS)** L1000 dataset provides:

- Gene expression profiles for ~20,000 compounds
- 978 landmark genes measured
- Multiple cell lines and time points
- Publicly available at [clue.io](https://clue.io)

### Anti-Epileptic Drugs

We curated a list of FDA-approved anti-epileptic drugs from:

- DrugBank
- PubChem
- Clinical literature

---

## Contact

For questions, issues, or collaboration opportunities:

- **GitHub Issues**: [Report a bug or request a feature](https://github.com/fieryknight2010/fieryknight2010.github.io/issues)
