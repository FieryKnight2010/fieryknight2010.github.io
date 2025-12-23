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

## Research Team

**Ravi Kondadadi**

- Lead Researcher
- GitHub: [@fieryknight2010](https://github.com/fieryknight2010)

---

## Publications

```bibtex
@article{kondadadi2024ctdn,
  title={CTDN: Causal Temporal Diffusion Networks for Drug Repurposing in Epilepsy},
  author={Kondadadi, Ravi},
  journal={AMIA Annual Symposium},
  year={2024}
}

@article{kondadadi2024mgandr,
  title={MGAN-DR: Multi-Modal Graph Attention Networks for Drug Repurposing in Epilepsy},
  author={Kondadadi, Ravi},
  journal={AMIA Annual Symposium},
  year={2024}
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

## Acknowledgments

- **Data**: LINCS L1000 gene expression database (Broad Institute)
- **Inspiration**: Lv et al. (2024), Brueggeman et al. (2019)
- **Frameworks**: PyTorch, scikit-learn, NumPy

---

## License

Both CTDN and MGAN-DR are released under the **MIT License**.

```
MIT License

Copyright (c) 2024 Ravi Kondadadi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Contact

For questions, issues, or collaboration opportunities:

- **GitHub Issues**: [Report a bug or request a feature](https://github.com/fieryknight2010/fieryknight2010.github.io/issues)
- **Email**: [Contact via GitHub]

---

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request
