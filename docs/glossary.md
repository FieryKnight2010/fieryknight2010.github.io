# Glossary

Key terms and concepts used throughout this documentation.

---

## Drug Repurposing & Pharmacology

**AED (Anti-Epileptic Drug)**
:   A medication used to treat epileptic seizures. Also called anticonvulsants or antiseizure medications.

**Drug Repurposing**
:   The process of finding new therapeutic uses for existing drugs, also known as drug repositioning or drug reprofiling.

**LINCS (Library of Integrated Network-Based Cellular Signatures)**
:   An NIH program that generates gene expression profiles for thousands of compounds, genetic perturbations, and disease states.

**L1000**
:   A gene expression profiling technology that measures 978 landmark genes, which can be used to infer the expression of the full transcriptome.

**Landmark Genes**
:   The 978 genes directly measured in L1000 assays, selected because their expression levels can predict the expression of other genes.

**Connectivity Map (CMap)**
:   A database and methodology that uses gene expression signatures to discover connections between drugs, genes, and diseases.

**Perturbagen**
:   Any agent (drug, genetic modification, etc.) that causes a measurable change in cellular state.

---

## Machine Learning & Deep Learning

**AUROC (Area Under the Receiver Operating Characteristic Curve)**
:   A metric measuring classification performance across all thresholds. Values range from 0.5 (random) to 1.0 (perfect).

**AUPRC (Area Under the Precision-Recall Curve)**
:   A metric particularly useful for imbalanced datasets, measuring the trade-off between precision and recall.

**Precision@K (P@K)**
:   The proportion of true positives among the top K predictions. P@10 means precision in the top 10 predictions.

**Recall@K (R@K)**
:   The proportion of all positives captured in the top K predictions.

**Focal Loss**
:   A loss function designed for class-imbalanced problems that down-weights easy examples and focuses on hard negatives.

**Class Imbalance**
:   When one class significantly outnumbers another in a dataset. Our dataset has 11:1 imbalance (non-AED:AED).

**Early Stopping**
:   A regularization technique that stops training when validation performance stops improving.

**Batch Normalization**
:   A technique that normalizes layer inputs to stabilize and accelerate training.

**Dropout**
:   A regularization technique that randomly sets a fraction of neurons to zero during training to prevent overfitting.

**AdamW**
:   An optimizer that combines Adam with decoupled weight decay regularization.

---

## CTDN-Specific Terms

**Causal Discovery**
:   The process of identifying cause-and-effect relationships from data, as opposed to mere correlations.

**DAG (Directed Acyclic Graph)**
:   A graph with directed edges and no cycles, used to represent causal relationships.

**Diffusion Process**
:   A stochastic process that models how signals propagate through a network over time.

**Denoising Network**
:   A neural network trained to recover clean data from noisy observations, used in diffusion models.

**Temporal Dynamics**
:   Time-dependent changes in a system, such as how drug effects evolve over time.

**LSTM (Long Short-Term Memory)**
:   A recurrent neural network architecture capable of learning long-term dependencies in sequential data.

**MAML (Model-Agnostic Meta-Learning)**
:   A meta-learning algorithm that learns initializations that can quickly adapt to new tasks with few examples.

**Few-Shot Learning**
:   Machine learning with very few training examples per class.

**Neural Processes**
:   A family of models that combine neural networks with Gaussian processes for uncertainty quantification.

**Do-Calculus**
:   A set of rules for reasoning about interventions in causal models, developed by Judea Pearl.

---

## MGAN-DR-Specific Terms

**Graph Attention Network (GAT)**
:   A neural network that uses attention mechanisms to weight the importance of neighboring nodes in a graph.

**Multi-Head Attention**
:   An attention mechanism that runs multiple attention operations in parallel, capturing different types of relationships.

**Cross-Modal Attention**
:   Attention mechanism that aligns and integrates information from different data modalities.

**Hierarchical Learning**
:   Learning representations at multiple levels of abstraction, from low-level features to high-level concepts.

**Multi-Modal Learning**
:   Learning from multiple types of data simultaneously (e.g., gene expression + molecular structure).

---

## Evaluation Metrics

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| **Precision** | TP / (TP + FP) | How many predicted positives are correct |
| **Recall** | TP / (TP + FN) | How many actual positives are found |
| **F1 Score** | 2 × (P × R) / (P + R) | Harmonic mean of precision and recall |
| **AUROC** | Area under ROC curve | Overall ranking quality |
| **AUPRC** | Area under PR curve | Ranking quality for positives |

Where:

- **TP** = True Positives (correctly predicted AEDs)
- **FP** = False Positives (non-AEDs predicted as AEDs)
- **FN** = False Negatives (AEDs predicted as non-AEDs)
- **TN** = True Negatives (correctly predicted non-AEDs)

---

## Data & Preprocessing

**Z-Score Normalization**
:   Transforming data to have mean 0 and standard deviation 1: $z = (x - \mu) / \sigma$

**StandardScaler**
:   A scikit-learn transformer that applies z-score normalization.

**Stratified Split**
:   A train/test split that preserves the class distribution in both sets.

**Weighted Sampling**
:   Sampling strategy that over-samples minority classes to balance training batches.

