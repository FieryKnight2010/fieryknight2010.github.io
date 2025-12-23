# CTDN Architecture

Detailed explanation of the CTDN model architecture.

---

## Architecture Diagram

```
Input (978 genes)
    |
[Preprocessing: StandardScaler]
    |
[Causal Discovery Module]
    ├─ Structural Encoder (978 → 512)
    ├─ Causal Adjacency Matrix Predictor
    └─ Intervention Effect Estimator
    |
[Diffusion Propagation Module]
    ├─ Learnable Diffusion Schedule (10 timesteps)
    ├─ Denoising Network (UNet-style)
    └─ Forward/Reverse Diffusion Processes
    |
[Temporal Dynamics Module]
    ├─ Bidirectional LSTM (2 layers, hidden=128)
    ├─ Temporal Attention (8 heads)
    └─ Time-aware Feature Aggregation
    |
[Multi-Head Attention Layer]
    ├─ Self-Attention (8 heads)
    └─ Cross-Modal Attention
    |
[Classifier Head]
    ├─ Dense Layer (256 → 128 → 64)
    ├─ Dropout (0.3)
    └─ Output (64 → 1)
    |
[Sigmoid → Probability]
```

---

## Key Components

### 1. Causal Discovery Module

Learns structural causal relationships using neural structural equation models:

- Enforces DAG (Directed Acyclic Graph) constraints
- Estimates intervention effects (do-calculus)
- Discovers true causal relationships beyond correlations

### 2. Diffusion Propagation Module

Models drug effects as diffusion processes:

- **Forward diffusion**: Drug → Immediate targets → Downstream effects
- **Reverse diffusion**: Denoises observations to predict clean drug effects
- **Learnable beta schedule**: Adapts to biological timescales

### 3. Temporal Dynamics Module

Captures time-dependent drug effects:

- Bidirectional LSTM models temporal dependencies
- Multi-head temporal attention weights time points
- Handles variable-length drug response trajectories

### 4. Meta-Learning Component

MAML (Model-Agnostic Meta-Learning) for few-shot learning:

- Learns general drug representations from all data
- Quickly adapts to new drug classes with limited examples
- **Inner loop**: Drug-specific adaptation
- **Outer loop**: General learning

---

## Loss Function

### Focal Loss + Causal Regularization

$$
\text{Total Loss} = \text{Focal Loss} + \lambda_1 \cdot \text{Causal Reg} + \lambda_2 \cdot \text{Diffusion Reg}
$$

**Focal Loss:**

$$
FL(p_t) = -\alpha(1 - p_t)^\gamma \cdot \log(p_t)
$$

Where:

- $\alpha = 0.75$ (weight for positive class)
- $\gamma = 2.0$ (focusing parameter)

**Causal Regularization:**

$$
\text{Causal Reg} = ||A \odot A^T - I||_F
$$

(DAG constraint)

**Diffusion Regularization:**

$$
\text{Diffusion Reg} = KL(q(x_t | x_0) || p(x_t))
$$

(Diffusion consistency)

**Hyperparameters:**

- $\lambda_1 = 0.01$
- $\lambda_2 = 0.001$

---

## Training Strategy

1. **Class-weighted sampling**: Sample minority class 11x more frequently
2. **Focal loss**: Focus on hard examples
3. **Causal regularization**: Enforce valid causal structures
4. **Early stopping**: Patience of 20 epochs on validation AUROC
5. **Optimizer**: AdamW with weight decay 1e-4
6. **Learning rate**: 0.001 with cosine annealing
7. **Batch size**: 32

---

## Hyperparameters

```python
# Model architecture
HIDDEN_DIM = 256
N_HEADS = 8
N_TIMESTEPS = 10  # Diffusion timesteps
LSTM_HIDDEN = 128
LSTM_LAYERS = 2

# Training
BATCH_SIZE = 32
LEARNING_RATE = 0.001
WEIGHT_DECAY = 1e-4
MAX_EPOCHS = 100
EARLY_STOP_PATIENCE = 20

# Loss function
FOCAL_ALPHA = 0.75
FOCAL_GAMMA = 2.0
CAUSAL_REG_LAMBDA = 0.01
DIFFUSION_REG_LAMBDA = 0.001

# Class imbalance
CLASS_WEIGHTS = {0: 1.0, 1: 11.0}

# Reproducibility
RANDOM_SEED = 2024
```
